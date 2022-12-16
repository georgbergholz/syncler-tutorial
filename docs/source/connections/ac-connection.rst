ActiveCampaign
==============

ActiveCampaign ist eine Cloud-Softwareplattform für die Automatisierung von E-Marketing-Kampagnen.
Diese Verbindung dient in erster Linie dem Austausch von Stammdaten und unterstützt dabei die
benutzerdefinierten Felder.

Für die Einrichtung müssen Sie die API URL und den API Key über das Web-Portal ermitteln.
Beides finden Sie unter "Settings" / "Developer".
Achten Sie darauf, dass der API Key mit ausreichenden Rechten abgerufen wird.
Ansonsten besteht die Möglichkeit, dass Daten nicht gelesen oder geschrieben werden können.

Funktionen
----------

:Schema ermitteln:

Das Schema wird fest vorgegeben und um die benutzerdefinierten Felder für Account und Contact erweitert.


:Lesen von Schema-basierten Daten:

Das Lesen von Daten erfolgt über die REST API.
Eine Abfrage von Änderungen mittels eines Grenzwertes ist möglich.
Bei der Abfrage von Accounts kann dieser Grenzwert aber nicht der Abfrage übergeben werden, sondern wird
nachträglich als Filter eingesetzt. Bei sehr vielen Accounts kann so ein hoher Datenverkehr entstehen.
In diesem Fall sollte das Übertragungsintervall größer gewählt werden.
Das abhängige Lesen von Contacts zu einem Account wird unterstützt und kann für Nachfolgeprozesse verwendet werden.

Der Abfragefilter kann verschieden eingesetzt werden.
Eine Angabe in Feldnotation beginnend mit "id|:|" führt zu einer Einzelabfrage des Datensatzes.
Eine Angabe in Feldnotation mit den Werten "Related" und "RelatedId" kann zum Abfragen von Contacts zu einem Account genutzt werden.
Ansonsten wird der Abfragefilter als URL-Ergänzung verwendet und kann z.B. Suchen realisieren.

Für Contact stehen folgende Optionen zur Verfügung.
Siehe https://developers.activecampaign.com/reference/list-all-contacts

* email=info@mydomain.com
* email_like=mydomain.com
* search=MyLastName

Für Accounts steht der Parameter "search=MyCompany" für eine Suche zur Verfügung.


:Lesen von Abfrage-basierten Daten:

Diese Funktion wird nicht unterstützt.


:Schreiben von Daten:

Das Schreiben von Daten erfolgt über die REST API.
Es können Accounts und Contacts angelegt, aktualisiert oder gelöscht werden.
Die doppelte Verwendung einer Emailadresse löst beim Speichern eine Fehlermeldung aus.


:Schreiben von Bulk-Daten:

Diese Funktion wird nicht unterstützt.


Einstellungen
-------------

:API URL:

Die URL der API. Die Version 3 wird automatisch ergänzt.
Der Wert kann dem Web-Portal entnommen werden.

:API Key:

Der API Key.
Der Wert kann dem Web-Portal entnommen werden.
Die Berechtigungen sind abhängig vom Benutzer, der den API Key erstellt hat.


Besonderheiten
--------------

Für die Kombination mit CAS stehen Vorlagen für eine bidirektionale Synchronisation der Stammdaten zur Verfügung.
Für die Realisierung der Account-Contact-Beziehung werden Transformationen für das Abfragen von vorhandenen
Datenabbildungen eingesetzt. Diese müssen noch manuell auf den jeweiligen Prozess eingestellt werden, damit diese Funktion
zur Verfügung steht.


