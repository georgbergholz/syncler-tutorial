Synchronisation zwischen Microsoft 365 und Zoho CRM
===================================================

Die Microsoft Graph Verbindung stellt das Objekt "Event" für den Zugriff auf Kalendereinträge zur Verfügung.
Dabei handelt sich um ein geschachteltes Objekt, das die Teilnehmer des Termins als Positionsliste anbietet.
Dieses Objekt kann z.B. in Universalprozessen für die Abfrage von Terminen bzw. auch geänderten Terminen genutzt werden.
Ausgenommen von dieser Art des Zugriffs sind gelöschte Daten und Instanzen einer Serie.
Für eine vollständige Synchronisation müssen aber auch diese Informationen ausgewertet werden.
Deshalb stehen für die Synchronisation von Terminen eigene Prozesse und Vorlagen zur Verfügung.

Microsoft Graph Ereignis nach Zoho CRM Meeting
----------------------------------------------

Dieser Prozess bildet die Richtung Microsoft 365 nach Zoho CRM ab.
Für dieses Szenario steht eine Vorlage zur Verfügung, die neben Feldzuordnung auch Teilnehmer aus Benutzern, Kontakten oder 
Interessenten verbindet und deren Antwort überträgt.
Wenn der Teilnehmer in diesen Bereichen nicht gefunden wird, kann er als Emailadresse übernommen werden.
Für diesen Fall setzt Zoho eine gültige Emailadresse voraus, ansonsten wird das Speichern mit einer Fehlermeldung
abgebrochen. Dies wird bereits in der Vorlage behandelt.
Die Vorlage bildet den Organisator auf den Host des Meetings ab. Sollte dies nicht möglich sein, wird der Verbindungsadministrator 
automatisch von Zoho zugeordnet. In der Vorlage werden diese Termine aber über den zweiten Filter übersprungen.
Da Zoho keine privaten Termine unterstützt, werden diese in der Vorlage bereits ausgefiltert.
Die Daten werden von der Graph Verbindung mittels Delta-Funktion gelesen. 
Siehe :doc:`/connections/msgraph-connection`

Dabei werden alle Benutzer berücksichtigt, die durch den Benutzerfilter oder -liste in der Verbindung ausgewählt wurden.
Delta-Datum und Delta-Token werden Prozess-bezogen intern gespeichert.

Serien werden mittels Seriendefinition in Zoho angelegt.
Eine nachträgliche Änderung der Serie lässt Zoho nicht zu.
Sollte eine Serie angelegt oder aktualisiert werden, werden alle Serientermine im Zoho gelöscht und die Datensätze neu angelegt.
Im Anschluss findet ein Abgleich der Serienvorkommen statt, damit ggf. Lücken und Ausnahmen übernommen werden.
Unbegrenzte Serien werden nicht unterstützt und übersprungen.

Eine Serie mit einer definierten Anzahl wird auf das Maximum von Zoho von 99 begrenzt, da die Serie sonst nicht 
angelegt werden kann.

Die Delta-Funktion synchronisiert nur ein definiertes Zeitfenster.
Durch den Abgleich der Serientermine können aber auch Termine bzw. Vorkommen außerhalb des Zeitfensters synchronisiert werden.

Bei einer bidirektionalen Synchronisation ist zu beachten, dass anhand der Zoho CRM Daten nicht unterschieden werden kann, 
ob es sich um ein Vorkommen oder eine Ausnahme handelt.
Deshalb werden alle Einträge aktualisiert, wodurch diese in Microsoft 365 automatisch zu Ausnahmen werden.

:Besonderheiten:

Abgebrochene Termine werden nicht als neue Termine übertragen.
Der Prozess verfügt nur über einen sekundären Filter, da die Delta-Funktion nicht mit einem Filter 
kombiniert werden kann.

Ganztägige Termine haben als Endzeit in Microsoft 365 0 Uhr des Folgetages, wohingegen Zoho 23:59 Uhr
voraussetzt.

Zoho unterstützt keine formatierten Inhalte für die Details. Deshalb wird der Html-Inhalt per 
Transformation in reinen Text konvertiert. Sollte durch eine Änderung eine Übertragung in der entgegengesetzten
Richtung ausgelöst werden, wird der Html-Inhalt mit der Textdarstellung überschrieben.


Zoho CRM Meeting nach Microsoft Graph Ereignis
----------------------------------------------

Dieser Prozess bildet die Richtung Zoho CRM nach Microsoft 365 ab und arbeitet auf der Basis des Änderungsdatums 
von Meetings. Da bei dieser Art der Abfrage keine gelöschten Datensätze erfasst werden, ist hierfür ein 
weiterer Prozess erforderlich, für den ebenfalls eine Vorlage bereitgestellt wird.

Der Owner des Termins wird in der Vorlage als Organisator zugeordnet. Deshalb ist es erforderlich, dass alle 
im Prozess berücksichtigten Benutzer auch Mitglied des Unternehmens sind, da sonst die Neuanlage nicht 
möglich ist.
Bei Aktualisierungen wird der Graph Benutzer verwendet, über den der Termin abgerufen wurde.

Serien in Zoho CRM haben keinen direkt nutzbaren Master, sondern sind über $u_id verbunden.
Der Serienmaster in Microsoft 365 erhält eine Datenabbildung zu dieser $u_id, damit bekannt ist, dass eine Serie bereits angelegt wurde.
Dies wird auch in umgekehrter Richtung vorgenommen.
Sollte diese Datenabbildung nicht vorliegen, wird eine neue Serie mit dem Muster aus Zoho angelegt.
Nach der Anlage einer Serie werden die Vorkommen abgeglichen, damit Lücken und Ausnahmen übertragen werden.

Da Serien in Zoho nicht geändert werden können, entfällt das Löschen und Neuanlagen einer kompletten Serie.

:Besonderheiten:

Problematisch ist die Verarbeitung von ganztägigen Terminen.
Diese werden von Zoho fälschlicherweise mit 0 Uhr UTC zurückgeliefert.
Der Prozess korrigiert deshalb einen positiven Zeitzonen-Offset, damit der korrekte Tag zugeordnet wird.
Negative Zeitzonen-Offsets müssen per Transformation ausgeglichen werden, was nicht Teil der Vorlage ist.


Zoho CRM gelöschte Meetings nach Microsoft Graph Ereignis
---------------------------------------------------------

Diese Vorlage basiert auf einem Standardprozess, der gelöschte Datensätze in Zoho ermittelt und für Aktualisierung oder 
Löschen nutzen kann.
Dabei werden die Ereignisse in Mircosoft 365 über vorhandene Datenabbildungen zwischen den eingestellten Verbindungen ermittelt.
Diese werden gelöscht und auch die Datenabbildungen werden entfernt.
