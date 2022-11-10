Release 4.4.2 - 11.11.2022
==========================

Änderungen
----------

Die Graph Verbindung:

* Die Filter-Abfragen in Feldnotation kann um "user" ergänzt werden, damit die Abfrage bei vielen Benutzern beschleunigt wird.
* Benutzer mit leerer Emailadresse werden bei der Verarbeitung übersprungen, da diese zu fehlerhaften Abfragen führen.
* Die Warnungen bei Abfragen wurden in Debug-Meldungen umgewandelt.
* Per Parameter kann der Client als Public-Client definiert werden. Dies ist für das Zustimmungsverfahren relevant.
* Es wurden zusätzliche Fehlermeldungen für Hintergrundabfragen eingefügt, damit Fehlerquellen leichter gefunden werden.
* Die Benutzerauswahl kann durch die Angabe eines Gruppennames getroffen werden. Benutzer, die zur Gruppe hinzugefügt werden, werden dann automatisch synchronisiert. Diese Funktion setzt zusätzliche Berechtigungen voraus.

Prozess "SQL nach interne Auswahlliste":

* Es kann eine beliebige Zielverbindung ausgewählt werden. Diese wird dann der Auswahlliste zugeordnet und in deren Prozessen kann die Auswahlliste dann verwendet werden.

Die Abläufe unterstützen Abfrage-Prozesse und es stehen auch Prozesse für das Lesen von Abfragen zur Verfügung.
Dafür müssen Abfragen eine Identität für jeden Datensatzes erzeugen. 
Dies geschieht abgestuft. Sollte eine ID bekannt sein, wird diese verwendet. 
Sollte ein Änderungsdatensatz zugeordnet sein, wird dessen GUID verwendet. Ansonsten wird eine temporäre GUID erzeugt.

Die globale Konfiguration für On-premises hat einen neuen Parameter "Erweiterte Fehlermeldung" erhalten, der einen StackTrace in Fehlermeldungen aktivieren kann.

