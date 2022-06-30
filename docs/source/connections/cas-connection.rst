CAS genesisWorld und SmartWe
============================

Diese beiden CRM-Systeme können durch ihre fast identische REST API mit einer Verbindung angesteuert werden.
Die geringfügigen Unterschiede werden durch die Verbindung behandelt, weshalb per Parameter festgelegt
werden muss, um welches System es sich handelt.

Diese Verbindung unterstützt die bidirektionale Synchronisation von Datentypen der REST API und kann Emails 
und Dokumente archivieren. Außerdem besteht die Möglichkeit Bulk-Importe auszuführen

Schema-basierte und Abfrage-basierte Datenzugriffe werden über die REST API implementiert.
Für Abfragen wird der spezifische SQL-Syntax von CAS verwendet, der zusätzliche Funktionen für Dossier, Verknüpfungen 
und Filter bereitstellt.

Es stehen spezifische Prozesse für die Synchronisation mit Sage b7, Microsoft Dynamics Business Central,
Sage 100, Sage X3 und Mailing-Anbietern inklusive Vorlagen zur Verfügung.
Weitere Systeme und Entitäten können über Universalprozesse angebunden werden.


Funktionen
----------

:Schema ermitteln:

Das Schema der Verbindung wird über die REST API ermittelt. Basis sind die verfügbaren Datenobjekte.
Zusätzlich wird das Schema noch für die direkte Abfrage von Benutzern und Verknüpfungen erweitert.

Berechtigungen und Verknüpfungen können zu jedem Datentyp festgelegt werden.

Das Schema für DOCUMENT und EMAILSTORE wird um das Feld FileContent erweitert. Base64 Daten, die 
hier zugewiesen werden, werden in CAS abgelegt bzw. archiviert.

Das Schema von APPOINTMENT, TODO und GWPHONECALL wird um die Listen LinkToAddress, LinkToGWOpportunity
bzw. Participants erweitert. Speziell Participants ist dabei eine geschachtelte Liste.
Diese Daten stehen auch beim Lesen zur Verfügung.

Das Schema für GWOPPORTUNITY und BSVOUCHER wird um eine geschachtelte Positionsliste erweitert, 
die in der Sortierung die Gruppen berücksichtigt.

Das Schema von GWDISTRIBUTION wird um eine geschachtelete Liste für ADDRESS-Verweise erweitert.


:Lesen von Schema-basierten Daten:

Mit Ausnahme von Einzeldatensätzen werden alle Abfragen für Schema-Objekte per query ausgeführt und ergänzt.
Für genesisWorld wird das Statement automatisch um TEAMFILTER(Objektname; CASLOGGEDINUSER, CASPUBLICRECORDS, 
CASEXTERNALACCESS) erweitert.
Bei der Verwendung von Abfrage-Prozessen muss dies manuell erfolgen, da das Ergebnis ansonsten eine
Vervielfälltigung der Daten sein kann.


:Lesen von Abfrage-basierten Daten:

Auch für diese Art des Lesens wird die query Funktion der REST API genutzt. Hierbei wird allerdings kein bekanntes
Schema-Objekt gefüllt, sondern das Resultat dynamisch generiert.
Eine Anreichung des Ergebnisses durch Berechtigungen, Verknüpfungen oder Listen ist deshalb
nicht möglich.


:Schreiben von Daten:

Das Schreiben von Daten erfolgt über die REST API, wobei die Verbindung selbstständig eine Etag ermittelt.
Auch das Löschen von Datensätzen wird unterstützt.
Direkte Verknüpfungen können ebenfalls geschrieben oder gelöscht werden.
Das Schreiben von Benutzern ist nicht möglich.
Berechtigungen, Verknüpfungen und Listen an Schema-Objekten können geschrieben werden.
Das Löschen von Berechtigungen oder Verknüpfungen an Schema-Objekten wird nicht unterstützt.


:Schreiben von Bulk-Daten:

Da diese Funktion nicht über die REST API möglich ist, sondern ausschließlich in der SOAP Schnittstelle
zur Verfügung steht, kommt hier ein besonderes Verfahren zum Einsatz.
Es steht eine CAS SOAP Bridge zur Verfügung, die per Veröffentlichungspaket in einen Windows Internet-
Informationsdienst eingebunden werden kann.
Die Verbindungsdaten zu dieser API werden in den Einstellungen festgelegt.
Der Bulk-Import wird in definierte Pakete unterteilt und an die API übergeben, welche diese dann
an CAS übermittelt. Dabei können individuelle Verknüpfungen geschrieben und Fehler behandelt werden.
Lediglich Berechtigungen können nur gesammelt vergeben werden, wobei einfach die Berechtigungen des
ersten Datensatzes für alle übernommen werden.
Damit das Anlegen von Datensätzen auch generierte IDs ermitteln und für Datenabbildungen verwenden kann,
muss ein zusätzliches GUID-Feld (Textfeld) angelegt und angegeben werden.
Hier wird automatisch eine generierte GUID für die Wiedererkennung des Datensätzes eingetragen.
Die CAS Zugangsdaten werden dynamisch verschlüsselt an die API übergeben.


