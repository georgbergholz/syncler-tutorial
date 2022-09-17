Synchronisation zwischen Microsoft 365 und Sage CRM
===================================================

Die Microsoft Graph Verbindung stellt das Objekt "Event" für den Zugriff auf Kalendereinträge zur Verfügung.
Dabei handelt sich um ein geschachteltes Objekt, das die Teilnehmer des Termins als Positionsliste anbietet.
Dieses Objekt kann z.B. in Universalprozessen für die Abfrage von Terminen bzw. auch geänderten Terminen genutzt werden.
Ausgenommen von dieser Art des Zugriffs sind gelöschte Daten und Instanzen einer Serie.
Für eine vollständige Synchronisation müssen aber auch diese Informationen ausgewertet werden.
Deshalb stehen für die Synchronisation von Terminen spezialisierte Prozesse und Vorlagen zur Verfügung.

Es stehen ebenfalls Prozesse und Vorlagen für die Objekte "todoTask" und "Contact" zur Verfügung.
Diese ermöglichen die Synchronisation von Aufgaben und Kontakten.
Die Synchronisation von Aufgaben beschränkt sich auf die Standardliste des Benutzers.

Für eine optimale Unterstützung sollte im CRM in den Systemparametern die Verwendung einer Exchange-Integration
auf "Ja" gestellt werden. Dadurch wird der Organisator-Mechanismus für Termine in der Oberfläche aktiviert.
Eine weitere Einrichtung ist im CRM nicht erforderlich.


Microsoft Graph Ereignis nach Sage CRM Kommunikation
----------------------------------------------------

Dieser Prozess bildet die Richtung Microsoft 365 nach Sage CRM ab.
Für dieses Szenario steht eine Vorlage zur Verfügung, die neben Feldzuordnung auch Teilnehmer aus Benutzern
oder externe Teilnehmer aus Personen verbindet und deren Antwort überträgt.
Die Vorlage bildet den Organisator auf den Organisator des Termins ab und ordnet dabei auch
vorhandene Benutzer zu. Bei externen Organisatoren wird der Schreibschutz am Termin aktiviert (isstub), da keine bidirektionale
Synchronisation möglich ist.
Die Daten werden von der Graph Verbindung mittels Delta-Funktion gelesen. 
Siehe :doc:`/connections/msgraph-connection`

Dabei werden alle Benutzer berücksichtigt, die durch den Benutzerfilter oder -liste in der Verbindung ausgewählt wurden.
Delta-Datum und Delta-Token werden Prozess-bezogen gespeichert.

Serien werden mit Recurrence und RecuMaster übertragen. Die Vorkommen legen dabei die einzelnen
Termine direkt und fortlaufend abhängig vom Zeitfenster an, da die Delta-Funktion nur ein begrenztes Zeitfenster
bereitstellt. Eine Änderung der Serie löscht alle Vorkommen im CRM und erzeugt eine neue Serie.
Eine Seriendefinition ohne Enddatum wird übersprungen, da dies vom CRM nicht unterstützt wird.
Dazu zählen auch Serien mit einer definierten Anzahl.

Ganztägige Termine haben als Endzeit in Microsoft 365 0 Uhr des Folgetages, wohingegen Sage CRM 23:59 Uhr
voraussetzt. Eine Angabe von 0 Uhr wird von Sage CRM wie ein weiterer Tag interpretiert.
Aus diesem Grund wird die Endzeit von ganztägigen Terminen, die auf 0 Uhr enden um 1 Minute zurückdatiert.

:Besonderheiten:

Abgebrochene Termine werden nicht als neue Termine übertragen.
Der Prozess verfügt nur über einen sekundären Filter, da die Delta-Funktion nicht mit einem Filter 
kombiniert werden kann.
Die Vorlage filtert private Termine aus. Sollte dies nicht gewünscht sein, muss der Filter angepasst werden.
In diesem Fall sollte das Privat-Kennzeichen gesetzt werden.
Sage CRM unterstützt keine formatierten Inhalte für die Details. Deshalb wird der Html-Inhalt per 
Transformation in reinen Text konvertiert. Sollte durch eine Änderung eine Übertragung in der entgegengesetzten
Richtung ausgelöst werden, wird der Html-Inhalt mit der Textdarstellung überschrieben.


Microsoft Graph Aufgabe nach Sage CRM Kommunikation
---------------------------------------------------

Für Aufgaben werden in Microsoft 365 keine Anwendungsberechtigungen unterstützt.
Aus diesem Grund können Aufgaben nur für Benutzer synchronisiert werden, wenn diese dem Zugriff mit ihren Zugangsdaten
zustimmen oder eine Benutzeranmeldung in der Verbindung genutzt wird. 
Für die Zustimmung steht in Sage CRM unter Mein CRM eine Registerkarte zur Verfügung, worüber die Zustimmung erteilt 
oder entfernt werden kann.

Für die Synchronisation wird auch hier eine Delta-Abfrage verwendet, die neben Änderungen auch Lösungen erkennt
und überträgt. Das Feld "isDeleted" ist für diesen Fall vorhanden.
Outlook-Aufgaben haben Datumsangaben ohne Zeitwerte. Wenn eine Aufgabe bidirektional übertragen wurde, wären
dadurch die Zeitangaben in den Datumswerten auf 0 Uhr zurückgesetzt.
Damit dies nicht passiert, wird bei Aktualisierungen die Uhrzeit der Sage CRM Aufgabe beibehalten und ggf. nur
der Datumsanteil angepasst.
Dieser Mechanismus wird auf Anfangs-, End- und Benachrichtigungszeit automatisch angewendet.


