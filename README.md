# Lernjournal_M164_Mert_AP24a

Ein persönliches Lernjournal für das Modul **M164 – Datenbanken: Erstellen & Daten einfügen**. Hier findest du alle Theorie-Notizen, SQL-Skripte und Aufgabenlösungen geordnet nach den Unterrichtstagen.

## Inhaltsverzeichnis
- [Was ist SQL?](#was-ist-sql)
- [Wer hat SQL erfunden?](#wer-hat-sql-erfunden)
- [Wozu wird SQL verwendet?](#wozu-wird-sql-verwendet)
- [Aufgaben und Links](#aufgaben-und-links)
  - [Tag 1 – Grundlagen & Modellierung](#tag-1--grundlagen--modellierung)
  - [Tag 2 – Forward-Engineering & Partitionierung](#tag-2--forward-engineering--partitionierung)
  - [Tag 3 – Datendefinition & -manipulation](#tag-3--datendefinition--manipulation)
  - [Tag 4 – Mengenlehre & Joins](#tag-4--mengenlehre--joins)
  - [Tag 5 – Datenintegrität & Aggregation](#tag-5--datenintegrität--aggregation)
- [Bilder](#bilder)
- [Credits](#credits)

---

## Was ist SQL?

**SQL (Structured Query Language)** ist eine deklarative Sprache, mit der relationale Datenbanken definiert (*Data Definition Language – DDL*), abgefragt (*Data Query Language – DQL*) und manipuliert (*Data Manipulation Language – DML*) werden. Sie erlaubt es, komplexe Informationen aus tabellarisch strukturierten Datenbeständen effizient auszuwählen, zu verändern und zu verwalten – unabhängig von der konkreten Datenbank-Implementation.

## Wer hat SQL erfunden?

SQL geht auf die Sprache **SEQUEL** zurück, die 1974 von **Donald D. Chamberlin** und **Raymond F. Boyce** bei IBM Research (San José) entwickelt wurde. 1979 stellte Oracle die erste kommerzielle SQL-Implementierung vor, und 1986/1987 wurde SQL als ANSI- bzw. ISO-Standard normiert.

## Wozu wird SQL verwendet?

- **Schema-Definition:** Erstellen und Ändern von Tabellen, Views, Constraints und Indizes (DDL).
- **Datenabfragen:** Selektieren, Filtern und Aggregieren großer Datenmengen (SELECT).
- **Datenmanipulation:** Einfügen, Aktualisieren und Löschen von Datensätzen (INSERT, UPDATE, DELETE).
- **Transaktionskontrolle:** Atomare Ausführung mehrerer Anweisungen (COMMIT, ROLLBACK).
- **Berechtigungen & Sicherheit:** Zuweisen von Rechten oder Rollen (GRANT, REVOKE).

---

## Aufgaben und Links

### Tag 1 – Grundlagen & Modellierung
| # | Thema | Datei |
|---|-------|-------|
| 1 | Tourenplaner (ER-Modell) | [Aufgabe 1](Aufgaben/Aufgabe_1_Tourenplaner.md) |
| 2 | Normalisierung | [Aufgabe 2](Aufgaben/Aufgabe_2_Normalisierung.md) |

### Tag 2 – Forward-Engineering & Partitionierung
| # | Thema | Datei |
|---|-------|-------|
| 3 | Generalisierung | [Aufgabe 3](Aufgaben/Aufgabe_3_Generalisierung.md) |
| 4 | Beziehungsarten | [Aufgabe 4](Aufgaben/Aufgabe_4_Beziehungsarten.md) |
| 5 | DBMS Überblick | [Aufgabe 5](Aufgaben/Aufgabe_5_DBMS.md) |
| 6 | DDL – CREATE TABLE u.a. | [Aufgabe 6](Aufgaben/Aufgabe_6_DDL.sql) |
| 7 | Forward Engineering | [Aufgabe 7](Aufgaben/Aufgabe_7_Forward_Engineering.md) |
| 8 | Synchronize | [Aufgabe 8](Aufgaben/Aufgabe_8_Synchronize.md) |
| 9 | Partitionierung | [Aufgabe 9](Aufgaben/Aufgabe_9_Partitionen.md) |

### Tag 3 – Datendefinition & -manipulation
| # | Thema | Datei |
|---|-------|-------|
| 10 | Datentypen | [Aufgabe 10](Aufgaben/Aufgabe_10_Datentypen.md) |
| 11 | SELECT (Basis) | [Aufgabe 11](Aufgaben/Aufgabe_11_Select.sql) |
| 12 | INSERT | [Aufgabe 12](Aufgaben/Aufgabe_12_insert.sql) |
| 13 | UPDATE / DELETE / ALTER / DROP | [Aufgabe 13](Aufgaben/Aufgabe_13_update_delete_alter_drop.sql) |

### Tag 4 – Mengenlehre & Joins
| # | Thema | Datei |
|---|-------|-------|
| 14 | Mengenlehre | [Aufgabe 14](Aufgaben/Aufgabe_14_Mengenlehre.md) |
| 15 | JOINs | [Aufgabe 15](Aufgaben/Aufgabe_15_select_join.sql) |
| 16 | JOINs (Advanced) | [Aufgabe 16](Aufgaben/Aufgabe_16_select_join_adv.sql) |

### Tag 5 – Datenintegrität & Aggregation
| # | Thema | Datei |
|---|-------|-------|
| 17 | Referentielle Datenintegrität | [Aufgabe 17](Aufgaben/Aufgabe_17_Referentielle_Datenintegrität.md) |
| 18 | Referentielle Datenintegrität (Advanced) | [Aufgabe 18](Aufgaben/Aufgabe_18_Referentielle_Datenintegrität_Adv.md) |
| 19 | Aggregatsfunktionen | [Aufgabe 19](Aufgaben/Aufgabe_19_Aggregatsfunktionen.md) |
| 20 | GROUP BY | [Aufgabe 20](Aufgaben/Aufgabe_20_Select_group.md) |
| 21 | ORDER BY | [Aufgabe 21](Aufgaben/Aufgabe_21_order.md) |
| 22 | HAVING | [Aufgabe 22](Aufgaben/Aufgabe_22_select_having.md) |
| 23 | HAVING (Advanced) | [Aufgabe 23](Aufgaben/Aufgabe_23_Select_having_2.md) |