In Abläufen können in der Prozessausführung über eine Feldnotation mit Platzhaltern (z.B. GUID|:|#GGUID#|;|) Daten aus dem Zieldatensatz in den zwischengespeicherten
Quelldatensatz übernommen werden. Diese stehen dann in folgenden Schritten zur Verfügung, wenn diese ebenfalls die zwischengespeicherten Quelldaten verwenden.

Die Fehlermeldungen von Zoho CRM werden interpretiert und übersetzt zurückgemeldet.

Die REST Verbindung:

* Mit einem Parameter kann das Datumsformat für Json-Daten definiert werden, welches für Lesen und Schreiben genutzt wird.
* Das Abfragen von Änderungen ersetzt auch die Platzhalter "LastDatetime" und "LastVersion". Bisher wurden nur "LAST_SYNC_DATE" und "LAST_SYNC_VERSION" ersetzt.
* Einzelabfragen ohne ID-Platzhalter werden nicht ausgeführt.

Der SMTP-Versand in On-premises Installationen und die Email Verbindung unterstützen das OAuth 2.0 Verfahren für Microsoft 365.
Die Unterscheidung erfolgt durch die Angabe einer Client-ID.

Die generische Aktualisierung des Quellobjektes:
Dieses Verfahren wurde vereinheitlicht und in verschiedenen Prozessen ergänzt.
Es werden zwei Verfahren unterschieden, für reproduzierbare und für nicht reproduzierbare Datensätze.
Außerdem können für die Fälle Erfolgreich, Fehlerhaft und Übersprungen individuelle Daten aktualisiert werden.
Bei dem Verfahren für nicht reproduzierbare Datensätze wird ein Schema und eine Suchbedingung für die Aktualisierung definiert.
Bei folgenden Prozessen wurde die Funktion ergänzt.

* Alle Abfrage-Prozesse mit beschreibbarer Quelle
* Prozesse zur Kombination aus CAS und Sage 100
* Prozesse zur Kombination aus CAS und Business Central
* Prozesse zur Kombination aus Salesforce und Sage 100
* Prozesse zur Kombination aus Salesforce und IDoc
* Prozesse zur Kombination aus Sage CRM und Sage 100
* Prozesse zur Kombination aus Zoho CRM und Sage 100

Die HotFolder-Prozesse können einen Unterordner zum Basisorder aus der HotFolder Verbindung definieren.

Die Seriendruck Verbindung hat im Schema 4 neue Parameter für die Ausführungssteuerung erhalten.
Durch "RemoveEmptyRange" (Bool) werden Bereiche ohne gefüllte Felder komplett entfernt.
Diese Option führt bei Dokumenten ohne Seriendruckfelder zum Leeren des Dokuments.
Um das zuverhindern kann ein "BaseRangeName" definiert werden, der dann mittels RangeStart und RangeEnd das Dokument umschließt.
Mit "RemoveEmptyTableRows" werden Zeilen mit Feldern ohne Quelldaten komplett entfernt, unabhängig von sonstigen Inhalten. 
Diese Funktion ist jetzt nicht länger standardmäßig aktiviert.
Mit "RemoveEmptyTables" werden Tabellen mit Feldern ohne Quelldaten komplett entfernt, unabhängig von sonstigen Inhalten. 
Diese Funktion ist jetzt nicht länger standardmäßig aktiviert.
Bei der Verarbeitung von Bildern mit dem Präfix "Picture:" kann im Json auch die Breite in Bildpunkten angegeben werden.
Die Grafik wird dann entsprechend skaliert. Die unterstützen Eigenschaften im Json sind "FileMethod", "File" und "Width".

Im Syncler Administrator kann eine Adhoc-Ausführung ausgehend vom Änderungsspeicher gestartet werden.

Es gibt neue Vorlagen für die Synchronisation zwischen SpiceCRM und Sage 100. Das SpiceCRM wird dabei über die REST Verbindung angebunden.

Korrekturen
-----------

Synchronisation von Microsoft 365 nach Zoho CRM:

* Der Prozess prüft auf ganztägige Termine und passt die Endzeit für Zoho CRM an, da dort 23:59 Uhr erwartet wird.

Die Vorlage wurde ebenfalls angepasst. 

* Die Organizer-ID wird mit dem zweiten Filter auf ungleich leer geprüft.
* Das Setzen der Benachrichtigungsfunktion wurde entfernt.
* Die Positionsübereinstimmung sucht nach Email, Id oder Participant.

Syncler Administrator:

* In der Transformation "Datenabbildung abfragen" wurde das Ändern des Prozesses nicht als Änderung erkannt.
* In der Transformation "Werte abbilden" wurde an den Abbildungen eine Aktualisierungsfunktion ergänzt.

Die Fehlerbehandlung in Abläufen wurde korrigiert.

* Der ursprüngliche Parameter im Warteschlangendatensatz wurde umbenannt, wodurch nur eine einmalige Wiederholung möglich war.
* Wiederholte Datensätze wurden nicht in die zwischengespeicherten Listen aufgenommen, wodurch diese für Folgeschritte nicht zur Verfügung standen.
* Ein Prozess mit zwischengespeicherten Daten wurde nur ausgeführt, wenn der Zwischenspeicher Einträge enthielt. Die Fehlerbehandlung wurde ohne Einträge nicht ausgeführt.
* Nur manuell ausgeführte Prozesse werden bei erfolgreichem Resultat übersprungen.

Die Nachrichtenausgabe durch eine Verbindung wurde in der Transformation "Abfrage ausführen" ergänzt.

Die Sage 100 Verbindung:

* Die Antwort zu neu angelegten Kontokorrenten in Kombination mit einer Adresse hat nur die Versionsnummer der Adresse zurückgemeldet. Das hatte Einfluss auf die Änderungsprüfung mittels Datenabbildung.

In Prozessen, die das Quellobjekt verändert haben, wurde die neue Änderungsinformation für die Datenabbildung verwendet.
Dadurch bestand die Möglichkeit, dass Änderungen zwischen dem Lesen und dem Aktualisieren nicht erkannt werden.

Die Sage CRM Verbindung:

* Wenn die SQL-Bridge und die SQL Zugangsdaten definiert wurden, hat die Validierung nicht die SQL-Bridge verwendet.

Bei schreibenden Datenbankzugriffen werden leere Zeichenketten zu Datums- und numerischen Felder nicht übergeben, da dies zu einem Convert-Fehler führt.
Der Parameter verwendet dann den NULL-Wert.

Die Seriendruck-Prozesse haben bei der Grenzwertbehandlung nicht zwischen Datum und Version unterschieden, was zu einem Typ-Fehler führen konnte.

Die Seriendruck Verbindung:

* Die Behandlung von Bildern wurde korrigiert. Der Präfix "Picture:" wird nur in der Vorlage verwendet.

Der Prozess für den Emailversand von Serienbriefen wurde korrigiert. 
Die Quelldaten wurden nicht an die Email Verbindung übergeben, wodurch Platzhalter in der Nachricht nicht ersetzt wurden.