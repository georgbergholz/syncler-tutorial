Email-Archivierung mit CAS
==========================

Die Verarbeitung von eingehenden Email gehört zu einer häufigen Aufgabe.
In diesem Beispiel wird die Archivierung einer eingehenden Email in CAS beschrieben.


Ausgangspunkt für die Lösung sind eine Email-Verbindung für das Lesen von Nachrichten und 
eine CAS-Verbindung für das Speichern der Nachricht.

Für die Archivierung stehen zwei Wege zur Auswahl.
Sie können eine Email als Email in CAS archivieren und verarbeiten.
Außerdem können Sie ausschließlich die Anhänge einer Email einzeln archivieren und verarbeiten.

Archivierung als Email
----------------------

Für die Archivierung als Email kommt der Prozess "Universal Sync Prozess für Email" zum Einsatz.
Dieser Prozess hat als mögliche Quelle die Email-Verbindung.
Als Ziel können Sie jede vorhandene Verbindung und Objekt auswählen.
In unserem Fall wählen wir die CAS-Verbindung aus und als Zielobjekt "EMAILSTORE".


Die Archivierung der Email funktioniert auf der Basis von EML-Daten.
Die Email-Verbindung stellt die EML-Daten im Feld "EML (FileContent)" bereit.
Unser Ziel verfügt ebenfalls über ein Feld "EML (FileContent)".
Stellen Sie eine Verbindung zwischen den Feldern her und die Nachricht wird komplett archiviert.

Zusätzlich können Sie jetzt noch Verknüpfungen zu anderen CAS-Daten herstellen.
Nutzen Sie die Transformation, um z.B. Nummern aus dem Betreff per regulärem Ausdruck zu extrahieren.
Damit können Sie Daten abfragen, um z.B. die GGUID einer Verkaufschance zu ermitteln.
Erzeugen Sie noch einen Parameter für den OBJECTTYPE und weisen Sie beides den "LinkFrom"-Feldern zu.

Es stehen noch weitere Email-Optionen zur Verfügung, um eine verarbeitete Email zu löschen oder zu verschieben.
Generell arbeitet der Prozess aber mit einem Änderungsdatum, womit nur neue Emails verarbeitet werden können.
Außerdem erzeugt der Prozess Datenabbildungen, wodurch eine bereits abgelegte Email nicht erneut archiviert wird. 
Es können aber nachträglich noch Verknüpfungen zu archivierten Emails aktualisiert werden.

An der Beispielvorlage "Email-Archivierung in CAS" können Sie Vorgehensweise nachvollziehen.

Archivierung als Dokument
-------------------------

Für die Archivierung als Dokument kommt der Prozess "Email Anhänge nach CAS Dokument" zum Einsatz.
Dieser Prozess verarbeitet ausschließlich die Anhänge eine Email.
Sie können aber die Nachricht nutzen, um Felder und Verknüpfungen des Dokuments festzulegen.
Diese Angaben werden für jeden Anhang wiederverwendet.
Außerdem stehen Parameter zur Verfügung, um Mindestgröße und Dateityp zu kontrollieren.