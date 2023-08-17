SalesViewer
===========

SalesViewer ist ein Anbieter zum Überwachen Ihrer Webseite.
Anonyme Website-Besucher können damit in Firmendaten aufgelöst werden.
Zusätzlich stehen Informationen zum Besuch und den Interessen zur Verfügung.

Die SalesViewer-Verbindung bietet Schemaobjekte für die Sitzung, den Besuch und die Firma an.
Diese können mit Universalprozessen in jedes beliebige System übertragen werden.

Die Daten können dabei kontinuierlich abgerufen und verarbeitet werden.

Für die Einrichtung der Verbindung benötigen Sie lediglich den API Key.
Dazu melden Sie sich im SalesViewer Portal an und rufen den Menüpunkt "Projekte und Trackingcode" auf.
Hier können Sie den API Key einsehen.

Beim Anlegen der SalesViewer-Verbindung übertragen Sie nur diesen API Key in das Feld "API Key" und speichern die Verbindung.

Funktionen
----------

:Schema ermitteln:

Die Verbindung stellt automatisch die Objekte company, session und visit zur Verfügung.
Die Objekte enthalten eine Datum für die kontinuierliche Verarbeitung und einen Schlüssel für die Beziehungen zwischen den Objekten.
Dabei sind Besuche (visit) einer Sitzung (session) und Sitzungen einer Firma (company) zugeordnet.

:Lesen von Schema-basierten Daten:

Das Lesen kann vollständig oder kontinuierlich erfolgen.
Das gezielte Abrufen eines Datensatzes wird nicht unterstützt.
Bei einer Verarbeitung aller Objekte sollte deshalb die Reihenfolge der Beziehungen beachtet und dies 
ggf. durch einen Ablauf gesteuert werden.

:Lesen von Abfrage-basierten Daten:

Diese Funktion wird nicht unterstützt.

:Schreiben von Daten:

Diese Funktion wird nicht unterstützt.


Einstellungen
-------------

Nur die Einstellung "API Key" muss festgelegt werden.
Alle anderen Einstellungen können ignoriert werden.

