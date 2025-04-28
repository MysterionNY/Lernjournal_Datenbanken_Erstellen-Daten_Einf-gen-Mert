# Projekt Freifächer–Datenbank

## 1  Excel → 1. Normalform (1 NF) & CSV‑Exporte

| Ursprüngliche Spalte | Atomare Aufteilung (1 NF)             | Beispiel‑CSV (`;`‑Separator) |
|---------------------|----------------------------------------|--------------------------------|
| Schüler             | `schueler_id`; `vorname`; `nachname`  | **Schueler.csv**<br>1;Inge;Sommer |
| Geb.-Datum          | `geburtsdatum`                         | (s. oben) |
| Klasse              | `klasse_id`; `klassenbezeichnung`      | **Klasse.csv**<br>1;2a |
| Freifach            | `freifach_id`; `bezeichnung`           | **Freifach.csv**<br>1;Chor |
| Lehrer              | `lehrer_id`; `vorname`; `nachname`     | **Lehrer.csv**<br>1;Anna;Meier |
| Kombinationen       | `teilnahme_id`; \<FKs Schüler/Klasse/Freifach/Lehrer> | **Teilnahme.csv**<br>1;1;1;1;1 |

---

## 2  Logisches ERD (mind. 2 NF)

```
Schueler   1——∞  Teilnahme  ∞——1  Freifach
               ∞         ∞
                \       /
                 1——∞  Klasse
                   |
                   ∞
                  Lehrer
```

| Tabelle    | Primärschlüssel | Wichtige Attribute | Kardinalitäten | Bemerkungen |
|------------|-----------------|--------------------|----------------|-------------|
| Schueler   | schueler_id PK  | vorname, nachname, geburtsdatum | 1 Schueler hat 0…* Teilnahmen | – |
| Klasse     | klasse_id PK    | klassenbezeichnung              | 1 Klasse hat 0…* Schüler / 0…* Teilnahmen | – |
| Freifach   | freifach_id PK  | bezeichnung                     | 1 Freifach hat 0…* Teilnahmen | – |
| Lehrer     | lehrer_id PK    | vorname, nachname               | 1 Lehrer leitet 0…* Teilnahmen | – |
| Teilnahme  | teilnahme_id PK | FK schueler_id, klasse_id,<br>FK freifach_id, lehrer_id | – | Brückentabelle |

---

## 3  Physisches ERD & SQL‑DDL (Forward Engineering)

```sql
CREATE DATABASE IF NOT EXISTS Freifaecher DEFAULT CHARACTER SET utf8mb4;
USE Freifaecher;

-- 1) Basis­tabellen -------------------------------------------------
CREATE TABLE Klasse (
  klasse_id          INT AUTO_INCREMENT PRIMARY KEY,
  klassenbez         VARCHAR(10) NOT NULL UNIQUE
) ENGINE=InnoDB;

CREATE TABLE Freifach (
  freifach_id        INT AUTO_INCREMENT PRIMARY KEY,
  bezeichnung        VARCHAR(50) NOT NULL UNIQUE
) ENGINE=InnoDB;

CREATE TABLE Lehrer (
  lehrer_id          INT AUTO_INCREMENT PRIMARY KEY,
  vorname            VARCHAR(40) NOT NULL,
  nachname           VARCHAR(40) NOT NULL,
  CONSTRAINT uq_lehrer_name UNIQUE (vorname, nachname)
) ENGINE=InnoDB;

CREATE TABLE Schueler (
  schueler_id        INT AUTO_INCREMENT PRIMARY KEY,
  vorname            VARCHAR(40) NOT NULL,
  nachname           VARCHAR(40) NOT NULL,
  geburtsdatum       DATE        NOT NULL,
  klasse_id          INT NOT NULL,
  CONSTRAINT fk_schueler_klasse FOREIGN KEY (klasse_id)
            REFERENCES Klasse (klasse_id)
            ON UPDATE CASCADE ON DELETE RESTRICT
) ENGINE=InnoDB;

-- 2) Brückentabelle -------------------------------------------------
CREATE TABLE Teilnahme (
  teilnahme_id       INT AUTO_INCREMENT PRIMARY KEY,
  schueler_id        INT NOT NULL,
  freifach_id        INT NOT NULL,
  lehrer_id          INT NOT NULL,
  UNIQUE (schueler_id, freifach_id),   -- 1 Schüler <= 1 Teilnahme je Freifach
  CONSTRAINT fk_teiln_schueler FOREIGN KEY (schueler_id) REFERENCES Schueler(schueler_id),
  CONSTRAINT fk_teiln_freifach FOREIGN KEY (freifach_id) REFERENCES Freifach(freifach_id),
  CONSTRAINT fk_teiln_lehrer   FOREIGN KEY (lehrer_id)   REFERENCES Lehrer(lehrer_id)
) ENGINE=InnoDB;
```

