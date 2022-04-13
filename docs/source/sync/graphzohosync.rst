Termin-Synchronisation zwischen Microsoft 365 und Zoho CRM
=======================================================

Die Microsoft Graph Verbindung stellt das Objekt "Event" für den Zugriff auf Kalendereinträge zur Verfügung.
Dabei handelt sich um ein geschachteltes Objekt, das die Teilnehmer des Termins als Positionsliste anbietet.
Dieses Objekt kann z.B. in Universalprozessen für die Abfrage von Terminen bzw. auch geänderten Terminen genutzt werden.
Ausgenommen von dieser Art des Zugriffs sind gelöschte Daten und Instanzen einer Serie.
Für eine vollständige Synchronisation müssen aber auch diese Informationen ausgewertet werden.
Deshalb stehen für die Synchronisation von Terminen eigene Prozesse zur Verfügung.

Microsoft Graph Ereignis nach Zoho CRM Meeting
----------------------------------------------

Dieser Prozess bildet die Richtung Microsoft 365 nach Zoho CRM ab.
Für dieses Szenario steht eine Vorlage zur Verfügung, die neben Feldzuordnung auch Teilnehmer aus Benutzern, Kontakten oder 
Interessenten verbindet und deren Antwort überträgt.
Die Vorlage bildet den Organisator auf den Host des Meetings ab. Sollte dies nicht möglich sein, wird der Verbindungsadministrator 
automatisch von Zoho zugeordnet.
Die Daten werden von der Graph Verbindung mittels Delta-Funktion gelesen. Siehe :doc:`/connections/msgraph-connection`

Dabei werden alle Benutzer berücksichtigt, die durch den Benutzerfilter in der Verbindung ausgewählt wurden.
Delta-Datum und Delta-Token werden Prozess-bezogen gespeichert.

Serien werden mittels Seriendefinition in Zoho angelegt.
Eine nachträgliche Änderung der Serie lässt Zoho nicht zu.
Sollten neue Vorkommen hinzukommen, werden diese als Einzeltermine in Zoho ohne direkten Bezug zur Serie angelegt.

Die Delta-Funktion synchronisiert nur ein definiertes Zeitfenster.
Durch die Serien-Anlage können auch Meetings in Zoho vorhanden sein, die sich außerhalb des Zeitfensters befinden.
Eine Änderung an der Serie wirkt sich aktuell nur auf Termine im Zeitfenster aus.
Zukünftige Termine außerhalb des Zeitfensters können also noch einen alten Stand aufweisen.
Wenn dies nicht gewünscht ist, kann explizit das Feld "update_all_future_events" zugeordnet werden.
Dies beachtet allerdings keine Ausnahmen, weshalb es in der Vorlage nicht zugewiesen wird.

Bei der Anlage einer Serie werden die IDs der Vorkommen im Änderungsspeicher abgelegt.
Sobald ein Vorkommen der Serie aus Microsoft 365 verarbeitet wird, wird über den Änderungsspeicher und 
dem Startdatum das Ziel gesucht und verknüpft.
Dies ermöglich eine Synchronisation der Vorkommen und ggf. einzelner Anpassungen an Vorkommen, sogenannte Ausnahmen.

Bei diesem Verfahren ist zu beachten, dass der Änderungsspeicher ggf. gewartet wird. 
Ein Vorkommen außerhalb des Zeitfensters wird ggf. erst verzögert verarbeitet und hat dann keine Möglichkeit mehr, 
ein Ziel zuzuordnen.

Bei einer bidirektionalen Synchronisation ist zu beachten, dass anhand der Zoho CRM Daten nicht unterschieden werden kann, 
ob es sich um ein Vorkommen oder eine Ausnahme handelt.
Deshalb werden alle Einträge aktualisiert, wodurch diese in Microsoft 365 automatisch zu Ausnahmen werden.

Besonderheiten
--------------

Abgebrochene Termine werden nicht als neue Termine übertragen.
Der Prozess verfügt nur über einen sekundären Filter, da die Delta-Funktion nicht mit einem Filter kombiniert werden kann.


Zoho CRM Meeting nach Microsoft Graph Ereignis
----------------------------------------------








Dieser Prozess bildet die Richtung Zoho CRM nach Office 365 ab.
Eine Einschränkung auf einen Benutzer ist nicht erforderlich, da die Änderungserkennung über das Änderungsdatum realisiert wird.
Für das Löschen von Ereignissen ist ein weiterer Prozess erforderlich.

Der Owner des Termins wird in der Vorlage als Organisator zugeordnet.
Es muss ein Organisator zugeordnet werden, damit die Anlage und Aktualisierung von Ereignissen möglich ist.

Serientermine in Zoho CRM haben keinen direkt nutzbaren Master, sondern sind über $u_id verbunden.
Der Serienmaster in Office 365 erhält eine Datenabbildung zu dieser $u_id, damit bekannt ist, dass eine Serie bereits angelegt wurde.
Sollte diese Datenabbildung nicht vorliegen, wird eine neue Serie mit dem Muster aus Zoho angelegt.
Auch hier werden Änderungsdatensätze mit dem IDs der Serieninstanzen angelegt, damit die Vorkommen in Zoho eine Verbindung
herstellen können. Dies beschränkt sich auf Instanzen des aktuell über die Verbindung definierten Zeitfensters.
Bei der Anlage einer Serie wird eine Datenabbildung für den Serienmaster und eine für das aktuelle Vorkommen angelegt.

Folgende Besonderheiten gelten für diesen Prozess.

- Bei Serienterminen wird über die $u_id im Änderungsspeicher nach vorhandenen Instanzen gesucht und diese ggf. zugeordnet.
- Wenn für die $u_id keine Datenabbildung gefunden wird (zum Serienmaster) wird eine neue Serie angelegt.    