Einstellungen für Prozesse (Draft)
==========================

Jeder Prozess verfügt über verschiedene Einstellungen.
Spezialisierte Prozesse können zusätzliche Einstellungen haben oder auch Einstellungen ausblenden.
Im Folgenden sind allgemeine Prozesseinstellungen beschrieben.

Allgemein
---------

:Name:

Der Name dient der Identifikation eines Prozesses.

:Beschreibung:

Die Beschreibung ist ein Zusatz zum Namen, den nur der Administrator angezeigt bekommt.

:Kategorie:

Mit dieser freien Eingabe eines Kategorienames kann die Anzeige im Syncler-Administrator strukturiert werden.

:Laufende Nummer des Mandanten:

Diese Nummer struktuiert die synchronisierten Daten in Mandanten.
In Systemen wie Sage CRM, CAS oder Salesforce können die Sync-Statusfelder zu den Stammdaten nummeriert angegeben werden.
Dies steuert, welche Prozesse auf den Datensatz zugreifen dürfen und damit auch, welches Ziel der Datensatz hat.
Diese Nummer wird aber auch für Datenabbildungen verwendet.
Ein Prozess sucht nur nach vorhandenen Datenabbildung für seine laufende Nummer und auch nur diese Datenabbildungen
werden ggf. erzeugt oder aktualisiert.
Durch die Verwendung von unterschiedlichen Nummern können Datensätze dadurch auch gezielt doppelt angelegt werden.

Siehe :doc:`/bestpractices/clientnumber`











Zurückschreiben
---------------

In einigen Prozess ist die Möglichkeit, Daten im Quellsystem zu aktualisieren, implementiert.
In Prozessen mit reproduzierbaren Daten wird für die Aktualisierung der Quelldatensatz verwendet.
In Prozessen mit nicht reproduzierbaren Daten, sogenannten Abfrage-Prozessen, kann das Schema und die ID-Felder oder ein auswertbarer Filter für die Aktualisierung angegeben werden.

Das Zurückschreiben unterscheidet 3 Fälle, bei erfolgreicher Verarbeitung, bei fehlerhafter Verarbeitung und bei Überspringen des Datensatzes.