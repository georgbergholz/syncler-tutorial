Release 4.4.4 - 22.03.2023
==========================

Änderungen
----------

Die Sage b7-Verbindung

* Die Verbindung wurde grundlegend überarbeitet und auf die Bibliothek Azure.Messaging.ServiceBus migriert.

Der Syncler Administrator

* In den Bereichen Datenabbildung, Protokolle, Änderungsspeicher und Sicherungsspeicher steht eine neue Datensatz-Zusammenfassung zur Verfügung, welche Informationen trennt und Felder in Listenform ausgibt.
* Mit einem Doppelklick können Feldinhalte leicht entnommen werden.

Der Prozess "Sage CRM Aufgabe nach Microsoft Aufgabe".

* Ein geänderter Benutzer im CRM führt zum Löschen der Aufgabe im ursprünglichen Postfach und zum Neuanlegen im aktuellen Postfach. Damit kann eine neu zugewiesene Aufgabe synchronisiert werden.
* Dabei werden auch die Datenabbildungen gelöscht, damit die Aufgabe nicht im CRM gelöscht wird, falls der neue Benutzer nicht synchronisiert wird.

Die Zoho CRM-Verbindung

* Es werden Contact-Roles zwischen Abschlüssen und Kontakten unterstützt. Siehe :doc:`/bestpractices/zohocontactroles`

Der Universal-Löschprozess

* Es wurden Feldzuordnungen, Adhoc-Ausführungen und Filter freigegeben.

Die Universal-Prozesse

* Mit einem zusätzlichen Parameter kann festgelegt werden, ob die IDs in Datenabbildungen Groß- und Kleinschreibung unterscheiden müssen.

Der Prozess "SAP Beleg nach Salesforce Opportunity"

* Mit einer zusätzlichen Suche können Positionen für die Aktualisierung zugeordnet werden.
* Ohne eine Suchangabe erfolgt die Zuordnung weiterhin über die Reihenfolge der Positionen.

Die SQL-Brücke

* Die API der SQL-Brücke hat den neuen Endpunkt "Check", der die Verfügbarkeit der API prüfen kann.

Die Salesforce-Verbindung

* Das Speichern einer Verkaufschance unterstützt das kombinierte Schreiben von Opportunity und OpportunityLineItems.

Die Graph-Verbindung

* Mit einem Parameter können die Tage bis zur Aktualisierung des Zeitfensters eingestellt werden. Damit müssen nicht jeden Tag alle Termine des neuen Zeitfensters geprüft werden.
* Das Teilnehmer-Schema hat die Felder isExternalOrganizer und isCurrentUser erhalten. Beide werden gefüllt, wenn es sich um einen externen Organisator handelt und der Teilnehmer auch der aktuelle Benutzer der Abfrage ist.

Die Serienbrief-Verbindung

* Das Schema für die Serienbrieferzeugung wurde um "InsertDocument" erweitert. Über einen "InsertMarker" im Hauptdokument kann ein fremdes Dokument gezielt eingefügt werden.







Korrekturen
-----------

Die Sage b7-Verbindung

* Die Verarbeitung von geteilten Nachrichten prüft die ID des Datensatzes eines jeden Teils für die Zusammenführung. Bisher wurde nur die Reihenfolge verwendet, was bei wiederholtem Lesen von Nachrichten zu Fehlern führen konnte.
* Das Löschen von Nachrichten erfolgt bereits bei der Verarbeitung, damit das Lock-Timeout nicht überschritten wird. Dies war in der Cloud-Umgebung durch die eingeschränkte Parallelität möglich und hat zum wiederholten Lesen von Nachrichten geführt.
* Bei geteilten Nachrichten erfolgt das Löschen erst bei der Verarbeitung des letzten Teils.

Die Sage CRM-Verbindung

* Die Prüfung des Organisators einer Kommunikation und die Zwangsverknüpfung als Teilnehmer wurde auch bei Aufgaben angewendet. Dadurch könnten zusätzliche Kommunikationslinks für Aufgaben entstehen.

Die Graph-Verbindung

* Das Änderungsdatum des Serienmasters wurde bei der Delta-Verarbeitung noch an die Vorkommen übergeben. Das führte durch die neue Serienverarbeitung zu unnötigen Änderungserkennungen und Konfliktwarnungen.
* Der Vergleich zwischen Organisator und aktuellem Benutzer war case-sensitiv. Das konnte beim Schreiben von Terminen zu einem Fehler führen, falls sich die Schreibweise zwischen den Systemen unterschieden hat.
* Beim Schreiben einer Aufgabe wurde das Fehlen des Refresh-Tokens als Fehler interpretiert. Jetzt wird eine Warnung und Überspringen ausgelöst.

Die InxMail-Verbindung

* Das Abrufen eines gelöschten Datensatzes führt zu einen 404-Fehler, der als Fehler behandelt und nicht als gelöschtes Ziel interpretiert wurde.

Die Vorlagen für Prozesse ausgehend von Microsoft Graph

* Die Vorlagen haben eine Transformation "Dokument konvertieren" für die Umwandlung von HTML zu Text verwendet. Falls der Termin oder die Aufgabe aber bereits reinen Text enthalten hat, wurden dadurch Zeilenumbrüche entfernt.
* Jetzt wird die Transformation "Html zu Text" verwendet, bei der Zeilenumbrüche erhalten bleiben.

Die CAS-Verbindung

* Die bisherige Abfrage nach Verknüpfungen hat deaktivierte Adressen nicht berücksichtigt.

Interne Abfragen zu Datenabbildungen mit externen IDs verwenden einen Unicode-Präfix, da sonst Datenabbildung unter Umständen nicht gefunden werden.

Das Zurückschreiben in Prozessen wurde angepasst, damit nur tatsächliche Änderungen erkannt und übertragen werden.

Der Prozess "Microsoft Graph Ereignis nach Zoho CRM Meeting"

* Wenn die Funktion "Alle zukünftigen Vorkommen aktualisieren" im Zoho genutzt wird, ändert sich die u_id bei diesen Datensätzen. Das ist vergleichbar mit einem Splitting der Serie.
* Außerdem ist das Serienschema der neuen Serie mit der alten vermischt und damit ungültig.
* Bei der Neuanlage einer Serie wurden so nicht alle Vorkommen entfernt und es kam zu Dubletten.
* Das neue Verfahren löscht die Zielvorkommen über die Datenabbildungen.

Der Prozess "Zoho CRM Meeting nach Microsoft Graph Ereignis"

* Wenn die Funktion "Alle zukünftigen Vorkommen aktualisieren" im Zoho genutzt wird, ändert sich die u_id bei diesen Datensätzen. Das ist vergleichbar mit einem Splitting der Serie.
* Da das Serienschema der einzelnen Teile aber fehlerhaft ist, werden nicht alle Vorkommen korrekt angelegt.
* Die Ermittlung des Anfangs und Ende der Serie erfolgt deshalb über das Maximum und Minimum aus den Vorkommen.

In den Bulk und CSV-Prozessen kam es zu einem Konvertierungsfehler bei der Verwendung von Datensatzversionsnummern.

Das OAuth2-Anmeldeverfahren fordert zum Login statt zur Account-Auswahl auf. Damit kann ein Login auch gewechselt werden.

Das Oauth2-Anmeldverfahren im Syncler Administrator gibt ggf. eine Fehlerbeschreibung aus.