CAS (Draft)
===

Beschreibung

Funktionen
----------

:Schema ermitteln:

:Laden von Quelldaten:

:Laden von Schema-basierten Daten:

:Laden von Abfrage-basierten Daten:

:Schreiben von Daten:

:Schreiben von Bulk-Daten:

	Diese Funktion wird nicht unterstützt.


Einstellungen
-------------


Besonderheiten
--------------

Das Zuweisen einer leeren Guid für Link-Ziele überspringt die Anlage.

Für die Archivierung von Emails kann das Objekt "EMAILSTORE" verwendet werden.
Dieses verfügt über ein Feld "FileContent". Wenn Sie dort eine Email im EML-Format als Base64 Zeichenkette zuweisen, wird die Email im CAS archiviert.
Die restlichen Felder können für zusätzliche Daten, wie z.B. Verknüpfungen verwendet werden.
Die Archivierung wird nur mit neuen Datensätzen ausgeführt. Sollte es sich um einen bekannten Datensatz handelt, wird die Archivierung übersprungen.

