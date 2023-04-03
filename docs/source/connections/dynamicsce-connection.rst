Microsoft Dynamics 365 Customer Engagement
==========================================

Microsoft Dynamics 365 Customer Engagement ist Enterprise CRM-System mit verschiedenen Modulen.

Diese Verbindung unterstützt die bidirektionale Synchronisation ausgewählter Entitäten mittels Web-API.
Außerdem können beliebig lesende Abfragen über die Web-API ausgeführt werden.
Die Verbindung realisiert die Anmeldung an der Web-API mit OAuth 2.0.

Für die Einrichtung der Anmeldung ist eine registrierte Anwendung bei Microsoft erforderlich.

Registrieren Sie die Anwendung über das Registrierungsportal https://go.microsoft.com/fwlink/?linkid=2083908.
Melden Sie sich mit Ihrem Microsoft Konto an und rufen Sie die Funktion "Neue Registrierung" auf.
Vergeben Sie einen Anwendungsnamen und klicken Sie auf Registrieren.

Danach wird Ihnen die Übersicht zur Registrierung angezeigt.
Für die Verbindung benötigen Sie die Anwendungs-ID (Client) und die Verzeichnis-ID (Mandant).
Übernehmen Sie die Angaben in die gleichnamigen Felder.

Konfigurieren Sie als nächstes die API-Berechtigungen.
Fügen Sie die Berechtigung "Dynamics CRM - user_impersonation" zur App hinzu.

Sollten Sie die Client-Anmeldeinformationen nutzen wollen, müssen Sie einen Geheimschlüssel anlegen und übernehmen.
In diesem Fall muss "Client-Anmeldeinformationen verwenden" auf "Ja" gestellt werden.
Eine Umleitungs-URI und die OAuth 2.0 Anmeldung entfallen hier.

Ohne Client-Anmeldeinformationen legen Sie nun noch eine Umleitungs-URI fest.
Für On-premises Installation oder die Konfiguration mit dem Syncler Administrator können Sie eine beliebige URL angeben.

Zum Beispiel: https://localhost/myapp

Tragen Sie die URL in das Feld "Redirect URI" ein.

Als nächstes müssen Sie den Web-API-Endpunkt ermitteln.
Melden Sie sich dazu in Dynamics 365 an und rufen Sie die Einstellungen auf.
Wechseln Sie zu Anpassungen und rufen Sie die Entwicklerressourcen auf.
Unter Instanz-Web-API finden Sie die spezifische URL für Ihre Instanz.
Kopieren Sie den Wert in das Feld "Web-API-Endpunkt" und das Feld "Scopes".
Im Feld "Scopes" ergänzen Sie am Ende der URL noch "/.default".

Ohne Client-Anmeldeinformationen können Sie jetzt die OAuth 2.0 Anmeldung durchführen.
Rufen Sie die Seite an der Verbindung dafür auf und starten Sie den Anmeldeprozess.
Als nächstes müssen Sie die Microsoft Anmeldung ausführen und der App den Zugriff gestatten.
Mit dem Speichern der Verbindung wird ein Langzeit-Token ermittelt und gespeichert.
Dieser wird bei Verwendung der Verbindung für die Anmeldung genutzt und aktualisiert.


Funktionen
----------

:Schema ermitteln:

Das Schema der Verbindung wird über die Web-API ermittelt.
Dafür wird der Endpunkt "EntityDefinitions" verwendet.
Die Änderungsinformation zur Entität wird über den Feldnamen "modifiedon" identifiziert.


:Lesen von Schema-basierten Daten:
 
Das Lesen von Datensätzen erfolgt über die Web-API.
Zusätzlich können über den Prozess noch weitere Filter im OData-Syntax definiert werden.
Die Zugriff erfolgen in der Regel mit Universalprozessen.
Die Besonderheiten von Lookup-Feldern werden durch die Verbindung behandelt.
Eine Beschreibung dazu finden Sie in den Besonderheiten.


:Lesen von Abfrage-basierten Daten:

Das Lesen von Abfragen erfolgt ebenfalls über die Web-API.
Dabei wird automatisch der Web-API-Endpunkt verwendet.
Im Prozess definieren Sie lediglich den Teil der URL nach dem Endpunkt.
Dabei verwenden Sie kein führenden Schrägstrich.


:Schreiben von Daten:

Das Schreiben von Datensätzen erfolgt über die Web-API.
Dabei werden Anforderungen an die Übergabe von Lookup-Felder durch die Verbindung behandelt.
Eine Beschreibung dazu finden Sie in den Besonderheiten.
Das Löschen von Datensätzen wird unterstützt.


Einstellungen
-------------

Folgende Einstellungen können bereitgestellt werden.

:Verzeichnis-ID (Mandant):

Diese ID definiert das Unternehmen und kann bei der Registrierung der Anwendung ausgelesen werden,

:Anwendungs-ID (Client):
    
Die Anwendungs-ID der registrierten Anwendung.

