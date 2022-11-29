Release 4.4.1 - 22.09.2022
==========================

Änderungen
----------

Die Erzeugung eines Delta-JSON auf der Basis von geänderten Felder eines Objektes wurde angepasst.
Ungeänderte Pflichtfelder und Unterobjekte mit ungeänderten Pflichtfeldern werden nicht übersprungen,
sondern in das Resultat übernommen.
Abhängig vom Zielsystem verhindert das Fehlermeldungen durch fehlende Pflichtfelder.

Das Schema der Zoho Verbindung wurde u.a. für die Erstellung eines Delta-JSON angepasst.
Die Felder "type" und "participant" des Objektes "Participants" wurden als Pflichtfelder definiert.
Das Feld "id" des Objektes "Participants" wurde als ID-Feld definiert.
Das Feld "percentage" des Objektes "Linetax" wurde als Pflichtfeld definiert.
Der Feldtyp des Feldes "Remind_At" des Objektes "Events" wurde auf Datetime geändert,
damit eine automatische Formatierung ausgeführt werden kann.

Der neue Prozesstyp "SQL Abfrage nach Auswahllisten" kann interne Auswahllisten für Transformationen
auf der Basis von SQL-Abfragen erzeugen.

Bei der Erzeugung einer Terminserie in Zoho werden die Termine direkt über die $u_id abgefragt.
Die erzeugten Einträge im Änderungsspeicher werden um das Anfangsdatum ergänzt, damit die
Zuordnung von Terminvorkommen das Ziel nicht erneut in Zoho abfragen muss. 
Dies hatte zu wiederholten Abfragen bei historischen Serien geführt, die das API-Limit unnötig belasten.

Bei der Erzeugung einer Terminserie in Graph wird das Startdatum und der Benutzer am erzeugten
Eintrag im Änderungsspeicher hinterlegt. Damit kann das Vorkommen für die Zuordnung zum Quelldatensatz 
effizienter ermittelt werden.

Die Verarbeitung von JSON in der CAS Verbindung wurde intern zur Optimierung umgestellt.

Die Graph Verbindung wurde angepasst und erweitert.

* Das automatische Parsing von Datumswerten wurde deaktiviert. Dies hat in der Verarbeitung zu nicht ISO-konformen Datumsangaben und damit API-Fehlern geführt. Datumswerte werden jetzt als Zeichenketten verarbeitet und müssen ggf. manuell konvertiert werden (z.B. für Berechnungen).
* Per Verbindungsparameter kann eine bevorzugte Zeitzone eingestellt werden. Datumswerte werden bei Abfragen dann in dieser Zeitzone zurückgemeldet und müssen nicht extra umgerechnet werden. Ohne eine angegebene Zeitzone werden Datumswerte in UTC bereitgestellt.
* Das Verbindungsschema wurde um die Objekte "TodoTask" und "Contact" erweitert.
* Die Schemaobjekte werden um das Feld "isDeleted" (bool) ergänzt. Bei Delta-Abfragen wird dieses Feld gefüllt, damit gezielt gelöschte Datensätze in Prozessfiltern berücksichtigt werden können.
* Die Schemaobjekte "TodoTask" und "Contact" erhalten zusätzlich das Feld "user", damit der zugeordnete Benutzer per Feldzuordnung festgelegt werden kann.
* Die Abfrage von Vorkommen zu einer erzeugten Terminserie erfolgt nicht mehr über das Zeitfenster, sondern über Start- und Enddatum der Serie. Nur bei Serien ohne Enddatum wird das Ende des Zeitfensters verwendet.
* Bei Request-Fehlern wird die Url in die Fehlermeldung aufgenommen, da diese sonst nur als Debug-Nachricht ausgegeben wird.
* Fehlermeldungen zu ErrorItemNotFound, ResourceNotFound oder MailboxNotEnabledForRESTAPI erzeugen nur eine Warnung. Damit soll der Abbruch mit globalen Fehler unterbunden werden, wenn einzelne Benutzer nicht abgefragt werden können.

Die Zoho-Graph Vorlagen wurden überarbeitet, um den genannten Änderungen an der Graph Verbindung gerecht zu werden.
Dies optimiert die Prozesse, da Skript-Transformationen entfallen können.

Die Sage CRM Verbindung wurde angepasst und erweitert.

