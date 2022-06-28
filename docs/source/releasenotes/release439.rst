Release 4.3.9 - 28.06.2022
==========================

Änderungen
----------

Die erneute Eingabe eines Zoho Grant-Token aktualisiert auch aktuell verwendete Access-Token, damit geänderte 
Scopes sich direkt auswirken und nicht erst nach dem Refresh des Access-Tokens.

Sage 200 wurde in Infoniqa One 200 umbenannt.

Prozessvorlagen für Sage 100 und Microsoft 365 wurden überarbeitet.

Das Datenbanksystem MariaDB wird als Systemdatenbank und in der SQL-Verbindung unterstützt.
Für die Migration von Microsoft SQL-Server steht der Prozess "Syncler Datenbank Kopierprozess" zur Verfügung.
Mit diesem Prozess kann die aktuelle Datenbank in eine bereits vorhandene Datenbank kopiert werden.
ID-Werte bleiben dabei erhalten und der Prozess kann auch kontinuierlich verwendet werden.

Für Abfragen durch die REST API Verbindung wird die Url auch durch das Objekt geparst. 
Dadurch sind neben #name#, #idfield# und #id# auch weitere Parameter steuerbar.

Die Verbindungstypen SQL, CSV und Email stehen nicht mehr automatisch zur Verfügung, sondern müssen explizit bestellt werden.

Die aktuelle Schnittstelle zur Dynamics Business Central unterstützt keine Unterstriche in Feldbezeichnungen mehr.
Damit einen flexible Unterstützung gewährleistet ist, prüfen die Verbindung und die spezifischen Prozesse das ermittelte
Datenschema und passen ihre Abfragen dementsprechend an.

Im Syncler Administrator Testlauf einer Transformation wird der Offset zu Datumswerten ausgegeben.

Die Meldungen zu übersprungenen Datensätzen wurden für eine bessere Nachvollziehbarkeit angepasst.

Für Bulk-Prozesse wurde eine zusätzliche parallele Verarbeitung eingeführt, um die Gesamtdauer zu optimieren.
Die Nachbearbeitung (Resultat, Datenabbildung, Zurückschreiben) des Resulats wird parallel zur Datensatzverarbeitung
(Datenabbildung suchen, Ziel ermitteln) ausgeführt.

Die neue Transformation "Dokument konvertieren" ermöglich die Umwandlung bestimmter Typen.
Die Typen HTML, TXT, RTF, XML und DOCX können als Eingabetyp definiert werden.
Die Typen HTML, TXT, RTF, XML, DOCX, PDF und XPS können als Ausgabetyp definiert werden.
Die binären Typen DOCX, PDF und XPS werden als Base64 erwartet und geliefert.
Die Typen HTML, TXT und RTF werden als Zeichenkette erwartet und geliefert.

Es steht ein neuer Verbindungstyp "Tabellenkalkulation" zur Verfügung. Dieser kann ähnlich wie der
Seriendruck eingerichtet und eingesetzt werden.
Als Vorlagen können XLSX Dateien verwendet werden. Platzhalter werden mit der #..# Notation definiert.
Ranges, Bilder und Html-Inhalte werden wie im Seriendruck definiert.
Die Ausgabe kann auch per PDF erfolgen.

Die Serienbrief Verbindung legt das Zielverzeichnis an, falls es noch nicht vorhanden ist.

Die Verbindungsherstellung durch die SQL Verbindung wurde auf eine lokale Verbindung statt einer globalen umgestellt.
Damit werden Fehler aus paralleler Verarbeitung vermieden.

Korrekturen
-----------

Die Sortierung von Listen im Syncler Administrator wurde korrigiert.

Das Parsing von Json-Angaben für Picture-Felder im Seriendruck wurde korrigiert.

Wenn eine Abfrage über die REST API Verbindung nur ein Objekt ohne typische Antwortstruktur (data, success, ...)
liefert, wird dieses Objekt als Ergebnis verwendet.

In der CAS-Verbindung wird vor dem Speichern der Positionen zu Verkaufschancen oder Belegen geprüft, ob eine gültige
Etag vorliegt und ggf. wird diese angefordert. Durch die Konstellation unveränderter Datensatz und geänderte Positionen
konnte diese Fehlersituation eintreten.

Die Transformation "Typ konvertieren" erzeugt Ergebnisfelder vom Typ Zeichenkette. Dies entspricht auch dem tatsächlichem
Ergbnis dieser Funktion.

Die EmarSys-Verbindung hat keine ID zu angelegten Kontakten zurückgeliefert, wodurch dieser Datensatz fälschlich als 
"übersprungen" interpretiert wurde.

Die Sage b7 Verbindung wurde korrigiert. Leere Werte zu Feldern werden nicht mehr als leere Zeichenkette, sondern als NULL
übergeben.
Außerdem wurd die Verabreitung der Antwort zu einer neu angelegten Person oder Anschrift korrigiert.

