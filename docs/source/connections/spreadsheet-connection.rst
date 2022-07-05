Tabellenkalkulation
===================

Diese Verbindung ermöglich die Erstellung und Befüllung von Tabellen auf der Basis einer Vorlage.
Das Verfahren ist vergleichbar mit einem Seriendruck.

Das Resultat kann als Tabellenkalkulation oder PDF-Druck weiterverwendet werden.

Neben einzelnen Feldern können auch geschachtelte Listen, HTML und Bilder verarbeitet werden.

Für die Funktion stehen spezifische Prozesse zur Verfügung, die die Konfiguration und den Ablauf
unterstützen. Außerdem ist eine direkte Ausführung über die Syncler API möglich.


Funktionen
----------

:Schema ermitteln:

Die Verbindung erstellt nur ein Schema-Objekt "SpreadsheetFile" für die Konfiguration und das Resultat.
Damit ist auch eine individuelle Konfiguration je Datensatz möglich.
Außerdem enthält das Schema generische Nutzfelder, die bei der Ausführung zugewiesen und in der
Nachfolger-Bearbeitung ausgewertet werden können.
Die eigentlichen Daten werden dynamisch durch die Prozesse bereitgestellt.


:Lesen von Schema-basierten Daten:

Die Verbindung kann ausschließlich Datensätze aus dem Änderungsspeicher lesen.
Eine erfolgreiche Verarbeitung mit Nachfolgerprozess speichert das Resulat im Änderungsspeicher zwischen.
Der Nachfolger liest und verabeitet die Datensätze. Bei erfolgreicher Verarbeitung und ohne
weiteren Nachfolger werden die Daten aus dem Änderungsspeicher entfernt.


:Lesen von Abfrage-basierten Daten:

Diese Funktion wird nicht unterstützt.


:Schreiben von Daten:

Das Schreiben führt die eigentliche Funktion aus.
Die Vorlage wird dabei gelesen und mit dem bereitgestellten Daten gefüllt.
Das Resultat wird je nach Konfiguration gespeichert oder ausschließlich zurückgegeben.

:Schreiben von Bulk-Daten:

Diese Funktion wird nicht unterstützt.


Einstellungen
-------------

Folgende Einstellungen können bereitgestellt werden.

:FTP Quellverzeichnis:

Dies definiert das Quellverzeichnis für die Vorlagen, welche per FTP gelesen werden sollen.

:FTP Zielverzeichnis:

Dies definiert das Zielverzeichnis für die Resultat, welche per FTP gespeichert werden sollen.

:FTP Verzeichnis für Schriftarten:

Für den PDF-Druck kann hier ein optionales Verzeichnis für Schriftarten angegeben werden.
Es stehen bereits einige Standardschriftarten zur Verfügung bzw. werden On-premises die installierten
Schriftarten verwendet.
Falls der PDF-Druck nicht mit der in der Vorlage konfigurierten Schriftart erfolgt, muss diese
über dieses Verzeichnis bereitgestellt werden.

:Schriftarten löschen:

Nach erfolgreicher Ausführung kann hiermit das Löschen der lokalen Schriftartkopie veranlasst werden.

:FTP Server:

Serveradresse des FTPs.

:FTP Port:

Serverport des FTPs.

:FTP Benutzername:

Benutzername für den FTP-Zugriff.

:FTP Passwort:

Passwort für den FTP-Zugriff.

:SFTP verwenden:

Soll SFTP verwendet werden.

:Erweitertes Protokoll:

Optional können zusätzliche Protokolleinträge erzeugt werden, damit im Fehlerfall eine genauere
Analyse möglich ist.


Besonderheiten
--------------

Als Eingabeformat stehen die Dateitypen XLS, XLSX, CSV, HTML und ODS zur Verfügung.
Auf diese Vorlagen kann per lokalem PFad (nur On-premises), Base64-Daten, Vorlagendatenbank, URL 
oder FTP zugegriffen werden.

Als Ausgabeformat stehen die Dateitypen XLS, XLSX, CSV, HTML, Image, ODS, XPS und PDF zur Verfügung.
Das Resultat kann lokal (nur On-premises) und auf einem FTP abgelegt werden.
Außerdem kann das Resultat als Base64 direkt zurückgegeben oder im Änderungsspeicher abgelegt werden.

Nicht alle Funktionen stehen mit jedem Eingabe- oder Ausgabeformat zur Verfügung.

Seriendruck-Felder werden mit der #..#-Notation in der Vorlage definiert und in allen Tabellenblättern verarbeitet.

Wenn der Feldname den Präfix "Html:" hat, wird der Inhalt als HTML interpretiert und die Formatierungen übernommen.
Damit ist eine Daten-bezogene Formatierung des Resultats möglich.

Wenn der Feldname den Präfix "Picture:" hat, wird der Inhalt als Anweisung zum Lesen einer Grafikdatei
verwendet. Die Skalierung des Bildes im Dokument wird dabei durch die Dimension der verwendeten Zelle festgelegt.
Die Anweisung kann in Json angegeben werden. Wird kein gültiges Json vorgefunden, wird der Inhalt direkt als Url
zur Datei interpretiert. In Json werden die Eigenschaften "FileMethod" und "File" erwartet.
FileMethod kann dabei die Ausprägungen PATH, BASE64, URL und DATABASE (Vorlagendatenbank) haben.
File enthält die Daten zu dieser Methode. Die Formate JPG, BMP, GIF, PNG, TIFF und WMF werden unterstützt.

Die Verarbeitung von geschachtelten Listen erfordert die Feldern #RangeStart:..# und #RangeEnd:..# in der Vorlage.
Alle Zeilen zwischen diesen Positionen werden kopiert und für jeden Listeneintrag ausgefüllt.
Das Kopieren erfolgt dabei auf der Basis von kompletten Zeilen, wobei auch Formatierungen erhalten bleiben.
Die Start- und Endpositonsfelder werden geleert.

Sollte für die geschachtelte Liste eine Transformation definiert sein, bei der neue Felder erzeugt werden,
werden diese in das Listenelement kopiert, damit sie zur Verfügung stehen. Dies unterscheidet sich zur regulären
Verarbeitung von geschachtelten Listen.

Der PDF-Druck verwendet das in der Excel-Vorlage definiert Seitenlayout für das Resultat.
Außerdem erfolgt der Druck über alle Tabellenblätter.
