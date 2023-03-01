Support-Datenbank
=================

Die Support-Datenbank ist eine zusätzliche Funktion zum Speichern und Aufbereiten von Daten.
Es wird eine SQL-Datenbank bereitgestellt, die die Ausführung von SQL-Anweisungen zulässt und in der beliebig Tabellen angelegt werden können.
Auch können Daten aus Excel- oder CSV-Dateien direkt in eine neue automatisch erstellte Tabelle importiert werden.

Die Support-Datenbank steht zur Verfügung, sobald das Feature für den Mandanten aktiviert wurde.
Alle Berechtigungen bei der Benutzung sind auf diese Datenbank beschränkt.
Zugriff auf die Synchronisationsdatenbank werden nicht gewährt.

Sobald das Feature aktiviert wurde, wird der verbrauchte Datenbankspeicher aus beiden Datenbanken summiert.
Unter Umständen ist das Limit der Datenbankgröße dann anzupassen.

In der Admin-Oberfläche steht eine Übersicht zu den vorhandenen Tabellen zur Verfügung und die Inhalte der Tabellen können direkt bearbeitet, eingefügt oder gelöscht werden.
Auch können ganze Tabellen angelegt oder direkt gelöscht werden.

Beim Anlegen einer Tabelle muss ein Name festgelegt werden.
Danach können die gewünschten Spalten in einer Liste angegeben werden.
Dabei kann auch eine Spalte als Auto-ID-Spalte definiert werden.
Dies ermöglich einen optimalen Einsatz in Prozessen.

Es steht eine Import-Funktion für Excel- und CSV-Dateien zur Verfügung. Diese Import-Funktion erstellt automatisch eine neue Tabelle und legt Spalten und Inhalte an.
Die erste Zeile in der Datei wird für die Spaltenbezeichnung verwendet.
Über die zweite Zeile in der Datei wird der Datentyp für die erzeugte Spalte bestimmt.
Besonders muss hier auf Ganz- und Kommazahlen geachtet werden. Eine Ganzzahl wird eine entsprechende Spalte in der Tabelle anlegen.
Sollte in weiteren Zeilen dann Kommazahlen folgen, werden diese nicht importiert.
Es wird automatisch eine ID-Spalte der Import-Tabelle hinzugefügt, damit diese optimal eingesetzt werden kann.

Eine nachträgliche Bearbeitung der Tabellenstruktur wird nicht unterstützt.

Es wird auch eine Export-Funktion bereitgestellt, mit der eine komplette Tabelle als Excel-Datei exportiert werden kann.

Die Support-Datenbank-Verbindung
--------------------------------

Für den Einsatz der Support-Datenbank in Prozessen steht eine eigene Verbindung zur Verfügung.
Für diese Verbindung kann optional ein geschachtelteter Datentyp definiert werden.
Weitere Konfiguration sind nicht erforderlich.
Die Schema-Objekte werden über die vorhandenen Tabellen erstellt.

Diese Verbindung kann wie eine SQL-Verbindung in Prozessen zum Lesen, Schreiben oder für Anweisungen verwendet werden.