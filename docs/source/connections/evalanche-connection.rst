Evalanche
=========

Evalanche ist eine Marketing Automation Plattform und kann u.a. für den Versand und die Auswertung von Newslettern genutzt werden.
Mit dieser Verbindung können Sie die Empfänger Ihrer Kampagnen mit jedem beliebigen System synchronisieren.
Sie erhalten Zugriff auf verschiedene Auswertungen und können diese in andere Systeme übertragen.

Die Verbindung nutzt die SOAP-Schnittstelle von Evalanche für die Kommunikation.
Für die Einrichtung benötigen Sie nur die Domain, Benutzername und Passwort.

Eine eingerichtete Verbindung ist mit einem Mandanten und einem Pool verbunden.


Funktionen
----------

:Schema ermitteln:

Das Schema der Verbindung wird über die SOAP-API ermittelt.
Es stehen Mailing, MailingDetails, MailingStatistics, Article, Profile, Recipient, Bounce, Unsubscription, GrantedPermission, RevokePermission, Impression (Openings) und Clicks zur Verfügung.


:Lesen von Schema-basierten Daten:
 
Das Lesen von Datensätzen erfolgt über die SOAP-API.
Die Zugriff erfolgen in der Regel mit Universalprozessen.
Die Verbindung bereitet Daten auf, damit diese möglichst einfach verwendet werden können.
Zum Beispiel werden Clicks mit der Url des Links angereichert.
Profile (Empfänger) können beliebig angelegt, aktualisiert oder gelöscht werden. Auch können Berechtigungen gesetzt oder entfernt werden.
Profile verfügen über ein Änderungsdatum, was eine Änderungs-basierte Synchronisation ermöglicht.

:Lesen von Abfrage-basierten Daten:

Diese Funktion wird nicht unterstützt.


:Schreiben von Daten:

Das Schreiben von Datensätzen erfolgt über die SOAP-API.
Für das Schreiben oder Löschen können die Entitäten Profile und RevokePermission genutzt werden.


Einstellungen
-------------

Folgende Einstellungen können bereitgestellt werden.

:Login Domäne:

Die Domäne Ihrer Anmeldung.

:Benutzername:

Der Benutzername Ihrer Anmeldung.

:Passwort:

Das Passwort Ihrer Anmeldung.

:Mandant ID:

Die ID des zuverwendenden Mandanten.
Wenn nicht eingetragen wird, wird der Wert ggf. aus dem Namen ermittelt oder der erste verfügbare Mandant ausgewählt.

:Mandant Name:

Der Name des zuverwendenden Mandanten.
Wenn nicht eingetragen wird, wird der Wert ggf. aus der ID ermittelt oder der erste verfügbare Mandant ausgewählt.

:Pool ID:

Die ID des zuverwendenden Pools.
Wenn nicht eingetragen wird, wird der Wert ggf. aus dem Namen ermittelt oder der erste verfügbare Pool des Mandanten ausgewählt.

:Pool Name:

Der Name des zuverwendenden Pools.
Wenn nicht eingetragen wird, wird der Wert ggf. aus der ID ermittelt oder der erste verfügbare Pool des Mandanten ausgewählt.