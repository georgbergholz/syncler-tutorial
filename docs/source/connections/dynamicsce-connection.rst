Microsoft Dynamics 365 Customer Engagement
==========================================

Microsoft Dynamics 365 Customer Engagement ist Enterprise CRM-System mit verschiedenen Modulen.

Diese Verbindung unterstützt die bidirektionale Synchronisation ausgewählter Entitäten mittels Web API.
Außerdem können beliebig lesende Abfragen über die Web API ausgeführt werden.
Die Verbindung realisiert die Anmeldung an der Web API mit OAuth 2.0.

Für die Einrichtung der Anmeldung ist eine registrierte Anwendung bei Microsoft erforderlich.

Registrieren Sie die Anwendung über das Registrierungsportal https://go.microsoft.com/fwlink/?linkid=2083908.
Melden Sie sich mit Ihrem Microsoft Konto an und rufen Sie die Funktion "Neue Registrierung" auf.
Vergeben Sie einen Anwendungsnamen und klicken Sie auf Registrieren.

Danach wird Ihnen die Übersicht zur Registrierung angezeigt.
Für die Verbindung benötigen Sie die Anwendungs-ID (Client) und die Verzeichnis-ID (Mandant).
Übernehmen Sie die Angaben in die gleichnamigen Felder.

Konfigurieren Sie als nächstes die API-Berechtigungen.
Fügen Sie die Berechtigung "Dynamics CRM - user_impersonation" zur App hinzu.

Nun legen Sie noch eine Umleitungs-URI fest.
Für On-premises Installation oder die Konfiguration mit dem Syncler Administrator können Sie eine beliebige URL angeben.
Zum Beispiel: https://localhost/myapp

Tragen Sie die URL in das Feld "Redirect URI" ein.
Als nächstes müssen Sie den Web-API-Endpunkt ermitteln.
Melden Sie sich dazu in Dynamics 365 an und rufen Sie die Einstellungen auf.
Wechseln Sie zu Anpassungen und rufen Sie die Entwicklerressourcen auf.
Unter Instanz-Web-API finden Sie die spezifische URL für Ihre Instanz.
Kopieren Sie den Wert in das Feld "Web-API-Endpunkt" und das Feld "Scopes".
Im Feld "Scopes" ergänzen Sie am Ende der URL noch "/.default".

Als nächstes können Sie die OAuth 2.0 Anmeldung durchführen.
Rufen Sie die Seite an der Verbindung dafür auf und starten Sie den Anmeldeprozess.
Als nächstes müssen Sie die Microsoft Anmeldung ausführen und der App den Zugriff gestatten.
Mit dem Speichern der Verbindung wird ein Langzeit-Token ermittelt und gespeichert.
Dieser wird bei Verwendung der Verbindung für die Anmeldung verwendet und aktualisiert.


Funktionen
----------

:Schema ermitteln:

Das Schema der Verbindung wird über die Web API ermittelt.
Dafür wird der Endpunkt "EntityDefinitions" verwendet.
Die Änderungsinformation zur Entität wird über den Feldnamen "modifiedon" identifiziert.


:Lesen von Schema-basierten Daten:
 
Das Lesen von Datensätzen erfolgt über die Web-API.
Zusätzlich können über den Prozess noch weitere Filter im OData-Syntax definiert werden.
Die Zugriff erfolgen mit Universalprozessen.


:Lesen von Abfrage-basierten Daten:

Das Lesen von Abfragen erfolgt ebenfalls über die Web-API.
Dabei wird automatisch der Web-API-Endpunkt verwendet.
Im Prozess definieren Sie lediglich den Teil der Url nach dem Endpunkt.
Dabei verwenden Sie kein führenden Schrägstrich.


:Schreiben von Daten:

