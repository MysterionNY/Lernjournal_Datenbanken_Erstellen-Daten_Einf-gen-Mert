# DBMS

## Zusammenfassung Datenbanksysteme (DBS / DBMS)

**1. Begriff & Aufbau**  
- **Datenbanksystem (DBS):** Software + Datenbestand zur elektronischen Verwaltung großer Datenmengen.  
- **Datenbankmanagementsystem (DBMS):** Verwaltungskomponente, die Speicherung, Konsistenz und Zugriffskontrolle übernimmt.  
- **Datenbank (DB):** Die tatsächlichen, persistent gespeicherten Daten.

**2. Kernfunktionen eines DBMS**  
1. **Integrierte Datenhaltung**  
   - Einheitliche Ablage aller Daten– keine Mehrfachspeicherung von logischen Daten­elementen  
   - Definition komplexer Beziehungen, Verknüpfungen, kontrollierte Redundanz  
2. **Datenbanksprache**  
   - **DQL/DRL (SELECT)** – Abfragen  
   - **DDL (CREATE, ALTER, DROP)** – Strukturdefinition  
   - **DML (INSERT, UPDATE, DELETE)** – Datenmanipulation  
   - **DCL (GRANT, REVOKE)** – Rechteverwaltung  
   - **TCL (COMMIT, ROLLBACK)** – Transaktionskontrolle  
3. **Katalog (Data Dictionary)**  
   - Metadaten über Tabellen, Spalten, Beziehungen, Constraints  
4. **Benutzersichten (Views)**  
   - Externe Schemata für unterschiedliche Benutzer­anforderungen  
5. **Konsistenz- und Integritätskontrolle**  
   - Constraints (Prüfbedingungen)  
   - Physische Integritätsprüfung (Speicher­konsistenz)  
6. **Zugriffskontrolle (Access Control)**  
   - Benutzer- und Rollen-Rechte auf Tabellen, Spalten und Views  
7. **Transaktionen & Mehrbenutzerfähigkeit**  
   - Atomarität, Konsistenz, Isolation, Dauerhaftigkeit (ACID)  
   - Sperr- und Synchronisations­mechanismen  
8. **Datensicherung & Recovery**  
   - Backup/Restore, Journaling, Crash-Recovery

**3. Vorteile eines DBMS**  
- Standardisierung von Daten­namen und Formaten  
- Effiziente Speicherung & Retrieval großer Daten­mengen  
- Kürzere Entwicklungs­zeiten durch fertige DB-Funktionen  
- Hohe Flexibilität (Daten­unabhängigkeit)  
- Hohe Verfügbarkeit & gleichzeitiger Zugriff  
- Kosteneinsparung durch Zentralisierung

**4. Nachteile eines DBMS**  
- Hohe Anschaffungs- und Betriebskosten  
- Geringere Performance in Spezialfällen  
- Komplexität: Fachpersonal (DBA) erforderlich  
- Kosten für Security, Concurrency-Management  
- Single Point of Failure (Lösung: verteilte DB)

**5. Wann statt DBMS reguläre Dateien?**  
- Kein Mehr­benutzer­zugriff nötig  
- Harte Echtzeit­anforderungen  
- Sehr einfache, unveränderliche Daten­strukturen

## DB-Ranking

### Vergleich: Ursprüngliche Liste vs. Aktuelles DB-Engines Ranking (April 2025)

| DBMS               | Hersteller        | In Top 10? (Rang) |
|--------------------|-------------------|-------------------|
| Adabas             | Software AG       | Nein              |
| Cache              | InterSystems      | Nein              |
| IBM Db2            | IBM               | Ja (9)            |
| Firebird           | —                 | Nein              |
| IMS                | IBM               | Nein              |
| Informix           | IBM               | Nein              |
| InterBase          | Borland           | Nein              |
| MS Access          | Microsoft         | Nein              |
| MS SQL Server      | Microsoft         | Ja (3)            |
| MySQL              | MySQL AB          | Ja (2)            |
| Oracle             | Oracle            | Ja (1)            |
| PostgreSQL         | —                 | Ja (4)            |
| Sybase ASE         | Sybase            | Nein              |
| Versant            | Versant           | Nein              |
| Visual FoxPro      | Microsoft         | Nein              |
| Teradata           | NCR Teradata      | Nein              |

### Mindmap der Top 10 DB-Engines
mindmap
  root((Top 10 DB-Engines))
    Oracle
    MySQL
    Microsoft SQL Server
    PostgreSQL
    MongoDB
    Snowflake
    Redis
    Elasticsearch
    IBM Db2
    SQLite
