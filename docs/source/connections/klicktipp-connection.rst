KlickTipp
=========

KlickTipp ist ein Tool für Newsletter und Marketing Automation.
Die Datenstruktur ist geprägt von Tagging, um Attribute, Aktivitäten und Historien zu Kontakten zu erfassen.
Für die Anmeldung muss an der Verbindung der Benutzername und das Passwort eingegeben werden.

Schemaobjekte
-------------

Folgende Schemaobjekte stehen zur Verfügung.

:tag:

Dieses Objekt ist die Basis für das Tagging und die Abfrage von anderen Objekten.
Tags können nur einzeln per ID oder komplett abgerufen werden.
Die ID kann für AdHoc-Ausführungen direkt oder als Filter in Feldnotation übergeben werden.
Als Filter kann in Feldnotation auch eine Namenssuche übergeben werden.
Tags können erzeugt und aktualisiert werden.

:subscriber:

Subscriber sind die Kontakte oder Empfänger, die per Newsletter angeschrieben werden.
Das Schema enthält sowohl Standard- also auch benutzerdefinierte Felder.
Zugeordnete Tags sind als Array-Feld lesend verfügbar.
Subscriber können einzeln per ID oder komplett abgerufen werden.
Außerdem ist eine Abfrage mit einem Filter in Feldnotation möglich. Hierfür stehen die Felder id und email zur Verfügung.
Eine Abfrage über Tags muss mit dem Schemaobjekt taggedsubscriber erfolgen.
Die Array-Felder in den Daten enthalten entweder eine ID als Wert oder eine ID als Name und ein Datum als Wert. Das Datum liegt als Unix-Timestamp vor.
Subscriber können angelegt und aktualisiert werden.
Über die Objektgruppe addTag können direkt mehrere Tags zugeordnet werden. Dafür muss auch das Feld email in dieser Gruppe zugeordnet werden.

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

