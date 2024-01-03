[Gestern 16:07] Tom Fuchs
Hey Georg,
folgende Anpassung müssen im CAS getroffen werden, um die Prozesse von bzw. nach MsGraph anzuwenden (alles mit ML abgesprochen):
Es muss eine Verknüpfung angelegt werden mit dem Namen "ORGANIZER" von Terminen nach Adressen (m:1). (zwingend)
Die Benutzer müssen somit im CAS als Mitarbeiter (Adressen) angelegt werden. (nicht zwingend aber sinnvoll)
Es muss sichergestellt werden, dass das Hinzufügen von Teilnehmer bzw. des Organisators als Adresse, das Änderungsdatum aktualisiert. Das kann über eine Berechnung der Teilnehmeranzahl in die Appointmenttabelle geschehen und mit der Übertragung der GUID des Organisators in die Appointment-Tabelle. (nicht zwingend aber sinnvoll)
Als Hinweis:
Es müssen keine Teilnehmer über das Feldmapping hinzugefügt werden, die werden automatisch anhand der Email-Adresse mit Benutzern und Adressen im CAS verbunden
Im CAS sollten die Teilnehmer/ der Organisator über die Adressen hinzugefügt werden. Sie können aber auch über die standardmäßige Teilnehmerliste des Termins hinzugefügt werden.
Beim Organisator gilt dann folgende Reihenfolge bei der Übernahme
Organisator als Adresse
Benutzer mit den meisten Rechten (bei mehreren -> Zufall)

[Gestern 16:09] Tom Fuchs
Falls ich den Vorgang von RTC schneller fertig bekomme, setze ich mich nochmal an den Delete Prozess. Das geht über die APPOINTMENTBIN Tabelle.