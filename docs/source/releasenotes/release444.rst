Release 4.4.4 - 22.03.2023
==========================

Änderungen
----------

Die Sage b7-Verbindung

* Die Verbindung wurde grundlegend überarbeitet und auf die Bibliothek Azure.Messaging.ServiceBus migriert.

Der Syncler Administrator

* In den Bereichen Datenabbildung, Protokolle, Änderungsspeicher und Sicherungsspeicher steht eine neue Datensatz-Zusammenfassung zur Verfügung, welche Informationen trennt und Felder in Listenform ausgibt.
* Mit einem Doppelklick können Feldinhalte leicht entnommen werden.

Der Prozess "Sage CRM Aufgabe nach Microsoft Aufgabe".

* Ein geänderter Benutzer im CRM führt zum Löschen der Aufgabe im ursprünglichen Postfach und zum Neuanlegen im aktuellen Postfach. Damit kann eine neu zugewiesene Aufgabe synchronisiert werden.
* Dabei werden auch die Datenabbildungen gelöscht, damit die Aufgabe nicht im CRM gelöscht wird, falls der neue Benutzer nicht synchronisiert wird.

Die Zoho CRM-Verbindung

* Es werden Contact-Roles zwischen Abschlüssen und Kontakten unterstützt. Siehe :doc:`/bestpractices/zohocontactroles`
* Es werden Notes für andere Module unterstützt. Für Notes steht ein eigenes Schema-Objekt zur Verfügung.
* Per Filter können Datensätze aus einer Beziehung abgefragt werden. Die Formulierung erfolgt in Feldnotation mit den Parametern "Related" und "RelatedId". Der Filter "Related|:|Accounts|;|RelatedId|:|1234|;|" ruft nur die Datensätze zu diesem Account ab.

Der Universal-Löschprozess

* Es wurden Feldzuordnungen, Adhoc-Ausführungen und Filter freigegeben.

Die Universal-Prozesse

* Mit einem zusätzlichen Parameter kann festgelegt werden, ob die IDs in Datenabbildungen Groß- und Kleinschreibung unterscheiden müssen.

Der Prozess "SAP Beleg nach Salesforce Opportunity"

* Mit einer zusätzlichen Suche können Positionen für die Aktualisierung zugeordnet werden.
* Ohne eine Suchangabe erfolgt die Zuordnung weiterhin über die Reihenfolge der Positionen.

Die SQL-Brücke

* Die API der SQL-Brücke hat den neuen Endpunkt "Check", der die Verfügbarkeit der API prüfen kann.

Die Salesforce-Verbindung

* Das Speichern einer Verkaufschance unterstützt das kombinierte Schreiben von Opportunity und OpportunityLineItems.

Die Graph-Verbindung

* Mit einem Parameter können die Tage bis zur Aktualisierung des Zeitfensters eingestellt werden. Damit müssen nicht jeden Tag alle Termine des neuen Zeitfensters geprüft werden.
* Das Teilnehmer-Schema hat die Felder isExternalOrganizer und isCurrentUser erhalten. Beide werden gefüllt, wenn es sich um einen externen Organisator handelt und der Teilnehmer auch der aktuelle Benutzer der Abfrage ist.
* Der Refresh-Token wird automatisch bei der Anforderung eines Access-Tokens aktualisiert.

Die Serienbrief-Verbindung

* Das Schema für die Serienbrieferzeugung wurde um "InsertDocument" erweitert. Über einen "InsertMarker" im Hauptdokument kann ein fremdes Dokument gezielt eingefügt werden. Das Einfügen erfolgt auf Block-Ebene, wodurch Kopf- und Fußzeile nicht übernommen werden.
* Einem Feld mit dem Präfix "Picture:" kann neben einer Json-Anweisung auch direkt eine Url für das Einbinden einer Grafik übergeben werden.

Die Support-Datenbank

