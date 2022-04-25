Wartungsprozess
---------------

Der Wartungsprozess dient dazu, den Inhalt der Syncler Datenbank von alten Daten zu bereinigen.
Es werden Warteschlangeneinträge, Protokolle, Sicherungen und Änderungsdatensätze abhängig vom Alter entfernt.

Bei der Wartung von Sicherungsdatensätzen gibt es eine Besonderheit.
Der erste und letzte Eintrag zu einem Datensatz wird nicht automatisch gelöscht.
Dies soll den initialen Zustand und die letzte Veränderung vorhalten.
Vor allem der letzte Eintrag soll die Untersuchung von Fehlerquellen ermöglichen, was nicht abhängig vom Alter ist.

Wenn kein Wartungsprozess eingerichtet wird, führt Syncler eine tägliche Zwangswartung durch.
Dabei wird das Standardalter von 14 Tagen angewendet.

Wenn ein abweichendes Alter gewünscht ist, muss ein Wartungsprozess eingerichtet werden.
Falls dieser nicht in die Warteschlange eingereiht wird, wird er ebenfalls täglich automatisch ausgeführt.

Das Erhöhen des maximalen Alters führt zu einem größeren Bedarf an Datenbank-Speicherplatz.
Da dieser limitiert ist, kann dies zur Unterbrechung der Synchronisation führen.
In den Einstellungen kann die aktuelle und maximale Datenbankgröße eingesehen werden.


