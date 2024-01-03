Die Entwicklung eines Verbindungsplugins in .Net
================================================

Jedes Verbindungsplugin wird durch eine Klasse implementiert, die von ConnectionBase ableitet.
Die Klasse wird in einer .Net Bibliothek entwickelt, die das SynclerCommon Assembly einbindet.
Bereitgestellt wird die DLL der Bibliothek in den connections Verzeichnissen der Installation.
Diese werden nur beim Start des Systems eingelesen.

In der Basisklasse werden virtuelle Methoden definiert, die in den Verbindungsplugins individuell implementiert werden.
Diese Methoden dienen der Steuerung des Verbindungsplugins.
Bei der Planung eines Verbindungsplugins müssen diese Berührungspunkte mit der Syncler Umgebung berücksichtigt werden.

Auch stehen Eigenschaften bereit, die verwendet werden könnnen.
Unter anderen werden Objekte für den Zugriff auf die Konfiguration der Instanz, die aktuelle Datenbank und Übersetzungen bereitgestellt.

* SisDatabaseWrapper Database: Datenbank-Instanz
* SisTenantConfig Config: Konfiguration der Instanz
* SisTenantInstance Instance: Instanz mit Übersetzer

Die Benutzeroberfläche für die Konfiguration der Verbindung wird durch Attribute an der Klasse und den Eigenschaften definiert.
Die Page-Attribute an der Klasse aktivieren bestimmte Konfigurationsseiten.
Mit 'PageCommon' wird die Konfiguration von Eigenschaften aktiviert.
Eigenschaften können mit Attributen beschriftet und kategorisiert werden.
Auch Anleitungstexte lassen sich so platzieren.
Für alle Texte können Übersetzungscodes aus den erweiterbaren XML-Übersetzungsdateien genutzt werden.

* LocalizedCategory: übersetzte Kategorie
* LocalizedDisplayName: übersetzte Beschriftung
* LocalizedDescription: übersetzte Anleitung

Mit weiteren Attributen kann die Konfiguration noch detailierter definiert werden.

* CommaSeparatedValues: komma-separierte Daten
* JsonFormat: Legt ein Schema für JSON-Daten fest
* KeyValueList: Liste von Name-Wert-Paaren in Feldnotation
* LocalizedEnumDescription: für die Übersetzung von Enumerations
* Multiline: mehrzeiliger Wert
* OnlyMaster: Eigenschaft steht nur On-premises zur Verfügung
* Required: Es muss ein Wert festgelegt werden
* RequiresSchemaRefresh: Eine Änderung erzwingt ein Schema-Refresh

Einsatz der Verbindung
----------------------

Von der Verbindung wird bei Konfiguration eine verschlüsselte Serialisierung in der Datenbank gespeichert.
Sobald die Verbindung verwendet wird, wird für jede Anforderung eine Instanz erzeugt und ausgeführt.
In einer parallelen Ausführung existieren dadurch mehrere Instanzen dieser Klasse, die untereinander keine Berührungspunkte haben.
Aus diesem Grund sollten gemeinsam genutzte Informationen zur Laufzeit (z.B. Token) nicht in der Verbindung, sondern separat in der Parameter-Tabelle gespeichert werden.
Wird eine Verbindung nicht weiter benötigt, wird diese wieder aus dem Speicher entfernt.
Geänderte Informationen in der Verbindung gehen dabei verloren bzw. werden zurückgesetzt.


Planen einer Verbindung
-----------------------

Wenn Sie eine Verbindung planen, muss die Funktion mit den Berühungspunkten zum Syncler abgestimmt werden.
Daraus ergeben sich dann Vorgehensweisen für die Implementierung.

Nutzung der Verbindung
----------------------

Folgende Fällen lassen sich bei der Nutzung unterscheiden.

:Konfiguration:

Die Konfiguration erfolgt über die Benutzeroberfläche des Synclers und wird durch Attribute gesteuert.
Durch die Attribute können bereits Pflichtfelder und ähnliches definiert werden, die der Benutzer angeben muss.
Beim Speichern der Verbindung und vor der Nutzung durch einen Prozess wird die Validate-Methode aufgerufen.
Diese kann Prüfungen durchführen, die die Einsatzfähigkeit gewährleisten.
Ggf. aufgetretene Fehler werden als Rückgabe der Methode gemeldet.
Eine positive Antwort ist ein null-Wert.
Bei einer direkten Verwendung der Verbindung durch die API wird die Validate-Methode nicht aufgerufen.

:Schema:

