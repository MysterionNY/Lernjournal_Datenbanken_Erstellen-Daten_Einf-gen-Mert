# Forward Engineering eines Datenbankmodells

### 1.1 Modell erstellen
- Erstelle in deinem Modellierungs‐Tool (z. B. MySQL Workbench) ein ER-Diagramm  
  - Verwende dein Tourenplaner-Modell oder ein eigenes Beispiel mit mind. 3 Tabellen und Beziehungen  

### 1.2 Forward Engineering starten
1. **Forward Engineering**-Assistent öffnen  
2. **Ziel‐Datenbank** auswählen (z. B. MySQL auf TBZ-Cloudserver, localhost:127.0.0.1 oder AWS-Instanz)  
3. **Benutzername/Passwort** eingeben  
4. **Optionen wählen**  
   - DDL-Statements (CREATE SCHEMA, CREATE TABLE, ALTER TABLE, FOREIGN KEYS)  
   - ggf. Indizes, Views, Stored Procedures  
   - Filter, was nicht erzeugt werden soll  

### 1.3 SQL-Skript sichern
- Klicke auf **Save to File…** und sichere das generierte SQL-Script (z. B. `tourenplaner_forward.sql`)  
- Füge das SQL-Script in dein Lernportfolio ein oder verlinke es  

### 1.4 Skript auf DB-Server übertragen
- Mit **Next** die Statements an den Server senden  
- Verbindung prüfen: keine Fehlermeldungen  

### 1.5 Struktur im DB-Server prüfen
USE AufgabenDB;
SHOW TABLES;
DESCRIBE Tour;
DESCRIBE Teilnehmer;
DESCRIBE Tour_Ort;
