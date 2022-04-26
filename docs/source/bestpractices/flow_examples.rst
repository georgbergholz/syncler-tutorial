Beispiel für den Einsatz von Abläufen
=====================================

Hier ein paar Beispiele, wie mit Abläufen komplexere Anforderungen umgesetzt werden können.

Übertragung eines Beleges
-------------------------

Bevor ein Beleg übertragen werden kann, muss meistens auch ein Stammdatensatz bereits angelegt sein, welchem
der Beleg zugeordnet wird.
Übertragungsprozesse für den Beleg können so etwas prüfen und dann eine Fehlermeldung generieren.
Jetzt muss der Benutzer eigenverantwortlich diese Meldung interpretieren, die Stammdaten übertragen und 
kann erst dann den Beleg erfolgreich übertragen.

Diese einzelnen Schritte sind nicht nur umständlich, sondern führen auch zu Fehlern, falls der Benutzer
diesem nicht nachkommt.

Für dieses Szenario bietet sich ein Ablauf an, der sicherstellt, dass die Voraussetzungen gegeben sind.
Mit folgenden Schritten kann dieser Ablauf gestaltet werden.

Beginnen wir mit den einzelnen Prozessen.
Es wird ein oder mehrere Prozesse für die Stammdatenübertragung benötigt.
Diese können direkt mit Vorlagen oder auch manuell konfiguriert werden.
Natürlich können auch die Prozesses einer eingerichteten Synchronisation verwendet werden.
Ein weiterer Prozess realisiert die Belegübertragung. 
Auch dieser kann aus einer Vorlage oder der Synchronisation stammen.

Und ein weiterer Prozess übernimmt ausschließlich das Lesen der Quelldaten des Beleges.
Dieser ist üblicherweise nicht Teil einer Synchronisation und muss neu angelegt werden.
Dafür kann z.B. der Prozess "Universal Ablauf - Geschachtelte Daten lesen" verwendet werden.
Stellen Sie die Verbindung und das Objekt ein. Weitere Transformationen sind an dieser Stelle nicht unbedingt erforderlich.
Wichtig ist, dass Sie mit den generierten Daten in der Lage sind einen Filter für die Stammdaten zu formulieren.

Jetzt kann der Ablauf angelegt werden.
Als Verbindung und Objekt stellen wir die Quelldaten ein, damit der Prozess auch für Adhoc-Übertragungen
genutzt werden kann.
Der erste Schritt führt den Prozess "Lesen der Quelldaten" als manuellen Prozess aus.
Eine Adhoc-Anforderung wird hiermit dann ebenfalls die Daten abrufen.
Der zweite Schritt soll die Stammdaten übertragen. Wählen Sie den betroffenden Prozess aus.
Als Ausführungsart wählen Sie "Prozess für jeden Quelldatensatz aus Vorgänger und einem ausgewerteten Filter ausführen"
und stellen als Vorgänger den Prozess aus Schritt 1 ein.
Der Filter muss jetzt so formuliert werden, dass exakt die benötigten Daten erfasst werden.
Hier ein Beispiel zu Sage CRM:

