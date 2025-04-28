# Projekt Freifächer–Datenbank Teil 2

## 10  Stored Procedures (gespeicherte Prozeduren)

### 10.1  Hintergrund & Lernportfolio‑Eintrag
Gespeicherte Prozeduren (Stored Procedures) sind **vordefinierte SQL‑Blöcke**, die in der Datenbank abgelegt und beliebig oft aufgerufen werden können.

- **Wiederverwendbarkeit:** Einmal erstellt → ständig nutzbar.
- **Zentralisierung der Geschäftslogik:** Komplexe Abläufe liegen serverseitig, nicht in Client‑Skripten.
- **Performance:** Ausführung direkt im DB‑Server spart Netzwerk‑Round‑Trips.
- **Sicherheit:** Benutzer benötigen nur `EXECUTE`‑Rechte auf die Prozedur statt DML‑Rechte auf Tabellen.

### 10.2  Implementierte Prozeduren
```sql
DELIMITER $$

-- 1) Teilnehmerzahl je Lehrkraft ----------------------------------
CREATE PROCEDURE sp_GetTeilnehmerProLehrer (IN p_lehrer_id INT)
BEGIN
    SELECT l.lehrer_id,
           l.vorname,
           l.nachname,
           COUNT(t.teilnahme_id) AS anzahl_teilnehmer
    FROM   Lehrer l
    LEFT  JOIN Teilnahme t ON l.lehrer_id = t.lehrer_id
    WHERE  l.lehrer_id = p_lehrer_id
    GROUP BY l.lehrer_id;
END $$

-- 2) Klassenübersicht mit Aggregaten ------------------------------
CREATE PROCEDURE sp_KlassenUebersicht ()
BEGIN
    SELECT k.klassenbez,
           COUNT(DISTINCT s.schueler_id) AS anzahl_schueler,
           COUNT(t.teilnahme_id)         AS anzahl_freifachteilnahmen,
           MAX(t.teilnahme_id)           AS max_teilnahme_id
    FROM   Klasse k
    LEFT  JOIN Schueler  s ON k.klasse_id = s.klasse_id
    LEFT  JOIN Teilnahme t ON s.schueler_id = t.schueler_id
    GROUP  BY k.klasse_id
    ORDER  BY k.klassenbez;
END $$

-- 3) Freifach‑Statistik (AVG / MAX) --------------------------------
CREATE PROCEDURE sp_FreifachStatistik ()
BEGIN
    SELECT f.bezeichnung,
           COUNT(t.teilnahme_id) AS teilnehmer,
           MAX(t.teilnahme_id)   AS max_t_id,
           AVG(sub.cnt)          AS avg_pro_lehrer
    FROM   Freifach f
    LEFT  JOIN Teilnahme t ON f.freifach_id = t.freifach_id
    LEFT  JOIN (
        SELECT lehrer_id, freifach_id, COUNT(*) AS cnt
        FROM   Teilnahme
        GROUP  BY lehrer_id, freifach_id
    ) sub ON sub.freifach_id = f.freifach_id
    GROUP BY f.freifach_id;
END $$

DELIMITER ;
```

### 10.3  Aufrufbeispiele
```sql
CALL sp_GetTeilnehmerProLehrer(1);
CALL sp_KlassenUebersicht();
CALL sp_FreifachStatistik();
```

### 10.4  Rechte
```sql
GRANT EXECUTE ON PROCEDURE Freifaecher.sp_GetTeilnehmerProLehrer TO 'app_user'@'%';
GRANT EXECUTE ON PROCEDURE Freifaecher.sp_KlassenUebersicht     TO 'app_user'@'%';
GRANT EXECUTE ON PROCEDURE Freifaecher.sp_FreifachStatistik     TO 'app_user'@'%';
```


