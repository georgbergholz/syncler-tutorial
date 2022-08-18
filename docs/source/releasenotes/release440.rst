Release 4.4.0 - 18.08.2022
==========================

Änderungen
----------

Die API hat einen Endpunkt für die Ausführung der Tabellenkalkulation erhalten (RunSpreadsheet).
Die Verwendung ist identisch zum API Endpunkt für Serienbriefe.

Konfigurationsfehler für Serienbriefe und Tabellenkalkulation in Prozessen lösen keine Fehlerwiederholung aus,
da der Fehler nur durch manuelle Anpassung behoben werden kann.

Das Format XLS wurde für die Verbindung Tabellenkalkulation ergänzt.

Die On-Premises Lizenz wurde angepasst. Für den Lizenztyp Basic müssen verfügbare Verbindungstypen definiert werden.
Der Lizenztyp Extended ist nicht betroffen.

Der Schritt "Datendienst ausführen" im Universal Ablauf kann per Checkbox das Resultat als Anhang oder Seriendruck 
mit einer Emailvorlage ausgeben.

Die CAS Fehlermeldung "Data object not found" wird nicht als Fehler, sondern als leere Antwort interpretiert.
Damit kann das Ziel als gelöscht erkannt werden.

Die Anmeldung an der Microsoft Graph API kann optional auch mit Benutzernamen und Passwort erfolgen.

Die Microsoft Graph API Verbindung unterstützt das Objekt OnlineMeeting.

In der Tabellenkalkulation wird die Zelle bei gefundenem Platzhalter für Textdaten nicht komplett ersetzt, sondern nur der Platzhalter.
Damit können auch mehrere Platzhalter in einer Zelle verwendet werden.
Für Zahlen- und Datumswerte wird weiterhin der Zellenwert ersetzt, damit die Zellenformatierung eingehalten werden kann.

In der Microsoft Graph API Verbindung können die Benutzer optional auch in einem Feld mit Semikolon getrennt aufgelistet werden, 
statt eine Abfrage zu verwenden. Als Wert ist die Emailadresse zu verwenden.

In der REST API Verbindung kann neben der automatischen Schemaerzeugung per Beispielabfrage die Feld- und Listen-Eigenschaften des Objekts 
auch mit der properties-Eigenschaft definiert werden. In diesem Fall darf keine Beispiel-ID angegeben werden.
Die Basis der Definition folgt der json-schema.org Konvention, wie sie auch in der SDK Verbindung verwendet wird.

Das Schema für die Tabellenkalkulation Verbindung wurde um die Gruppe AppendSheets erweitert.
Hier kann eine beliebig lange Liste von weiteren Quelldokumenten angegeben werden.
Die Tabellenblätter dieser Dateien werden dem Hauptobjekt hinzugefügt, bevor der Merge ausgeführt wird.
Die Namen der Tabellenblätter werden geprüft und ggf. angepasst, da Dopplungen nicht zulässig sind.

Die Meldung zum Überspringen eines Datensatzes in der Übereinstimmungsregel wurde von Debug auf Rückmeldung geändert.

Die Prozesse zu Sage b7 und IDoc Verbindungen haben einen neuen Parameter erhalten, worüber Quelldaten aus dem Änderungsspeicher 
gelöscht werden können, sollten diese durch den zweiten Filter ausgeschlossen werden.


Korrekturen
-----------

Bei Serienbriefen und Tabellenkalkulation standen Felder in Listen, die durch eine Transformation erzeugt wurden,
nicht in den Daten zur Verfügung, da diese auf oberster Ebene eingefügt wurden.
Diese Felder werden jetzt in das Listenobjekt kopiert und überschreiben ggf. bereits vorhandene gleichnamige Felder.

In der Sage 100 Verbindung wurde bei der Abfrage von geänderten abweichenden Lieferanschriften das Feld Kto nicht gefüllt.
In Einzel- oder Komplettabfragen stand das Feld bereits zur Verfügung.

Beim Anlegen eines Empfängers in der Kopplung CAS nach Cleverreach wird nicht mehr das Aktualisierungsdatum des Empfängers geprüft.
Dieser Wert entspricht dem Registrierungsdatum und hat nur für die entgegengesetzte Richtung eine Relevanz.

In der Kopplung CAS nach Cleverreach lässt eine Warnung im Empfängerprozess den Verteilerprozess nicht mehr stoppen.

In der Microsoft Business Central Verbindung wird bei der Suche nach Feldern mit Änderungsinformationen die
Schreibweise nicht mehr unterschieden.

In der Salesforce Verbindung werden Felder vom Typ Numerisch oder Währung automatisch in die Punktschreibweise vor dem
Schreiben überführt.

Passwörter werden in der API auch für Prozessparameter gecovert.

Das Füllen von Listen im Email-Seriendruck wurde korrigiert.

Die generische Erzeugung eines Json-Objektes wurde korrigiert. Leere Felder in Unterobjekten werden bei Aktualisierungen nicht erneut übertragen.

Die CAS Verbindung für SmartWe erfordert einen TYPE für Berechtigungen.

Eine leere Quelle in der Transformation "Dokument konvertieren" hat zu einer Fehlermeldung geführt.

Der REST API Verbindung sucht die ID von neu angelegten Daten zuerst auf der obersten Feldebene und danach erst in 
Unterstrukturen. Damit sollen falsche Zuordnung durch identische Namen unterbunden werden.

Multitext-Felder in der IDoc Verbindung haben zu einem Fehler geführt, wenn die erste Zeile mit einem Null-Wert übergeben wurde.

Die REST API Verbindung hat untergeordnete Listen mit unbenannten Werten als JValue übernommen, was zu einem Fehler in der 
Verarbeitung geführt hat.

Die Serienbrief- und Tabellenkalkulationsverbindung ignorieren nicht XML-zulässige Zeichen in den übergebenen Daten.
Dies soll die Erzeugung von korrupten Resultaten verhindern.