:Client-Geheimschlüssel:

Ein geheimer Schlüssel der registrierten Anwendung. Dieser wird für das Client-Anmeldeverfahren benötigt.

:Redirect URI:

Für die Authentifizierung mit OAuth 2.0 ohne Client-Anmeldeinformationen muss eine Weiterleitungs-URI konfiguriert werden.
Bei der Freigabe über den Syncler Administrator kann eine beliebige URI angegeben werden.
Für die Freigabe über das Web-Frontend ist folgender Wert notwendig.
Die Weiterleitungs-URI muss bei der registrierten Anwendung festgelegt werden.

:Scopes:

Diese Berechtigungen werden bei einer Benutzerzustimmung angefordert.
Kopieren Sie den Wert aus dem Feld "Web-API-Endpunkt" und ergänzen Sie am Ende der URL noch "/.default".
Der offline_access wird automatisch ergänzt.

:Web-API-Endpunkt:

Diese URL ist die Basis für alle lesenden und schreibenden Zugriffe auf die Web-API.
Sie ist spezifisch für Ihre Instanz und kann den Entwicklerressourcen entnommen werden.

:Client-Anmeldeinformationen verwenden:

Mit "Ja" erfolgt die Anmeldung mit Client-ID und dem Geheimschlüssel. Dieses Verfahren setzt einen Anwendungsbenutzer voraus.
Diesen können Sie im PowerApps Admin Center anlegen. Er muss der registrierten App zugeordnet sein und über ausreichende Berechtigungen für die Synchronisation verfügen.

:Auswahllisten abrufen und speichern:

Die Aktualisierung des Schemas kann ebenfalls alle Optionssätze (Auswahlen) abrufen und intern speichern.
Ein Optionssatz ist eine Liste von Wert-Text-Kombinationen, die für ein Auswahlfeld verwendet werden.
Gespeicherte Auswahllisten können in der Transformation "Auswahllisten abbilden" verwendet werden.

Siehe :doc:`/processes/converting/picklist`

Optionswerte werden in Dynamics 365 CE numerisch gespeichert und sind damit nicht lesbar.
Mit den Auswahllisten und der Transformation können Sie eine lesbare Variante erzeugen.
Das Abfragen der Auswahllisten benötigt zusätzliche Zeit bei der Aktualisierung.


Besonderheiten
--------------

Lookup-Felder wie Suche oder Kunde unterscheiden sich in den Lese- und Schreibanforderungen zu anderen Feldern.
Die Anforderungen werden durch die Verbindung weitestgehend kompensiert, damit in der Prozesskonfiguration einheitlich gearbeitet werden kann.

Werte werden beim Lesen durch die Web-API in einem Feld "_entityid_value" bereitgestellt. Die Verbindung übernimmt diesen Wert in das eigentlich Feld.
Dies ist nur beim Schema-basierten Lesen möglich.
Im Abfrage-basierten Lesen werden alle Daten des Resultats direkt übergeben. In diesem Fall steht der Wert nicht unter der eigentlichen Feldbezeichnung zur Verfügung.
Wenn nach Werten in diesen Feldern gefiltert werden soll, muss die Variante "_entityid_value" verwendet werden.


Wenn ein Feld ein oder mehrere Lookup-Ziele hat, werden diese in der Feldbeschreibung im Schema dargestellt.
Einfache Ziele werden durch die Verbindung automatisch behandelt, solange es sich um eine bekannte Zielentität handelt.
Bei Zielen, die nicht in den verfügbaren Schemaobjekte vorhanden sind, muss die Wertübergabe anders erfolgen.

Beispiel Währung:

Die Entität "transactioncurrency" ist bekannt und einem Feld "transactioncurrencyid" kann direkt der ID-Wert zugewiesen werden.

Beispiel mit unbekannten Ziel:

Damit die Wertübergabe an die Web-API möglich ist, muss der Wert in Feldnotation angegeben werden.
Für die Bezeichnung muss der CollectionName der Entität verwendet werden.

.. code-block:: none

    accounts|:|83883308-7ad5-ea11-a813-000d3a33f3b4|;|

Die Verbindung erzeugt in beiden Fällen daraus die benötigte Darstellung.

.. code-block:: none

    Feld@odata.bind : CollectionName(83883308-7ad5-ea11-a813-000d3a33f3b4)


Wenn mehrere Ziele möglich sind, z.B. beim Feldtyp Kunde, muss die Wertübergabe generell in Feldnotation erfolgen.
Die Bezeichnung definiert dabei das gewünschte Ziel und der CollectionName wird über das Schemaobjekt ermittelt.

Beispiel Kunde für Kontakte:

.. code-block:: none

    account|:|83883308-7ad5-ea11-a813-000d3a33f3b4|;|

Die Verbindung erzeugt in beiden Fällen daraus die benötigte Darstellung.

.. code-block:: none

    Feld_account@odata.bind : accounts(83883308-7ad5-ea11-a813-000d3a33f3b4)
