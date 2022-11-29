CleverReach
===========

CleverReach ist ein Email-Marketing-Tool für den Versand und die Auswertung von Email-Kampagnen.
Die CleverReach-Verbindung nutzt die REST API von CleverReach für die Kommunikation.

Für die Einrichtung des Zugangs müssen Sie sich im CleverReach-Portal anmelden.
Wechseln Sie dort in den Bereich

* Mein Account
* Extras
* REST API

Hier müssen Sie eine neue OAuth-App erstellen.
Vergeben Sie einen individuellen Namen und wählen Sie die REST API Version 3 aus.
Abhängig vom Einsatz der Verbindung müssen Sie noch die erforderlichen Scopes aktivieren.
Empfänger und Report benötigen Sie für die Empfängerübertragung und das Abrufen von Resultaten.
Nachdem Sie die App gespeichert haben, rufen Sie erneut den Bearbeitungsdialog mit dem 3-Punkte-Icon auf.
Jetzt stehen Ihnen zusätzliche Registerkarten zur Verfügung, die die benötigten Informationen enthalten.
Wechseln Sie zu "Oauth2 App Daten".
Übernehmen Sie die Client ID und das Client Secret in die entsprechenden Felder der Verbindung.
Um einen Refresh Token zu generieren, müssen Sie die Schaltfläche "Prozess jetzt testen" anklicken.
Es öffnet sich ein neues Fenster, wo Sie sich erneut mit Ihren CleverReach-Zugangsdaten anmelden müssen.
Nach der erfolgreichen Anmeldung erhalten Sie eine Tabelle, aus der Sie den Refresh Token in das Feld der Verbindung übernehmen müssen.
Mit dem Speichern der Verbindung haben Sie die Einrichtung abgeschlossen.
Der Refresh Token ist 30 Tage gültig und wird automatisch erneuert, wenn die Verbindung verwendet wird.
Sollten Sie die Verbindung mehr als 30 Tage nicht benutzen, muss ein neuer Refresh Token mit der Schaltfläche "Prozess jetzt testen" abgerufen werden.


Funktionen
----------

:Schema ermitteln:

Das Schema wird von der Verbindung fest erstellt.
Das Empfänger-Schema wird mit benutzerdefinierten globalen Attributen in einer eigenen Objektgruppe ergänzt.
Sobald eine Gruppen-ID in den Verbindungseinstellungen hinterlegt wird, werden auch Gruppenattribute in einer eigenen Objektgruppe ergänzt.
Für die Arbeit mit Tags werden zwei Verfahren unterstützt.
Wenn "Tags als Freitext" abgeschaltet ist, werden die vorhandenen Tags ermittelt und als einzelne Felder in einer Objektgruppe dem Schema hinzugefügt.
Sollten neue Tags hinzukommen, muss das Schema der Verbindung aktualisiert werden.
Wenn "Tags als Freitext" eingeschaltet ist, steht im Empfängerschema das Feld "tags" zur Verfügung, welches alle Tags in getrennter Form enthält.
Nur bei diesem Verfahren stehen auch automatisch neue Tags zur Verfügung.
Für die Verarbeitung muss dann allerdings z.B. auf Transformationen zurückgegriffen werden.
Das Empfängerschema enthält neben der ID auch noch die Gruppen-ID als Identifikator, da nur mit beiden Werten auch Gruppenattribute zur Verfügung stehen.


:Lesen von Schema-basierten Daten:

Das Lesen von Daten erfolgt über die REST API.
Abhängig vom Schemaobjekt stehen verschiedene Parameter nicht zur Verfügung.

Gruppen können einzeln oder als Liste und auch mittels Änderungserkennung gelesen werden.
Ein Filter kann für Gruppen nicht eingesetzt werden.

Mailings können einzeln oder als Liste und auch mittels Änderungserkennung gelesen werden.
Mittels Feldnotation können noch folgende Kriterien zur Einschränkung angegeben werden: limit, channel_id, state, start und end.

Empfänger können einzeln oder als Liste abgerufen werden. Die Abfrage benötigt eine Gruppe, die über die Verbindung oder spezialisierte Prozesse definiert werden kann.
Sollte keine Gruppe angegeben werden, werden zuerst alle Gruppen und dann alle Empfänger dieser Gruppen abgerufen.
Empfänger haben keine Änderungsinformation, wodurch eine Änderungsübertragung ausgehend von CleverReach so nicht möglich ist.
Die Aktualisierung eines Empfängers ändert jedoch das Änderungsdatum der Gruppe.
Durch die Verbindung wird das Registrierungsdatum des Empfängers als Änderungsdatum herangezogen.
Dadurch können keine geänderten Empfänger abgerufen, aber kontinuierlich neue Empfänger übertragen werden.

Resultate oder Links können nur mit den spezialisierten Prozessen oder mit SDK-Prozessen abgerufen werden, da hier immer ein übergordneter Datensatz angegeben werden muss
Dies wird mit den Parameter "GETDATA_RELATED" und "GETDATA_RELATED_ID" gesteuert.
"GETDATA_RELATED" kann dabei die Werte groups, mailings oder reports annehmen.


:Lesen von Abfrage-basierten Daten:

Diese Funktion wird nicht unterstützt.


:Schreiben von Daten:

Das Schreiben von Daten erfolgt über die REST API.
Empfänger können einzeln gespeichert werden. 
Einige spezialisierte Prozesse unterstützen ein UPSERT-Verfahren zum Abgleich einer Liste von Empfängern.


:Schreiben von Bulk-Daten:

Diese Funktion wird nicht unterstützt.


Einstellungen
-------------

:Client ID:

Die ID der OAuth App.

:Client Secret:

Der Geheimschlüssel der OAuth App.

:Refresh Token:

Der aktuelle Refresh Token. Bei fortlaufender Benutzung wird dieser Wert automatisch aktualisiert.

:Gruppen-ID:

Damit gruppenspezifische Attribute angesprochen werden können, muss hier die Gruppen-ID hinterlegt werden. Außerdem kann diese Gruppen-ID als Standardgruppe verwendet werden.

:Tags als Freitext:

Tags werden im Empfänger-Schema als kommata- und leerzeichengetrennter Freitext in einem Feld gepflegt statt als einzelne Spalten in einem Unterobjekt.

