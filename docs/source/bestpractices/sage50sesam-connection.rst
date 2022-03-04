Sage50 Schweiz Einrichtung
==========================

Es wird der eigens entwickelte REST-WebService für die Sage50 Schweiz angebunden. Dazu muss das WebDeploy installiert werden (Sage50SesamBridge.deploy.cmd /Y)
Einrichtung der Verbindungseigenschaften im Admin-Tool Sage50SesamBridgeAdmin.exe
Eigenschaften "Benutzername für Web-Service Zugriff" und "Passwort für Web-Service Zugriff" dienen der Authentifizierung an der Bridge und müssen als Basic-Authentifizierung mitgegeben werden
Sage50Mandant muss in jedem Geschäftsjahr mit weitergezogen werden

.. image:: /images/Sage50SesamBridgeAdmin.png
  :width: 400
  :alt: Beispiel Einrichtung Sage50SesamBridgeAdmin

Zertifikat für 443 im IIS hinzufügen (Self-Signed reicht)
32-Bit Anwendungen im App-Pool aktivieren (DefaultAppPool -> Adcanced Settings -> Enable 32-Bit Applications)

Wichtig: Für die Vorlagen muss im ZOHO ein Feld Sprache an der Person existieren sowie die Felder sis_refid1, sis_status1
