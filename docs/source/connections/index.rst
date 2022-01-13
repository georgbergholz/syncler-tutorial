Verbindungen
============

Eine Verbindung stellt die Anbindung eines externen Systems oder Funktion bereit.
Sie speichert Zugangsdaten und Einstellungen und realisiert eine einheitliche Schnittstelle für andere Elemente des Synclers.
Neben klassischen System wie CRM oder ERP kann sich hinter einer Verbindung auch der Eingang für Daten, 
z.B. Push-Nachrichten oder Dateien
und der Ausgang von Daten, z.B. Serienbriefe verbergen.

Zu den Kernaufgaben zählt das Lesen von Daten, das Schreiben von Daten und das Ermitteln eines Datenschemas.
Beim Lesen von Daten können zwei Methoden unterschieden werden, die aber nicht jede Verbindung auch implementieren muss.
Daten können auf der Basis eines Schemas oder auf der Basis einer Abfrage gelesen werden.
Auch beim Speichern von Daten können zwei Methoden unterschieden werden, 
die ebenfalls nicht von jeder Verbindung bereitgestellt werden müssen.
Daten werden Schema-basiert einzeln oder als Bulk gespeichert.

Außerdem stellen manche Verbindungen zusätzliche Funktionen, wie z.B. eine Preisfindung bereit.

Durch das Speichern einer neuen Verbindung oder das Speichern einer bestehenden Verbindung mit aktivierter Checkbox 
"Schema aktualisieren" ruft der Syncler das Schema des Systems ab und speichert es in ihrer Syncler-Datenbank.
Dieses Datenschema ist die Arbeitsgrundlage für die Konfiguration von Schema-basierten Prozessen und 
wird für eine bessere Performance zwischengespeichert.

Sollten sich das Datenschema ändern, z.B. durch das Anlegen neuer Felder, müssen Sie diese Änderung über die Aktualisierung 
des Verbindungsschemas dem Syncler bekannt machen, damit Sie diese verwenden können.

In der Detailbeschreibung zu jeder Verbindung finden Sie Angaben zu den folgenden Grundfunktionen.

:Schema ermitteln:

    Wie stellt die Verbindung ein Datenschema bereit und was ist enthalten.

:Laden von Quelldaten:

    Wie kann die Verbindung Quelldaten für Prozesse ermitteln.
    Diese Abfragen sind Schema-basiert und werden für die Ausführung eines Prozesses mit der Verbindung als Quelle benötigt.

:Laden von Schema-basierten Daten:

    Wie können Daten auf der Basis eines Schemas abgefragt werden.

:Laden von Abfrage-basierten Daten:

    Wie können Daten auf der Basis einer Abfrage ermittelt werden.

:Schreiben von Daten:

    Wie werden einzelne Datensätze geschrieben.

:Schreiben von Bulk-Daten:

    Wie können Sammlungen von Daten geschrieben werden.


Die folgenden Verbindungen stehen im Syncler zur Verfügung.

.. toctree::
    :titlesonly:

    b7-connection
    bc-connection
    cas-connection
    cleverreach-connection
    csv-connection
    fano-connection
    hotfolder-connection
    idoc-connection
    infor-connection
    inxmail-connection
    mailchimp-connection
    mailmerge-connection
    odoo-connection
    push-connection
    rest-connection
    s100-connection
    s200-connection
    salesforce-connection
    scrm-connection
    sdk-connection
    sql-connection
    x3-connection
    zoho-connection
    emarsys-connection
    bridgeservice