Sage CRM Kommunikation nach Microsoft Graph Ereignis
----------------------------------------------------

Dieser Prozess und die vorhandene Vorlage realisieren die Synchronisation von Sage CRM Terminen nach
Microsoft 365. 
Der Prozess wendet keine hartkodierten Filter auf die Quelldaten an, sondern die Vorlage enthält die
korrekten Angaben für eine optimale Unterstützung. Wenn Sie den Standardfilter der Vorlage reduzieren,
riskieren Sie eine fehlerhafte Synchronisation.
Serien werden nur über einen Serien-Master (RecuMaster) synchronisiert. Deshalb darf dieser spezielle
Kommunikationsdatensatz nicht ausgeschlossen werden, wenn Serien übertragen werden sollen.

Da über die Schnittstellen von Sage CRM keine gelöschten Datensätze abgerufen werden können,
steht für die Übertragung von Löschungen eigene Prozesse zur Verfügung, die konfigurierte SQL-Zugangsdaten
in der Sage CRM Verbindung voraussetzen.

Sollte eine Serie in Sage CRM geändert werden, wird die Serie in Microsoft 365 gelöscht und neu angelegt.
Sobald eine Serie angelegt wurde, werden die Vorkommen Änderungsspeicher
vorgehalten, damit die Einzeltermine bei der Verarbeitung darüber ihr Ziel identifizieren können.
Die Vorkommen werden dabei über das Startdatum und das Enddatum der Serie abgerufen.

Da ganztägige Termine in Sage CRM auf 23:59 Uhr enden und Microsft 365 Mitternacht voraussetzt,
wird das Enddatum durch den Prozess um eine Minute erhöht.

Damit der Organisator nicht als Teilnehmer dem Termin hinzugefügt wird, wird dieser Link-Eintrag per
Vorlagenfilter übersprungen. Dafür steht extra das Feld Organisator in den Link-Einträgen zur
Verfügung.


Sage CRM Kommunikation nach Microsoft Graph Aufgabe
---------------------------------------------------

Dieser Prozess und die vorhandene Vorlage realisieren die Synchronisation von Sage CRM Aufgaben nach
Microsoft 365. Auch hier werden keine hartkodierten Filter angewendet, sondern sind per Vorlage
voreingestellt.
Die Benutzerzuordnung erfolgt über das Feld "user". Dafür wird die Emailadresse des Benutzers der Aufgabe
abgefragt und zugeordnet.
Dieser Benutzer muss eine Zustimmung für den Zugriff erteilt haben oder an der Verbindung als Zugangsdaten
hinterlegt sein. Ansonsten wird das Speichern mit einer Fehlermeldung abgebrochen.
Sollte nur ein Teil der Benutzer synchronisiert werden, empfiehlt sich ein Prozessfilter auf diese
Benutzer.


Sage CRM Kontakte nach Microsoft Graph Kontakt
----------------------------------------------

Mit diesem Prozess und der vorhandenen Vorlage können Kontakte aus Sage CRM in die Outlook Kontakte synchronisiert werden.
Dabei ist die Basis-Datenquelle die Kontaktzuordnung zwischen Benutzer und Person. Die Details werden dann per 
Transformation nachgeladen und reichern den Kontakt an.
Die CRM Verbindung unterstützt die Änderungsabfrage zu Kontakten mit einer zusätzlichen Prüfung des Aktualisierungsdatum
von Person, Adresse und Firma aus der Sicht vSearchListPerson.
Damit die Übertragung dann nicht an der Synchron-Prüfung stoppt, werden diese Aktualisierungsdaten im Quellobjekt gesucht
und das Maximum wird verwendet.
Damit kann dieser Prozess den Kontakt aktualisieren, wenn sich eine der vier Datenobjekte ändert.


Sage CRM gelöschte Kommunikation nach Microsoft Graph Ereignis
--------------------------------------------------------------

Da über die Schnittstellen von Sage CRM nicht gezielt auf gelöschte Daten geprüft werden kann, sind diese Prozesse erforderlich.
Sie führen eine Abfrage über die eingestellte SQL Verbindung aus und übertragen die Löschung und bereinigen die
Datenabbildungen.


Sage CRM gelöschte Kontakte nach Microsoft Graph Kontakt
--------------------------------------------------------

Da über die Schnittstellen von Sage CRM nicht gezielt auf gelöschte Daten geprüft werden kann, sind diese Prozesse erforderlich.
Sie führen eine Abfrage über die eingestellte SQL Verbindung aus und übertragen die Löschung und bereinigen die
Datenabbildungen.


Sage CRM gelöschte Kommunikation nach Microsoft Graph Aufgabe
-------------------------------------------------------------

Da über die Schnittstellen von Sage CRM nicht gezielt auf gelöschte Daten geprüft werden kann, sind diese Prozesse erforderlich.
Sie führen eine Abfrage über die eingestellte SQL Verbindung aus und übertragen die Löschung und bereinigen die
Datenabbildungen.