---

## 4  CSV‑Import per `LOAD DATA`

```sql
LOAD DATA LOCAL INFILE '/path/to/Klasse.csv'
INTO TABLE Klasse
FIELDS TERMINATED BY ';'
LINES TERMINATED BY '\n'
(klasse_id, klassenbez);

LOAD DATA LOCAL INFILE '/path/to/Freifach.csv'
INTO TABLE Freifach
FIELDS TERMINATED BY ';'
LINES TERMINATED BY '\n'
(freifach_id, bezeichnung);

-- usw. für Schueler.csv, Lehrer.csv, Teilnahme.csv
```

> Kontroll­abfrage nach jedem Import (Beispiel):
> ```sql
> SELECT COUNT(*) FROM Schueler;
> SELECT COUNT(*) FROM Teilnahme WHERE schueler_id NOT IN (SELECT schueler_id FROM Schueler);
> ```

---

## 5  Daten­bereinigung

Beispiel‑Cleanup‑Skripte (leere Nachnamen, Dubletten …):

```sql
-- Leere Strings → NULL
UPDATE Schueler SET nachname = NULL WHERE TRIM(nachname) = '';

-- Dubletten in Lehrer (Gleicher Name → ersten behalten)
DELETE l2 FROM Lehrer l1
JOIN Lehrer l2 ON l1.lehrer_id < l2.lehrer_id
              AND l1.vorname = l2.vorname AND l1.nachname = l2.nachname;
```

---

## 6  Tests – Soll/Ist vergleichen

```sql
-- z. B. # Schüler pro Klasse (Quelle CSV vs. DB)
SELECT klassenbez, COUNT(*) AS anzahl
FROM   Schueler s JOIN Klasse k USING (klasse_id)
GROUP  BY k.klasse_id
ORDER  BY klassenbez;
```

*(Gleiche Abfrage auf CSV mit Excel/LibreOffice oder über `csvsql`.)*

---

## 7  +290 Test­datensätze generieren

```sql
-- Faker‑Beispiel (falls du Python + Faker nutzen willst)
-- python - <<EOF
-- from faker import Faker, providers; import csv, random, datetime
-- fake = Faker('de_DE');
-- with open('Schueler_extra.csv','w',newline='') as f:
--     w = csv.writer(f, delimiter=';')
--     for i in range(290):
--         dt = fake.date_between_dates(date_start=datetime.date(2005,1,1), date_end=datetime.date(2008,12,31))
--         w.writerow(['', fake.first_name(), fake.last_name(), dt, random.randint(1,6)])
-- EOF
```

Danach erneut **Punkte 4–6** ausführen.

---

## 8  Abfrage‑Aufgaben

```sql
-- 8.1  Teilnehmerzahl bei Freifach‑Leiterin Inge Sommer
SELECT COUNT(*) AS teilnehmer_ingesommer
FROM   Teilnahme t
JOIN   Schueler  s  ON t.schueler_id = s.schueler_id
JOIN   Lehrer    l  ON t.lehrer_id   = l.lehrer_id
WHERE  l.vorname = 'Inge' AND l.nachname = 'Sommer';

-- 8.2  Klassen + Anzahl SchülerInnen in Freifächern
SELECT k.klassenbez, COUNT(*) AS anzahl_teilnehmer
FROM   Teilnahme t
JOIN   Schueler s  ON t.schueler_id = s.schueler_id
JOIN   Klasse  k  ON s.klasse_id   = k.klasse_id
GROUP  BY k.klasse_id
ORDER  BY k.klassenbez;

-- 8.3  SchülerInnen im Freifach „Chor" oder „Elektronik"
SELECT s.vorname, s.nachname, f.bezeichnung
FROM   Teilnahme t
JOIN   Schueler s ON t.schueler_id = s.schueler_id
JOIN   Freifach f ON t.freifach_id = f.freifach_id
WHERE  f.bezeichnung IN ('Chor','Elektronik');
```

### Ergebnisse in Datei speichern (`SELECT … INTO OUTFILE`)

```sql
SELECT k.klassenbez, COUNT(*) AS anzahl_teilnehmer
INTO OUTFILE '/tmp/klassen_teilnehmer.csv'
FIELDS TERMINATED BY ';' LINES TERMINATED BY '\n'
FROM   Teilnahme t
JOIN   Schueler s ON t.schueler_id = s.schueler_id
JOIN   Klasse  k ON s.klasse_id   = k.klasse_id
GROUP  BY k.klasse_id;
```

*(analog für die anderen beiden Abfragen)*

---

## 9  Backup der DB `Freifaecher`

```bash
mysqldump -u backup_user -p --databases Freifaecher \
          --routines --events --triggers \
          --single-transaction --quick --add-drop-table \
          > Freifaecher_backup_$(date +%F).sql
```
