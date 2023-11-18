KlickTipp
=========

KlickTipp ist ein Tool für Newsletter und Marketing Automation.
Die Datenstruktur ist geprägt von Tagging, um Attribute, Aktivitäten und Historien zu Kontakten zu erfassen.


Schemaobjekte
-------------

Folgende Schemaobjekte stehen zur Verfügung.

:Tag:

Dieses Objekt ist die Basis für das Tagging und die Abfrage von anderen Objekten.
Tags können nur einzeln per ID oder komplett abgerufen werden.
Die ID kann für AdHoc-Ausführungen direkt oder als Filter in Feldnotation übergeben werden.
Als Filter kann in Feldnotation auch eine Namenssuche übergeben werden.
Tags können nur erzeugt werden.

:Subscriber:

Subscriber sind die Kontakte oder Empfänger, die per Newsletter angeschrieben werden.
Das Schema enthält sowohl Standard- also auch benutzerdefinierte Felder.
Zugeordnete Tags sind als Array-Feld lesend verfügbar.
Subscriber können nur einzeln per ID oder komplett abgerufen werden.
Die ID kann für Adhoc oder direkt als Filter übergeben werden.

:tagsubscriber:

TagSubscriber dient zum Markieren von vorhandenen Kontakten.
Das Schema wird für schreibende Zugriffe verwendet.
Es muss die Emailadresse und ein Array von TagIds übergeben werden.

:taggedsubscriber:

Dieses Schema wird für das Lesen verwendet.
Es muss eine ID oder ein Filter übergeben werden, der als TagID interpretiert wird.
Das Ergebnis ist eine Liste von Datensätzen mit SubscriberID, Datum und TagID.
Diese Subscriber sind mit dem übergebenen Tag verknüpft.
Das Datum ist der Zeitpunkt der Verknüpfung.