Einstellungen
-------------

:URL REST API:

Die Url der REST API.
Für SmartWe ist dies https://api.smartwe.de/SmartWe/rest/v6.0

:Benutzername:

Dieser Wert gehört zu den Zugangsdaten.

:Passwort:

Dieser Wert gehört zu den Zugangsdaten.

:Datenbank:

Der Datenbank- bzw. Mandantenname

:SmartWe:

Ist das Zielsystem SmartWe.

:Bridge Url:

Optional die Url zur CAS SOAP Bridge.

:CAS SOAP Url:

Optional die SOAP Url.
Für SmartWe ist dies https://api.smartwe.de/SmartWe/services

:Bridge Timeout:

Optional das Timeout für Aufrufe der Bridge Url.
Sollte es bei der Bulk-Verarbeitung zu Timeout-Meldungen kommen, kann hier ein abweichender Wert
festgelegt werden.
Die Eingabe erfolgt in Millisekunden.

:Maximale Anzahl von Datensätzen je Aufruf:

Bulk-Import erfolgen in Paketen. Je nach Leistungsfähigkeit und Datenmenge können sich unterschiedliche
Beschränkungen ergeben. Werte zwischen 100 und 200 sind in der Praxis üblich.
Das Timeout hat auch Einfluss auf diesen Wert.

:Feldname Massen-Neuanlage:

Optional der Feldname für die Wiedererkennung von angelegten Datensätzen für alle Datentypen.
Ohne diesen Wert können neue IDs aus dem Bulk-Import nicht ermittelt und bereitgestellt werden.
Das Feld muss als Textfeld manuell angelegt werden.

:Abfrage von Berechtigungen deaktivieren:

Hiermit kann das Lesen von Berechtigungen deaktiviert werden.
Das Schreiben steht dennoch zur Verfügung und überschreibt.
Da das Lesen der Berechtigungen zusätzliche Abfragen erfordert, kann hiermit die Lesegeschwindigkeit
erhöht werden.

:Prüfung von Pflichtfeldern deaktivieren:

Hiermit werden keine Pflichtfelder im Schema definiert und im späteren Verlauf geprüft.
Dies ist nur in Ausnahmen erforderlich.


Besonderheiten
--------------

Das Schema der verfügbaren Datenobjekte wird automatisch um die Objekte Permission, LinkTo und LinkFrom erweitert.
Diese unsortierten Listen bieten die Möglichkeit Berechtigungen und Verknüpfungen zu setzen oder Berechtigungen auszulesen.
Da es sich hier um 1:n verknüpfte Informationen handelt, die unsortiert bereitgestellt werden, müssen beim Lesen alle
Gruppen berücksichtigt werden.
Beim Aktualisieren von Berechtigungen wird über die RIGHTOWNERGGUID nach vorhandenen Zuordnungen gesucht. 
Die Verknüpfungen werden durch einen separaten API Aufruf festgelegt.

Das Zuweisen einer leeren Guid für Link-Ziele überspringt die Anlage.

Wenn Datensätze ohne Berechtigungen angelegt werden, stehen diese in der Anwendung den Benutzern nicht zur Verfügung.
Die Berechtigung ACCESSRIGHT = 32768 und RIGHTOWNER = 00000000000000000000000000000000 ermöglicht den 
Vollzugriff für alle Benutzer und wird in den Vorlage als Standardwert verwendet.
Weitere Permission Level sind Lesen = 64, Bearbeiten = 2048 und Löschen = 8192.

Für die Archivierung von Emails kann das Objekt "EMAILSTORE" verwendet werden.
Dieses verfügt über ein Feld "FileContent". Wenn Sie dort eine Email im EML-Format als Base64 Zeichenkette zuweisen, 
wird die Email im CAS archiviert. Diese Daten lassen sich mit der Email Verbindung bereitstellen.
Die restlichen Felder können für zusätzliche Daten, wie z.B. Verknüpfungen verwendet werden.
Die Archivierung wird nur mit neuen Datensätzen ausgeführt. 
Sollte es sich um einen bekannten Datensatz handelt, wird die Archivierung übersprungen.

