Release 4.3.5 - 06.01.2022
==========================

Änderungen
----------

Die Datendienste für CAS und Sage CRM zu Sage 100 wurden in eine universelle Form überführt.
Damit stehen nur noch 3 Datendienstplugins zur Verfügung, die alle bisherigen Anwendungsfälle durch Konfiguration abdecken.

Alle Abfrageplugins wurden vereinheitlicht. 
Die Unterscheidung findet nur noch auf der Ebene des Quellsystems statt, da dies ausschlaggebend für die Funktionsweise ist.
Nur für Sage CRM gibt es noch eine Ausnahme, da hier für Stammdaten zusätzliche Nacharbeiten enthalten sind.

Die Suche nach vorhandenen Datenabbildungen in anderen Prozessen wird über die laufende Nummer des Mandanten eingeschränkt.
Damit ist eine gezielte Anlage von Dubletten mit den selben Verbindungen möglich.

Bei der Subscription eines Empfängers zu einer Inxmail-Liste wird automatisch die Tracking-Permission vergeben.

Die REST-API Verbindung unterstützt alle Lade-Methoden, womit sie in den Universalprozessen verwendet werden kann.
Dafür wurden zwei weitere Lese-Urls, für alle Datensätze und für Änderungen von Datensätzen eingeführt.
Außerdem kann das Lesen seitenweise erfolgen, wofür zwei weitere Parameter eingeführt wurden.
Damit die Änderungsabfrage kontinuierlich auf der Datenbasis erfolgen kann, wurde die Schema-Angabe erweitert. 
Per UpdatedInfo kann ein Feld für die Änderungsinformation definiert werden. 
Dies muss entweder ein Datums- oder ein Integer-Feld sein.

Im CSV-Export kann ein zusätzlicher Datei-Kopf definiert werden.
Die CSV-Export-Prozesse haben ein neues mehrzeiliges Feld "Datei Kopfdaten". 
Der Inhalt wird den eigentlichen CSV-Daten vorangestellt und mit einem Zeilenumbruch abgeschlossen.

Die Sage CRM Verbindung kann Angebote und Aufträge mit Positionen speichern.
Damit können diese Objekte im Universalprozess für geschachtelte Daten eingesetzt werden.

Ein neuer Prozess für CAS Firma nach Business Central Kunde ermöglich diese Synchronisation inklusive Neuanlage, bei der der Kunde mit dem vorhanden Kontakt verknüpft wird.

Die Transformation führt eine Datensatz-spezifische Fehlerbehandlung aus.
Fehler brechen nicht mehr die gesamte Transformation ab, sondern führen die Fehlerbehandlung für den auslösenden Datensatz aus.

Die Serienbrief Verbindung hat einen neuen Parameter im Ausführungsschema.
Mit "ParseInputColumnType" wird der Inhalt nach seinem definierten Datentyp übersetzt.
Aus "" wird dann 0 für ein Zahlenfeld.
Aber aus "312.23 Euro" wird 0, wenn der Typ eine Zahl ist.
Der Standardwert ist "deaktiviert".

Die Salesforce Verbindung definiert ein Standard-Belegobjekt, welches über den Universalprozess synchronisiert werden kann.

Die Sage 100 Verbindung unterstützt abw. Rechnungsempfänger (VK) bzw. Rechnungsersteller (EK).
Die zugehörigen Adressdaten "A2" können ebenso übergeben werden.
Für die Lieferanschrift wird der Ansprechpartner unterstützt.

Die CAS Verbindung kann eine neue SOAP-Bridge ansprechen.
Diese wird über ein Paket im IIS eingefügt und braucht keine zusätzliche Konfiguration.
Über diese Bridge kann ein Bulk-Import in CAS durchgeführt werden.
Dazu stehen Prozesse auf der Basis von CAS, Sage b7, CSV und SQL zur Verfügung.

Abfrageplugins haben einen neuen Parameter "Seitenverarbeitung".
Mit diesem Parameter wird eine Seitenverarbeitung für die Quelldaten gestartet.
Die Daten werden komplett gelesen und dann in 1000-Schritten transformiert, verarbeitet und gespeichert.

Der neue Prozessparamter "Initialsync für Konfigurationsänderungen" ermöglicht eine einzelne gezielt Komplettverarbeitung im Fall einer geänderten Konfiguration, z.B. neue Feldabbildungen.
Der bisherige Initialsync-Parameter hatte den Fokus auf verpassten Änderungen, wodurch unveränderte Datensätze auf der Basis der Datenabbildung nicht verarbeitet wurden.

Die Parameter wurden umstrukturiert, damit eine logische und ablauforientierte Übersicht entsteht.

Der Hotfolder-Prozess ermöglicht ein Upload für Sage CRM.
Dafür wird die SData-Schnittstelle verwendet. Die zugehörige Url muss in der Verbindung eingestellt werden.

Die neue Eigenschaft "Kategorie" an Prozessen und Datendiensten ermöglicht eine individuelle Strukturierung in der Administration (aktuell nur On-Premise).

Ein globaler Fehler hat bisher immer die Fehlerbehandlung mit einer kompletten Wiederholung übersteuert.
Dies wird jetzt nur noch ausgeführt, wenn die Fehlerbehandlung nicht auf "Ignorieren" eingestellt ist.



Korrekturen
-----------

Die CSV-Prozesse haben keine Datensätze im Änderungsspeicher für Nachfolgeprozesse angelegt.
Damit war keine universelle Prozesskette möglich.

Die interne XML-Verarbeitung verwendet jetzt einen Textreader.
Damit werden Zeilenumbrüche CRLF nicht mehr auf LF reduziert.
Dies war z.B. in Prozessparametern der Fall.

Die Beleg-Ressource in der Sage 100 Verbindung definiert eine Änderungsinformation im Datenschema.
Damit kann dieses Objekt kontinuierlich in einer Änderungssynchronisation verwendet werden.

In Abfrageplugins war die Erzeugung von Datenabbildungen mit Zielen ohne ID-Rückgabe möglich, wodurch eine Datenabbildung mit leerem Ziel erzeugt wurde.
Das konnte beim Nachladen des Zieles in einem späteren Lauf zum Fehler führen.
Jetzt prüft der Prozess und springt raus bzw. führt die Übereinstimmungsregel erneut aus, damit ein vorher gespeicherter Schlüssel gesucht werden kann.
Den leeren Wert kann auch der Komplementärprozess füllen.

Die Adresse-Kontokorrentversion in der Sage 100 Verbindung wurde nicht in der Änderungsinformation beachtet.
Wenn die Adresse über das Kontokorrent First aktiviert wurde, wird die maximale Version für die Adresse verwendet.
Bisher wurde das nur im Parameter gespeichert, aber nicht in UpdatedInfoColumn.
Dadurch konnte ein Universalprozess eine alte Version erhalten.

Das Leeren von Datumsfeldern hat in den Verbindungen Sage b7, CAS, Mailchimp, Sage 100, REST-API, Infor CRM, Odoo und Zoho zu einem Konvertierungsfehler geführt.


