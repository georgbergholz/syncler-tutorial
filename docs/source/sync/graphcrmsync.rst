Synchronisation zwischen Microsoft 365 und Sage CRM
===================================================

Die Microsoft Graph Verbindung stellt das Objekt "Event" für den Zugriff auf Kalendereinträge zur Verfügung.
Dabei handelt sich um ein geschachteltes Objekt, das die Teilnehmer des Termins als Positionsliste anbietet.
Dieses Objekt kann z.B. in Universalprozessen für die Abfrage von Terminen bzw. auch geänderten Terminen genutzt werden.
Ausgenommen von dieser Art des Zugriffs sind gelöschte Daten und Instanzen einer Serie.
Für eine vollständige Synchronisation müssen aber auch diese Informationen ausgewertet werden.
Deshalb stehen für die Synchronisation von Terminen eigene Prozesse zur Verfügung.

Es stehen ebenfalls Prozesse für die Objekte "todoTask" und "Contact" zur Verfügung.
Diese ermöglichen die Synchronisation von Aufgaben und Kontakten.

Für eine optimale Unterstützung sollte im CRM in den Systemparametern die Verwendung einer Exchange-Integration
auf "Ja" gestellt werden. Dadurch wird der Organisator-Mechanismus für Termine in der Oberfläche aktiviert.
Eine weitere Einrichtung ist im CRM nicht erforderlich.


Microsoft Graph Ereignis nach Sage CRM Kommunikation
----------------------------------------------------

Dieser Prozess bildet die Richtung Microsoft 365 nach Sage CRM ab.
Für dieses Szenario steht eine Vorlage zur Verfügung, die neben Feldzuordnung auch Teilnehmer aus Benutzern
oder externe Teilnehmer aus Personen verbindet und deren Antwort überträgt.
Die Vorlage bildet den Organisator auf den Organisator des Termins ab und ordnet dabei auch
vorhandene Benutzer zu. Bei externen Organisatoren wird der Schreibschutz am Termin aktiviert, da keine bidirektionale
Synchronisation möglich ist.
Die Daten werden von der Graph Verbindung mittels Delta-Funktion gelesen. Siehe :doc:`/connections/msgraph-connection`

Dabei werden alle Benutzer berücksichtigt, die durch den Benutzerfilter in der Verbindung ausgewählt wurden.
Delta-Datum und Delta-Token werden Prozess-bezogen gespeichert.

Serien werden mit Recurrence und RecuMaster übertragen. Die Vorkommen legen dabei die einzelnen
Termine direkt und fortlaufend abhängig vom Zeitfenster an, da die Delta-Funktion nur ein begrenztes Zeitfenster
bereitstellt. Eine Änderung der Serie löscht alle Vorkommen im CRM und erzeugt eine neue Serie.
Eine Seriendefinition ohne Enddatum wird übersprungen, da dies vom CRM nicht unterstützt wird.
Dazu zählen auch Serien mit einer definierten Anzahl.

Besonderheiten
--------------

Abgebrochene Termine werden nicht als neue Termine übertragen.
Der Prozess verfügt nur über einen sekundären Filter, da die Delta-Funktion nicht mit einem Filter 
kombiniert werden kann.


Microsoft Graph Aufgabe nach Sage CRM Kommunikation
---------------------------------------------------

Für Aufgaben werden in Microsoft 365 keine Anwendungsberechtigungen unterstützt.
Aus diesem Grund können Aufgaben nur für Benutzer synchronisiert werden, wenn diese dem Zugriff mit ihren Zugangsdaten
zustimmen. Hierfür steht im CRM unter Mein CRM eine Registerkarte zur Verfügung, worüber die Zustimmung erteilt 
werden kann.





Sage CRM Kommunikation nach Microsoft Graph Ereignis
----------------------------------------------------





Sage CRM Kommunikation nach Microsoft Graph Aufgabe
---------------------------------------------------



Sage CRM Kontakte nach Microsoft Graph Kontakt
----------------------------------------------


Sage CRM gelöschte Kommunikation nach Microsoft Graph Ereignis
--------------------------------------------------------------


Sage CRM gelöschte Kontakte nach Microsoft Graph Kontakt
--------------------------------------------------------




Sage CRM gelöschte Kommunikation nach Microsoft Graph Aufgabe
-------------------------------------------------------------