* Das neue Feature "Support-Datenbank" steht zur Verfügung und kann gebucht werden.
* Damit wird eine neue Datenbank für den Account angelegt, deren Größe in die maximale Datenbankgröße mit eingerechnet wird.
* Innerhalb dieser Datenbank besteht weitestgehend eine SQL-Autonomie.
* Es können beliebig Tabellen amgelegt oder importiert werden.
* Die Importfunktion kann auch vorhandene Tabellen erweitern oder leeren.
* Als Importquelle können Xlsx- oder CSV-Dateien genutzt werden.
* Außerdem steht eine neue Verbindung "Support-Datenbank" zur Verfügung, über die dieser Bereich in die Prozessausführung integriert werden kann.
* Es können Tabellen über Prozesse gefüllt oder mit beliebigen SELECT-Anweisung für Prozesse ausgelesen werden.
* Jede vorhandene Tabelle erzeugt dabei ein eigenes Schema für diese Verbindung.
* Es können auch SQL-Anweisungen innerhalb der Datenbank mit einem Prozess ausgeführt werden.
* Im Syncler Administrator steht eine Tabellenbearbeitung für die Inhalte der Tabelle zur Verfügung.
* Siehe :doc:`/common/supportdatabase`

CSV-Prozesse

* Die Parameter LastDateTime- und LastVersion-Spalten wurden aktiviert, damit diese Informationen in der Verarbeitung genutzt werden können, um eine synchrone Situation zu erkennen.

Webhooks

* Webhooks unterstützen die Verwendung eines Abfrageprozesses für das Lesen von Daten. Dafür steht ein neuer Filterparameter zur Verfügung, der in die Abfrage einefügt werden kann.
* Webhooks können Formulardaten empfangen und verarbeiten. Die Unterscheidung erfolgt über den Content-Type der Anfrage.
* Zusätzlich kann eine LandingPage für die Weiterleitung definiert werden. Dadurch kann ein Webhook als Universal-Empfänger für Web-Formulare verwendet werden.
* Webhooks können die empfangenen Daten im Änderungsspeicher für einen Prozess ablegen.
* Mit einem speziellen Leseprozess können die Daten aus dem Änderungsspeicher in einem Ablauf verarbeitet werden.
* Wenn ein Webhook Daten mit einer Verbindung speichert, kann das Lese-Schema für die Rückgabe von Daten genutzt werden. Damit können z.B. erzeugte IDs weiterverarbeitet werden.

MailChimp-Prozesse für Sage CRM Marketing-Center

* Für das Sage CRM Addon "Marketing-Center" stehen Prozesse für die Verarbeitung zur Verfügung.

Die MailChimp-Verbindung

* Die Verbindung unterstützt Clicks, Opens und Email-Activities.

Die Sage WinCarat-Verbindung

* Für Syncler steht die Verbindung zu Sage WinCarat zur Verfügung.
* Für die Synchronisation können die Universal-Prozesse genutzt werden.
* Die Interessenten-Konvertierung kann mit separaten Prozessen und einer eigenen laufenden Mandantennummer umgesetzt werden. Voraussetzung dafür ist ein gleichbleibendes Kriterium, z.B. der Matchcode.

Der Testlauf in Prozessen

* Der Testlauf innerhalb der Transformation wurde grundlegend überarbeitet und erweitert.
* Es können Quelldaten per Filter oder aus Abfragen ermittelt werden.
* Außerdem können Zieldaten über ID, Filter oder Datenabbildung gelesen und die Feldzuordnungen getestet werden.
* Änderungen werden dabei farblich hervorgehoben.
* Siehe :doc:`/processes/converting/dryrun`

Die Transformation "Webhook aufrufen"

* Diese neue Transformation kann einen beliebigen Webhook aufrufen, um Daten zu lesen oder zu schreiben.
* Siehe :doc:`/processes/converting/webhook`

Die Transformation "Json in Spalten"

* Diese neue Transformation kann Json-Daten aus einem Feld in einzelne Spalten überführen.
* Siehe :doc:`/processes/converting/jsontocolumn`


Korrekturen
-----------

Die Sage b7-Verbindung

