CleverReach
===========

CleverReach ist ein Email-Marketing-Tool f�r den Versand und die Auswertung von Email-Kampagnen.
Die CleverReach-Verbindung nutzt die REST API von CleverReach f�r die Kommunikation.

F�r die Einrichtung des Zugangs m�ssen Sie sich im CleverReach-Portal anmelden.
Wechseln Sie dort in den Bereich

* Mein Account
* Extras
* REST API

Hier m�ssen Sie eine neue OAuth-App erstellen.
Vergeben Sie einen individuellen Namen und w�hlen Sie die REST API Version 3 aus.
Abh�ngig vom Einsatz der Verbindung m�ssen Sie noch die erforderlichen Scopes aktivieren.
Empf�nger und Report ben�tigen Sie f�r die Empf�nger�bertragung und das Abrufen von Resultaten.
Nachdem Sie die App gespeichert haben, rufen Sie erneut den Bearbeitungsdialog mit dem 3-Punkte-Icon auf.
Jetzt stehen Ihnen zus�tzliche Registerkarten zur Verf�gung, die die ben�tigten Informationen enthalten.
Wechseln Sie zu "Oauth2 App Daten".
�bernehmen Sie die Client ID und das Client Secret in die entsprechenden Felder der Verbindung.
Um einen Refresh Token zu generieren, m�ssen Sie die Schaltfl�che "Prozess jetzt testen" anklicken.
Es �ffnet sich ein neues Fenster, wo Sie sich erneut mit Ihren CleverReach-Zugangsdaten anmelden m�ssen.
Nach der erfolgreichen Anmeldung erhalten Sie eine Tabelle, aus der Sie den Refresh Token in das Feld der Verbindung �bernehmen m�ssen.
Mit dem Speichern der Verbindung haben Sie die Einrichtung abgeschlossen.
Der Refresh Token ist 30 Tage g�ltig und wird automatisch erneuert, wenn die Verbindung verwendet wird.
Sollten Sie die Verbindung mehr als 30 Tage nicht benutzen, muss ein neuer Refresh Token mit der Schaltfl�che "Prozess jetzt testen" abgerufen werden.


Funktionen
----------

:Schema ermitteln:

Das Schema wird von der Verbindung fest erstellt.
Das Empf�nger-Schema wird mit benutzerdefinierten globalen Attributen in einer eigenen Objektgruppe erg�nzt.
Sobald eine Gruppen-ID in den Verbindungseinstellungen hinterlegt wird, werden auch Gruppenattribute in einer eigenen Objektgruppe erg�nzt.
F�r die Arbeit mit Tags werden zwei Verfahren unterst�tzt.
Wenn "Tags als Freitext" abgeschaltet ist, werden die vorhandenen Tags ermittelt und als einzelne Felder in einer Objektgruppe dem Schema hinzugef�gt.
Sollten neue Tags hinzukommen, muss das Schema der Verbindung aktualisiert werden.
Wenn "Tags als Freitext" eingeschaltet ist, steht im Empf�ngerschema das Feld "tags" zur Verf�gung, welches alle Tags in getrennter Form enth�lt.
Nur bei diesem Verfahren stehen auch automatisch neue Tags zur Verf�gung.
F�r die Verarbeitung muss dann allerdings z.B. auf Transformationen zur�ckgegriffen werden.
Das Empf�ngerschema enth�lt neben der ID auch noch die Gruppen-ID als Identifikator, da nur mit beiden Werten auch Gruppenattribute zur Verf�gung stehen.


:Lesen von Schema-basierten Daten:

Das Lesen von Daten erfolgt �ber die REST API.
Abh�ngig vom Schemaobjekt stehen verschiedene Parameter nicht zur Verf�gung.

Gruppen k�nnen einzeln oder als Liste und auch mittels �nderungserkennung gelesen werden.
Ein Filter kann f�r Gruppen nicht eingesetzt werden.

Mailings k�nnen einzeln oder als Liste und auch mittels �nderungserkennung gelesen werden.
Mittels Feldnotation k�nnen noch folgende Kriterien zur Einschr�nkung angegeben werden: limit, channel_id, state, start und end.

Empf�nger k�nnen einzeln oder als Liste abgerufen werden. Die Abfrage ben�tigt eine Gruppe, die �ber die Verbindung oder spezialisierte Prozesse definiert werden kann.
Sollte keine Gruppe angegeben werden, werden zuerst alle Gruppen und dann alle Empf�nger dieser Gruppen abgerufen.
Empf�nger haben keine �nderungsinformation, wodurch eine �nderungs�bertragung ausgehend von CleverReach so nicht m�glich ist.
Die Aktualisierung eines Empf�ngers �ndert jedoch das �nderungsdatum der Gruppe.
Durch die Verbindung wird das Registrierungsdatum des Empf�ngers als �nderungsdatum herangezogen.
Dadurch k�nnen keine ge�nderten Empf�nger abgerufen, aber kontinuierlich neue Empf�nger �bertragen werden.

Resultate oder Links k�nnen nur mit den spezialisierten Prozessen oder mit SDK-Prozessen abgerufen werden, da hier immer ein �bergordneter Datensatz angegeben werden muss
Dies wird mit den Parameter "GETDATA_RELATED" und "GETDATA_RELATED_ID" gesteuert.
"GETDATA_RELATED" kann dabei die Werte groups, mailings oder reports annehmen.


:Lesen von Abfrage-basierten Daten:

Diese Funktion wird nicht unterst�tzt.


:Schreiben von Daten:

Das Schreiben von Daten erfolgt �ber die REST API.
Empf�nger k�nnen einzeln gespeichert werden. 
Einige spezialisierte Prozesse unterst�tzen ein UPSERT-Verfahren zum Abgleich einer Liste von Empf�ngern.


:Schreiben von Bulk-Daten:

Diese Funktion wird nicht unterst�tzt.


Einstellungen
-------------

:Client ID:

Die ID der OAuth App.

:Client Secret:

Der Geheimschl�ssel der OAuth App.

:Refresh Token:

Der aktuelle Refresh Token. Bei fortlaufender Benutzung wird dieser Wert automatisch aktualisiert.

:Gruppen-ID:

Damit gruppenspezifische Attribute angesprochen werden k�nnen, muss hier die Gruppen-ID hinterlegt werden. Au�erdem kann diese Gruppen-ID als Standardgruppe verwendet werden.

:Tags als Freitext:

Tags werden im Empf�nger-Schema als kommata- und leerzeichengetrennter Freitext in einem Feld gepflegt statt als einzelne Spalten in einem Unterobjekt.

