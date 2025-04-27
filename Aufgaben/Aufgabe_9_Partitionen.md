# Partition, Storage Engine & Tablespace (InnoDB)

### 1.1 Partition (Datenbanken)
- **Definition:** Aufteilung einer großen Datenbank-Tabelle oder -Datenbank in kleinere, unabhängige Teile (Partitionen). Jede Partition enthält einen disjunkten Teil der Daten, aber zusammen repräsentieren alle Partitionen den gesamten Datensatz.  
- **Arten:**
  - *Horizontale Partitionierung* (Shard, Subtable): Zeilen werden nach Kriterien (z. B. Datum, geografische Region) verteilt.  
  - *Vertikale Partitionierung:* Spalten oder Spalten-Gruppen werden getrennt abgelegt.  
- **Ziele:** Skalierbarkeit, Manageability, Performance-Optimierung, Verfügbarkeit und Lastverteilung  

### 1.2 Storage Engine
- **Definition:** Kernkomponente eines DBMS, die die physischen CRUD-Operationen (Create, Read, Update, Delete) auf den Datendateien übernimmt.  
- **Funktion:** Verwaltung von Datenseiten, Sperr­mechanismen, Transaktionen, Indizes, Puffer-Pooling, Crash-Recovery.  
- **Beispiele (MySQL):**  
  - **InnoDB:** Transaktional, MVCC, Foreign Keys, ACID  
  - **MyISAM:** Non-transaktional, Full-Text-Index, schneller bei reinen Lese­zugriffen  
  - **Memory:** Daten im RAM, sehr schnell, flüchtig  


### 1.3 Tablespace (InnoDB)
- **Definition:** Logische Einheit in InnoDB, die eine oder mehrere physische Datendateien (`ibdata-N` oder `.ibd`) kapselt und darauf Tabellen sowie Indexstrukturen speichert.  
- **Typen:**
  - **System Tablespace:**
