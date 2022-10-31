Einstellungen für Prozesse (Draft)
==========================

Jeder Prozess verfügt über verschiedene Einstellungen.
Spezialisierte Prozesse können zusätzliche Einstellungen haben oder auch Einstellungen ausblenden.
Im Folgenden sind allgemeine Prozesseinstellungen beschrieben.

Zurückschreiben
---------------

In einigen Prozess ist die Möglichkeit, Daten im Quellsystem zu aktualisieren, implementiert.
In Prozessen mit reproduzierbaren Daten wird für die Aktualisierung der Quelldatensatz verwendet.
In Prozessen mit nicht reproduzierbaren Daten, sogenannten Abfrage-Prozessen, kann das Schema und die ID-Felder oder ein auswertbarer Filter für die Aktualisierung angegeben werden.

Das Zurückschreiben unterscheidet 3 Fälle, bei erfolgreicher Verarbeitung, bei fehlerhafter Verarbeitung und bei Überspringen des Datensatzes.