Jede Verbindung kann Schemaobjekte bereitstellen, die in u.a. Prozessen verwendet werden.
Die Gestaltung von Schemaobjekten ist dabei relativ frei und muss durch die Verbindung verarbeitet werden.
So können z.B. Datenobjekte für CRUD-Operationen definiert werden.
Auch lassen sich Funktionen mittels Schemaobjekt bereitstellen, die dann durch Prozesse ausgelöst werden.
Schemaobjekte können auch beliebig geschachtelt werden, um z.B. logische Business-Objekte bereitzustellen.
Schemaobjekte können ID-Werte für das Objekt definieren.
Dies ist die Voraussetzung für einen Sync, der Datenabbildungen nutzen soll.
Auch können Einzelausführung nur mit ID-Werten ausgelöst werden.
Ein Datensatz ohne ID-Werte wird immer als neu interpretiert.
Zusätzlich kann ein Schemaobjekt eine Änderungsinformation definieren.
Diese wird in Prozessen genutzt, um Grenzwerte für eine änderungsbasierte Synchronisation zu ermitteln.
Das Konfliktmanagement basiert ebenfalls auf dieser Information.
Wichtig hierbei ist, dass beim Schreiben eines Datensatzes die aktuellen Daten zurückgeliefert werden.

Das Schema wird durch die Methode GetConnectionSchema erzeugt.
Diese liefert ein Dictionary mit dem Namen als Key und einer XML-Serialisierung des SisSchemaObject als Value zurück.
Die Methode wird automatisch bei der Neuanlage ausgeführt und jedesmal beim Speichern mit aktivierter Schema-Aktualisierung.
Nachdem die Methode ausgeführt wurde, wird die Verbindung erneut gespeichert.

:Schema-basiertes Lesen:

Ein lesender Aufruf an die Verbindung mit einem Schema wird durch die Methode GetData ausgeführt.
Dies erhält das aktuelle Schemaobjekt und eine Liste von Parametern.
Die Methode muss nun alle Anwendungsfälle umsetzen, die sich aus Parametern und Schema-Objekt ergeben.
Sollte die Ausführung durch den Benutzer abgebrochen werden, wird CancellationPending gesetzt. 
Die Behandlung muss in der Verbindung erfolgen und an geeignete Ausstiegspunkte geprüft werden. 
In diesem Fall muss mit der Exception SisOperationCanceledException die Verarbeitung verlassen werden.

Folgende Parameter werden verwendet und müssen für eine fehlerfreie und optimierte Nutzung ausgewertet werden.

* SisParam_ProcessObjects: Die gelesenen Daten sollen nicht als Rückgabe, sondern über die Methode ProcessMethod fortlaufend geliefert werden.
* SisParam_GetDataById: Ein einzelner Datensatz soll gelesen werden. Der Wert kann in Feldnotation übergeben werden.
* SisParam_NoMessage: Es sollen keine Nachrichten bei der Verarbeitung erzeugt werden. Ansonsten können Nachrichten über die Methode MessageMethod ausgegeben werden.
* SisParam_GetDataByWhere: Stellt den Filter für eine Listenabfrage durch einen Prozess bereit.
* SisParam_GetDataLimit: Die Rückgabe soll auf einen Anzahl von Datensätzen beschränkt werden. Dies wird durch Testläufe in der Konfiguration von Prozessen genutzt.

:Abfrage-basiertes Lesen:

Abfrage-Prozesse und Reports nutzen diese Art des Lesens. Eine Implementierung ist optional für diese Anwendungsfälle.
Die Methode GetQuerySchema wird aufgerufen, um das Schema der aktuellen Abfrage zu ermitteln und in der Konfiguration zu verwenden.
Die Methode GetQueryData wird bei der Anforderung von Daten aufgerufen.
Beide Methoden erhalten die definierte Abfrage als Parameter.
Die Anforderung von Daten erhält zusätzlich eine Datenabbildung für die Definition des Kontexts.

Reports im Syncler-Focus basieren auf SQL und werden entsprechend der Benutzerangaben (Sortierung, Filter, Paging) aufbereitet übergeben.
Zusätzlich wird ein Count-Statement übergeben, welches die Gesamtanazhl an Datensätzen ermittelt.
Da dieser Anwendungsfall durch eine Benutzeroberfläche gesteuert wird, muss das Antwortverhalten optimiert werden.

Abfrage-Prozesse stellen keine Anforderungen an das Format. 
Platzhalter für Änderungsinformationen werden ggf. durch den Prozess ersetzt.

Folgende Platzhalter können genutzt werden.

* #Mandant#: frei verwendbarer globaler Wert
* #UserService#: aktuelles Benutzerkennzeichen aus Syncler-Focus
* #SourceId#: Kontext-ID aus dem aktuellen System. Wird per Datenabbildung bereitgestellt und muss ersetzt werden.
* #TargetId#: Kontext-ID aus dem anfragenden System. Wird per Datenabbildung bereitgestellt und muss ersetzt werden.
* #OpportunityId#: Kontext-ID aus dem anfragenden System. Wird per Datenabbildung bereitgestellt und muss ersetzt werden.
* #LastVersion#: Wird ggf. durch den Prozess ersetzt.
* #LastDatetime#: Wird ggf. durch den Prozess ersetzt.
* #FlowFilter#: Wird ggf. durch den Ablauf ersetzt.