.. code-block:: sql

    comp_companyid IN (SELECT oppo_primarycompanyid FROM Opportunity WHERE oppo_opportunityid = #quot_opportunityid#)

An dieser Stelle kann ein weiterer Prozess erforderlich sein. 
Bestimmt Prozess für die Stammdaten-Synchronisation prüfen automatisch ein Status-Kennzeichen, 
um nicht alle Daten in das ERP-System zu übertragen.
Für Sage CRM gilt dies zum Beispiel. Um dies zu umgehen brauchen wir einen weiteren Lese-Prozess "Universal Ablauf - Daten lesen",
der hier mit dem Filter ausgeführt wird. An diesem Prozess kann dieses Verhalten deaktiviert werden.
Diesem folgt dann erst der eigentliche Übertragungsprozess, der direkt die Daten des Vorgängers verwenden kann,
wodurch die Prüfung des Status-Kennzeichen nicht mehr stattfindet.

Der letzte Schritt führt dann die Belegübertragung aus und kann direkt die Quelldaten aus Schritt 1 verwenden.


Verarbeitung von Emails
-----------------------

In diesem Szenario wird ein Postfach kontinuierlich überwacht.
Eingehende Emails sollen ein Ticket im Zielsystem anlegen und die Email dazu abspeichern.
Außerdem sollen Emails auch bestehenden Tickets zugeordnet werden, sofern eine Übereinstimmung mittels einer
Referenz gefunden wird.
Die Umsetzung kann abhängig vom Zielsystem verschieden komplex ausfallen.
Manche Systeme können Email gesamt abspeichern und in anderen Systemen muss das Speichern der Anhänge separat erfolgen.
Dieses Beispiel beleuchtet den komplexeren Fall am Beispiel von Sage CRM.

Für die Umsetzung werden zuerst die zwei Verbindungen zu Email-Postfächern und Sage CRM benötigt.
Folgende Prozesse müssen eingerichtet werden.

:1. Emails abrufen:
    
    Dieser Prozess ist vom Typ "Universal Ablauf - Daten lesen" und verwendet die Email-Verbindung
    und das Objekt MimeMessage. Transformationen werden nicht benötigt.

:2. Email zu Ticket:

    Dieser Prozess ist vom Typ "Universal Sync Prozess für Email" und verwendet die Email-Verbindung.
    Als Ziel wird Sage CRM und cases eingestellt. Der Prozess verändert nichts am Postfach, damit ggf.
    eine Fehlerwiederholung möglich ist. 
    Per Transformation kann die Referenz aufbereitet und die Firma bzw. die Person ermittelt werden.
    In der Übereinstimmungsregel wird nach einem Ticket gesucht. Falls bereits per Email ein Ticket angelegt wurde,
    kann eine Datenabbildung vorhanden sein.
    Das besondere an diesem Prozess ist, dass das nicht zum Überspringen führt, sondern die Verabreitung
    fortgesetzt werden kann.
    Neue Email können also das Ticket auch aktualisieren, aber zur identischen Email wird kein neues
    Ticket angelegt, falls dort der Referenz-Ansatz nicht möglich ist.

:3. Email zu Kommunikation:

    Dieser Prozess ist vom Typ "Universal Sync Prozess für Email" und verwendet die Email-Verbindung.
    Als Ziel wird Sage CRM und communication eingestellt. Auch dieser Prozess verändert nichts am Postfach, 
    damit ggf. eine Fehlerwiederholung möglich ist.
    Wenn der Prozess die transformierten Daten von Prozess 2 verwendet, kann direkt Firma und Person
    im Unterobjekt comm_link zugeordnet werden. Sonst müsste dies nochmal neu ermittelt werden.
    Als Besonderheit wird hier die Transformation "Datenabbildung abfragen" verwendet.
    Zusammen mit der Uid der Email kann so die Ticket-ID ermittelt und der Kommunikation zugeordnet werden.

:4. Email Anhänge speichern:

    Als letzter Prozess wird das Speichern von Anlagen mit dem Typ "Email Anhänge nach Sage CRM Dokument"
    eingerichtet. Wie im Prozess 3 kann mit der Transformation "Datenabbildung abfragen" die Ticket-ID
    ermittelt werden. Dies ist auch für die Kommunikation möglich, womit die Datei mit Ticket und
    Kommunikation, sowie Firma und Person verknüpft werden kann.
    Als letzter Prozess in unserem Ablauf kann dieser nun das Postfach verändern und die Email löschen
    oder verschieben.
    In diesem Prozess muss der Dateiinhalt (FileContent) und Dateiname nicht zugeordnet werden. Dies wird 
    automatisch durch den Prozess durchgeführt.
    
Nun kommen wir zum Ablauf. Dieser nimmt die 4 Prozesse in dieser Reihenfolge auf.
Die Prozesse 2 bis 4 können die Quelldaten von Prozess 1 verwenden.
Falls Firma und Person mit eigenen Transformationen gesucht werden, kann das erst in Prozess 2 erfolgen,
da erst dort eine Zielverbindung definiert ist. In diesem Fall sollte Prozess 3 und 4 auf die transformierten Quelldaten
von Prozess 2 zugreifen.


    


