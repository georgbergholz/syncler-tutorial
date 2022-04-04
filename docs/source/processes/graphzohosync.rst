Termin-Synchronisation zwischen Office 365 und Zoho CRM (Draft)
=======================================================

Die Microsoft Graph Verbindung stellt das Objekt "Event" für den Zugriff auf Kalendereinträge zur Verfügung.
Dabei handelt sich um ein geschachteltes Objekt, das die Teilnehmer des Termins als Positionsliste anbietet.
Dieses Objekt kann z.B. in Universalprozessen für die Abfrage von Terminen bzw. auch geänderten Terminen genutzt werden.
Ausgenommen von dieser Art des Zugriffs sind gelöschte Daten und Instanzen einer Serie.
Für eine vollständige Synchronisation müssen aber auch diese Informationen ausgewertet werden.
Deshalb stehen für die Synchronisation von Terminen eigene Prozesse zur Verfügung.

Microsoft Graph Ereignis nach Zoho CRM Meeting
----------------------------------------------

Dieser Prozess bildet die Richtung Office 365 nach Zoho CRM ab.
Dieser Prozess muss auf einen Benutzer eingeschränkt werden, damit alle Änderungen des Kalenders (delta) erfasst werden können.
Für weitere Benutzer muss der Prozess dubliziert werden.

Die Abfrage von Terminen muss für die Delta-Funktion auf ein Zeitfenster eingeschränkt werden.
Dies kann an der Verbindung eingestellt werden.
Durch den Prozess schreitet das Zeitfenster mit dem Wechsel des Tages weiter.

Bei Zoho CRM muss berücksichtigt werden, dass eine Seriendefinition nachträglich nicht verändert werden kann.
Sollte dies erforderlich werden, muss die Serie in Office 365 gelöscht und neu angelegt werden.
Ansonsten werden weitere Vorkommen in Zoho als Einzeltermine ohne Serienbezug angelegt.

Sobald eine Serie in Zoho CRM erzeugt wird, werden die IDs der Vorkommen im Änderungsspeicher abgelegt.
Sobald ein Vorkommen der Serie aus Office 365 verarbeitet wird, wird über den Änderungsspeicher und 
dem Startdatum das Ziel gesucht und verknüpft.
Dies ermöglich eine Synchronisation der Vorkommen und ggf. einzelner Anpassungen an Vorkommen, sogenannte Ausnahmen.

Bei diesem Verfahren ist zu beachten, dass der Änderungsspeicher ggf. gewartet wird. 
Ein Vorkommen außerhalb des Zeitfensters wird ggf. erst stark verzögert verarbeitet und hat dann keine Möglichkeit mehr, 
ein Ziel zuzuordnen.
In diesem Fall wäre eine Synchronisation von Ausnahmen nicht mehr möglich.

Bei einer bidirektionalen Synchronisation ist zu beachten, dass anhand der Zoho CRM Daten nicht unterschieden werden kann, 
ob es sich um ein Vorkommen oder eine Ausnahme handelt.
Deshalb werden alle Einträge aktualisiert, wodurch diese in Office 365 automatisch zu Ausnahmen werden.

Wenn Termine aus dem Kalender entfernt werden, steht die iCalUId nicht mehr zur Verfügung.
Für diesen Fall wird die ID in der Datenabbildung gespeichert.
Eine generelle Arbeit mit der ID ist nicht möglich, da sich diese zwischen Kalendern für dn selben Termin unterscheiden
und das zur Anlage von Dubletten führen würde.

Folgende Besonderheiten gelten für diesen Prozess.

- Es muss ein Benutzer eingestellt werden, dessen Kalender synchronisiert wird.
- Die Änderungsermittlung erfolgt mit der Delta-Funktion, die nur ein festes Zeitfenster betrachten kann.
- Das Zeitfenster wird mit jedem neuen Tag vorgeschoben, was zur Abfrage aller Kalendereinträge führt. Über die Datenabbildung wird das Änderungsdatum verglichen und ggf. keine Abfrage an Zoho ausgelöst, um das API-Limit nicht zu belasten.
- Der Serien-Master wird für die Anlage einer Serie genutzt. Danach werden nur noch die Vorkommen synchronisiert.
- Termine werden nur gelöscht, wenn der aktuelle Benutzer auch der Organisator ist, oder der Organisator nicht in Zoho CRM als Benutzer vorhanden ist.
- Das Löschen entfernt auch Datenabbildungen, damit ggf. der Termin neu angelegt werden kann, falls dieser nur aus dem betrachteten Zeitfenster verschoben wurde.
- Abgebrochene Termine werden nicht als neue Termine übertragen. Dies ist bei Teilnehmern eines gelöschten Termins der Fall.
- Vorkommen werden nach der Anlage über den Änderungsspeicher einem Serienziel zugeordnet. Bei Terminen außerhalb des Zeitfensters kann das durch die Wartung des Änderungsspeichers zur Anlage einer Dublette führen.
- Vorkommen werden nur über den Organisator synchronisiert, da die id sich bei Teilnehmern unterscheidet.
- Die Teilnehmer eines Termin können sich verändern, je nach dem mit welchem Benutzer der Termin verarbeitet wird. Bei Nicht-Organisatoren wird der Organisator als Teilnehmer geführt. Wird der selbe Termin über den Organisator verarbeitet, ist der Organisator nicht Teilnehmer des Termins.
- Der Prozess verfügt nur über einen sekundären Filter, da die Delta-Funktion nicht mit einem Filter kombiniert werden kann.

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