* Das Schema "comm_link" wird mit dem Feld "comm_organizer" angereichert, wenn Kommunikationen abgefragt werden. Damit können diese ggf. für die Synchronisation über die Graph Verbindung ausgefiltert werden.
* Wenn die Objekte "Quotes", "Orders", "Communication" und "ProjectOrders" gelöscht werden, werden auch die Positionsdatensätze gelöscht.
* Als gelöscht markierte Positionen werden bei der Verarbeitung nicht übersprungen, wenn sie keine Änderung enthalten.
* Die Abfrage nach geänderten UserContacts prüft automatisch auch die Tabellen "Person", "Address" und "Company" über die Sicht "vSearchListPerson" auf Änderungen.
* Der Upload wurde für die Version 2022 R2 erweitert. Es kann über das Feld "libr_filepath" ein Zielordner im Library-Verzeichnis definiert werden.
* Die Zeichenfolgen /* und */ in Where-Bedingungen werden ersetzt, damit die Abfragen durch das CRM nicht abgelehnt werden.

Die Syncler API enthält die neuen Endpunkte "GraphRefreshToken" und "DeleteGraphRefreshToken".
Diese können für die verschlüsselte Speicherung eines Benutzer-bezogenen Refresh-Tokens genutzt werden.
Da die Graph API für den Zugriff auf "TodoTask" nur delegierte und keine Anwendungsberechtigungen unterstützt, 
können so Benutzerzustimmungen für das Lesen und Schreiben von Aufgaben gespeichert und fortlaufend verwendet werden.
Die Implementierung des Zustimmungsprozesses ist abhängig vom Endsystem und steht in Sage CRM als neue 
Registerkarte in "Mein-CRM" zur Verfügung.
Der Zugriff auf "TodoTask" ist automatisch gegeben, wenn die Verbindung mit einer Benutzeranmeldung eingerichtet wird.
Allerdings beschränkt sich der Zugriff dann auf diesen Benutzer.

Die interne Verarbeitung von Datensatzsperren wurde angepasst, damit auch Zeichenketten als Änderungsdatum interpretiert werden können.

Es stehen Synchronisationsprozesse mit Delta-Funktion für die Kombination Sage CRM und Microsoft Graph API zur Verfügung.
Die unterstützen Objekte sind Termine, Aufgaben und Kontakte.
Für dieses Szenario wurden auch Vorlagen hinzugefügt.

Die Zoho-Graph Prozesse wurden angepasst.
Die Änderung einer Serie erzeugt im Zielsystem eine neue Serie und löscht den Vorgänger.
Der Parameter Monat wurde für Zoho-Serien mit dem Typ "Jährlich" nicht bereitgestellt.
Die Prozesse wurden um die Unterstützung von parallelen Datenabbildungen erweitert.
Damit können neue Prozesse aus Vorlagen die Datenabbildungen vorhandener Prozesse weiterverwenden.

Die Basis für Abfrageprozesse wurde erweitert.
Sobald Datenabbildungen verwendet werden und das Ziel nicht gefunden wird, wird die Abbildung als gelöscht markiert
und das Fehler-Rückschreiben ausgeführt, sowie der Datensatz übersprungen.

Die Antworteigenschaft "list" wird von der REST API Verbindung für das Resultat verwendet.

Korrekturen
-----------

Das Löschen von Verbindungen und Prozessen löscht auch zugeordnete Parameter aus der Datenbank.

In der Graph Verbindung hat eine Einzel-Abfrage durch einen Delta-Prozess zu einer fehlerhaften Abfrage geführt.

Im Syncler-Administrator konnte das Löschen von Feldzuordnungen zu Positionsdaten einen Fehler erzeugen.

Die Transformation "Dokument konvertieren" wurde angepasst. 
Bei einer Konvertierung in das Ausgabeformat "Text" wurden vertikale Tabulatoren erzeugt.
Dies hat zu internen Verarbeitungsfehlern geführt, da diese Zeichen in XML nicht zulässig sind.

Die CAS Bulk-Übertragung hat Verknüpfungen des ersten Datensatzes für alle Datensätze der aktuellen Übertragung genutzt.

Die Antwortabfrage zur Sage 100 Belegerzeugung hat mit der Version 9.0.x ungültige Header enthalten, die zu einem
Fehler geführt haben. Der Beleg wurde dennoch korrekt angelegt.

Das Laden von Wiederholungen, Nachfolgern und Fehlerwiederholungen durch die CAS Verbindung hat eine fehlerhafte Abfrage erzeugt.
