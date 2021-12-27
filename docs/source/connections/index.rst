Verbindungen
----

Eine Verbindung stellt die Anbindung eines externen Systems oder Funktion bereit.
Sie speichert Zugangsdaten und Einstellungen und realisiert eine einheitliche Schnittstelle f�r andere Elemente des Synclers.
Neben klassischen System wie CRM oder ERP kann sich hinter einer Verbindung auch der Eingang f�r Daten, z.B. Push-Nachrichten oder Dateien
und der Ausgang von Daten, z.B. Serienbriefe verbergen.

Zu den Kernaufgaben z�hlt das Lesen von Daten, das Schreiben von Daten und das Ermitteln eines Datenschemas.
Beim Lesen von Daten k�nnen zwei Methoden unterschieden werden, die aber nicht jede Verbindung auch implementieren muss.
Daten k�nnen auf der Basis eines Schemas oder auf der Basis einer Abfrage gelesen werden.
Auch beim Speichern von Daten k�nnen zwei Methoden unterschieden werden, die ebenfalls nicht von jeder Verbindung bereitgestellt werden m�ssen.
Daten werden Schema-basiert einzeln oder als Bulk gespeichert.

Au�erdem stellen manche Verbindungen zus�tzliche Funktionen, wie z.B. eine Preisfindung bereit.
Durch das Speichern einer neuen Verbindung oder das Speichern einer bestehenden Verbindung mit aktivierter Checkbox "Schema aktualisieren" ruft der Syncler das Schema des Systems ab und speichert es in ihrer Syncler-Datenbank.
Dieses Datenschema ist die Arbeitsgrundlage f�r die Konfiguration von Schema-basierten Prozessen und wird aus Performance-Gr�nden zwischengespeichert.
Sollten Sie das Datenschema �ndern, z.B. durch das Anlegen neuer Felder, m�ssen Sie diese �nderung �ber die Aktualisierung des Verbindungsschemas dem Syncler bekannt machen, damit Sie diese verwenden k�nnen.

.. toctree::

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