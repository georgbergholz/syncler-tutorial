Die Salesforce Verbindung
=========================


Funktionen
---------

:Schema ermitteln:

:Laden von Quelldaten:

:Laden von Schema-basierten Daten:

:Laden von Abfrage-basierten Daten:

:Schreiben von Daten:

:Schreiben von Bulk-Daten:


Einstellungen
------------

:Webservice Benutzername: 
    
    Der Benutzername der für die Synchronisation verwendet werden soll. 
    Es ist darauf zu achten, dass der Benutzer über die entsprechenden Berechtigungen verfügt, 
    die für die Synchronisation erforderlich sind.

:Webservice Passwort: 
    
    Passwort des o.g. Benutzers

:Sicherheitstoken: 
    
    Sicherheitstoken des o.g. Benutzers. 
    Das Sicherheitstoken kann über die Benutzereinstellungen in Salesforce mit der Funktion 
    "Mein Sicherheitstoken zurücksetzen" generiert bzw. geändert werden. 
    Das Sicherheitstoken ändert sich automatisch bei jeder Passwortänderung. 
    Es ist empfehlenswert, den Benutzer, der für die Synchronisation verwendet wird, so einzustellen, 
    dass das Passwort nicht abläuft (z.B. über einen Berechtigungssatz)

:Login Server Url: 
    
    Als Standard wird hier die URL für Salesforce Produktivumgebungen verwendet, 
    z.B. https://login.salesforce.com/services/Soap/u/46.0. 
    Soll eine Sandbox angesprochen werden, ist die URL auf https://test.salesforce.com/services/Soap/u/46.0 zu ändern. 
    Ebenso können hier custom domains eingetragen werden.

:Dublettenwarnungen ignorieren: 

    Erkennt Salesforce eine Dublette bei der Anlage, dann wird die Anlage mit einer Warnung abgebrochen 
    und der Datensatz nicht synchronisiert. In den meisten Synchronisierungsszenarien ist 
    dies jedoch nicht wünschenswert und die Warnungen können mit der entsprechenden 
    Einstellung ignoriert werden. Die Dublettenregel in Salesforce muss auf "warnen" und 
    nicht auf "blockieren" gestellt sein.