* Die Verarbeitung von geteilten Nachrichten prüft die ID des Datensatzes eines jeden Teils für die Zusammenführung. Bisher wurde nur die Reihenfolge verwendet, was bei wiederholtem Lesen von Nachrichten zu Fehlern führen konnte.
* Das Löschen von Nachrichten erfolgt bereits bei der Verarbeitung, damit das Lock-Timeout nicht überschritten wird. Dies war in der Cloud-Umgebung durch die eingeschränkte Parallelität möglich und hat zum wiederholten Lesen von Nachrichten geführt.
* Bei geteilten Nachrichten erfolgt das Löschen erst bei der Verarbeitung des letzten Teils.

Die Sage CRM-Verbindung

* Die Prüfung des Organisators einer Kommunikation und die Zwangsverknüpfung als Teilnehmer wurde auch bei Aufgaben angewendet. Dadurch könnten zusätzliche Kommunikationslinks für Aufgaben entstehen.

Die Graph-Verbindung

* Das Änderungsdatum des Serienmasters wurde bei der Delta-Verarbeitung noch an die Vorkommen übergeben. Das führte durch die neue Serienverarbeitung zu unnötigen Änderungserkennungen und Konfliktwarnungen.
* Der Vergleich zwischen Organisator und aktuellem Benutzer war case-sensitiv. Das konnte beim Schreiben von Terminen zu einem Fehler führen, falls sich die Schreibweise zwischen den Systemen unterschieden hat.
* Beim Schreiben einer Aufgabe wurde das Fehlen des Refresh-Tokens als Fehler interpretiert. Jetzt wird eine Warnung und Überspringen ausgelöst.

Die InxMail-Verbindung

* Das Abrufen eines gelöschten Datensatzes führt zu einen 404-Fehler, der als Fehler behandelt und nicht als gelöschtes Ziel interpretiert wurde.

Die Vorlagen für Prozesse ausgehend von Microsoft Graph

* Die Vorlagen haben eine Transformation "Dokument konvertieren" für die Umwandlung von HTML zu Text verwendet. Falls der Termin oder die Aufgabe aber bereits reinen Text enthalten hat, wurden dadurch Zeilenumbrüche entfernt.
* Jetzt wird die Transformation "Html zu Text" verwendet, bei der Zeilenumbrüche erhalten bleiben.

Die CAS-Verbindung

* Die bisherige Abfrage nach Verknüpfungen hat deaktivierte Adressen nicht berücksichtigt.

Interne Abfragen zu Datenabbildungen mit externen IDs verwenden einen Unicode-Präfix, da sonst Datenabbildung unter Umständen nicht gefunden werden.

Das Zurückschreiben in Prozessen wurde angepasst, damit nur tatsächliche Änderungen erkannt und übertragen werden.

Der Prozess "Microsoft Graph Ereignis nach Zoho CRM Meeting"

* Wenn die Funktion "Alle zukünftigen Vorkommen aktualisieren" im Zoho genutzt wird, ändert sich die u_id bei diesen Datensätzen. Das ist vergleichbar mit einem Splitting der Serie.
* Außerdem ist das Serienschema der neuen Serie mit der alten vermischt und damit ungültig.
* Bei der Neuanlage einer Serie wurden so nicht alle Vorkommen entfernt und es kam zu Dubletten.
* Das neue Verfahren löscht die Zielvorkommen über die Datenabbildungen.

Der Prozess "Zoho CRM Meeting nach Microsoft Graph Ereignis"

* Wenn die Funktion "Alle zukünftigen Vorkommen aktualisieren" im Zoho genutzt wird, ändert sich die u_id bei diesen Datensätzen. Das ist vergleichbar mit einem Splitting der Serie.
* Da das Serienschema der einzelnen Teile aber fehlerhaft ist, werden nicht alle Vorkommen korrekt angelegt.
* Die Ermittlung des Anfangs und Ende der Serie erfolgt deshalb über das Maximum und Minimum aus den Vorkommen.

In den Bulk und CSV-Prozessen kam es zu einem Konvertierungsfehler bei der Verwendung von Datensatzversionsnummern.

Das OAuth2-Anmeldeverfahren fordert zum Login statt zur Account-Auswahl auf. Damit kann ein Login auch gewechselt werden.

Das Oauth2-Anmeldverfahren im Syncler Administrator gibt ggf. eine Fehlerbeschreibung aus.