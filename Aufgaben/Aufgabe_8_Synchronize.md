# Synchronize Model

1. **Modell anpassen**  
   - Füge im ER-Diagramm eine neue Tabelle `tbl_MA` hinzu (z. B. für Administrationszwecke)  
   - Ziehe eine Relation von `tbl_MA` zu einer bestehenden Tabelle, z. B. `tbl_Tour`  
   - Erweitere eine bestehende Tabelle, z. B. `tbl_Tour`, um ein neues Attribut `Beschreibung VARCHAR(255)`

2. **Synchronize Model**  
   - Rechtsklick auf das Physical Schema → **Edit Schema** und ggf. Schema-Name anpassen  
   - Menü **Database → Synchronize Model…** öffnen  
   - Verbindung zum Ziel-Server (z. B. localhost:3306, AWS-Endpoint o. Ä.)  
   - Im Assistenten die Unterschiede zwischen Modell und DB-Schema prüfen  
   - Generierte DDL-Scripts anwenden oder in Datei exportieren  

3. **Ergebnis prüfen**  
   USE AufgabenDB;
   SHOW TABLES LIKE 'tbl_MA';
   DESCRIBE tbl_Tour;
