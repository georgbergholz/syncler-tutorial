Der SDK-Helper
==============

Der Helper ist in Skripten der Kommunikationsweg zur Anwendung und stellt darüberhinaus
unterstützende Funktionen zur Verfügung.
Parameter aus Verbindung und Prozessen können damit ausgetauscht werden.

Neben dem Helper und einigen .Net Basisfunktionen steht auch noch die Bibliothek Newtonsoft.Json zur
Verfügung, die vorallem das Lesen und Erzeugen von Json-Daten stark vereinfacht.

Alle Eigenschaften und Funktion des Helper beziehen sich immer auf den aktuellen Account.

Eigenschaften
-------------

Folgende Eigenschaften stehen am Helper zur Verfügung.
Einige werden nur intern vom Helper genutzt oder indirekt über Methoden gesetzt.

:Helper.IsCancelled (bool):

Die Wert zeigt an, dass das Skript einen Abbruch angefordert hat.
Der Wert wird auch mit der Methode Cancel gesetzt.
Der Wert wird in den SDK-Prozessen, der SDK-Verbindung und der Transformation ausgewertet.

:Helper.ConnectionId (int):

Die ID der aktuellen Verbindung.
Dieser Wert kann für API-Aufrufe verwendet werden.

:Helper.ProcessId (int):

Die ID des aktuellen Prozesses.
Dieser Wert kann für API-Aufrufe verwendet werden.
Wird von den Methoden IncreaseComplementaryMappings, IncreaseParallelMappings und InsertLog verwendet.

:Helper.ClientNumber (int):

Die Client-Number des aktuellen Prozesses.
Dies ist ein Prozessparameter, der für die Datenstrukturierung genutzt werden kann.
Die Methoden GetDataMappingComplementaryBySourceId und GetDataMappingParallelByTargetId schränken
das Ergebnis mit diesem Wert ein, realisieren das aber mittels Abfrage direkt.

:Helper.WhereClause (string):

Dies ist der Prozess-Filter für die Abfrage von Quelldaten.
In den SDK-Prozessen wird der Wert zurück an den Prozess gegeben und kann damit die
Prozessausführung direkt beeinflussen.

:Helper.ForceQueryAll (bool):

Dies ist der Prozessparameter für die Aktivierung des kompletten Lesens ohne Änderungseinschränkung.    
In den SDK-Prozessen wird der Wert zurück an den Prozess gegeben und kann damit die
Prozessausführung direkt beeinflussen.

:Helper.ConflictAction (string):

Dies ist der Prozessparameter für die Behandlung von Konflikten.
Die möglichen Werte sind USE_SOURCE, USE_TARGET, SKIP, IGNORE und SOURCE_CHANGES.

:Helper.ErrorAction (string):

Dies ist der Prozessparameter für die Behandlung von Fehlern.
Die möglichen Werte sind REPEAT_ALL, REPEAT_DIFFERENCES, QUERY_NEXT, IGNORE und STOP.

:Helper.ClientWhereClause (string):

Dies ist der Prozessparameter für die Suche nach Übereinstimmungen bei unbekannten Datensätzen.

:Helper.DublettActionNoMatch (string):

Dies ist der Prozessparameter für die Behandlung von keinem Treffer bei der Übereinstimmungssuche.
Die möglichen Werte sind SKIP, SKIP_WITH_WARNING, WRITE, REPEAT und REPEAT_WRITE.

:Helper.DublettActionOneMatch (string):

Dies ist der Prozessparameter für die Behandlung von einem Treffer bei der Übereinstimmungssuche.
Die möglichen Werte sind SKIP, SKIP_WITH_WARNING, MAPPING_ONLY, MAPPING_AND_SYNCH und WRITE_NEW.

:Helper.DublettActionMultipleMatches (string):

Dies ist der Prozessparameter für die Behandlung von mehreren Treffern bei der Übereinstimmungssuche.
Die möglichen Werte sind SKIP, SKIP_WITH_WARNING, MAPPING_ONLY_FIRST, MAPPING_AND_SYNCH_FIRST und 
WRITE_NEW.

:Helper.SecondWhereClause (string):

Dies ist der Prozess-Zweitfilter für die Auswahl von transformierten Quelldaten.
In den SDK-Prozessen wird der Wert zurück an den Prozess gegeben und kann damit die
Prozessausführung direkt beeinflussen.

:Helper.SourceObject (string):

Der aktuelle Quellobjekttyp in Prozessskripten.

:Helper.TargetObject (string):

Der aktuelle Zielobjekttyp in Prozessskripten.
In der SDK-Verbindung definiert der Wert das aktuell angeforderte Objekt.

:Helper.SourceType (string):

Der Typ der Quellverbindung in Prozessskripten.

:Helper.TargetType (string):

Der Typ der Zielverbindung in Prozessskripten.

:Helper.SourceSchemaObject (JObject):

Ein Schemaobjekt zur Beschreibung des aktuellen Quellobjekttyps.

:Helper.TargetSchemaObject (JObject):

Ein Schemaobjekt zur Beschreibung des aktuellen Zielobjekttyps.
In der SDK-Verbindung definiert der Wert das aktuell angeforderte Objekt.

:Helper.Statement (string):

Die Abfrage der aktuellen Abfrageanforderung.
Dies wird in JSON Abfrage Skript übergeben. 

:Helper.Action (JObject):

Dieses Objekt beschreibt die aktuellen Ausführungsparameter.

:Helper.Page (int):

Dieser Wert wird beim Lesen mit Paging mit jeder Ausführung erhöht.
Der Startwert ist 0.

:Helper.SkipLoading (bool):

Dieser Wert wird von der Methode SkipLoad gesetzt.
In den SDK-Prozessen führt der Wert true zum Überspringen des Lesens aus der Quelle.

:Helper.InnerException (string):

Dieser Wert wird vom Datensatzskript in den SDK-Prozessen verwendet.
Er wird als Fehlermeldung in den Prozess gegeben, wenn das Ergebnis Failed lautet.
In diesem Fall muss ein Wert zugewiesen sein.

:Helper.GetObject (JObject):

In den SDK-Prozessen wird hier der aktuelle Datensatz an das Datensatzskript übergeben.

:Helper.GetChildObjects (JArray):

Im SDK-Prozess für geschachtelte Daten enthält dieses Array die Liste der transformierten 
Positionsdatensätze.
Der Objektparameter "DELETE" führt je nach Verbindung zum Löschen der Position.

:Helper.SetObject (JObject):

Dieses Objekt repräsentiert das aktuelle Zielobjekt.
In den SDK-Prozessen wird das Zielobjekt für das Datensatzskript übergeben.
In der SDK-Verbindung und dem JSON-Daten schreiben Skript ist hier das Zielobjekt enthalten. 

:Helper.SetObject (JObject):

Dieses Objekt repräsentiert die Änderungen des aktuellen Zielobjektes und steht in der SDK-Verbindung zur Verfügung.
Sobald der Datensatz über einen Primärschlüssel verfügt können so die tatsächlichen Änderungen in den Daten ermittelt werden.

:Helper.Mappings (JArray):

Diese Liste enthält alle Feldzuordnungen, die im aktuellen Prozess definiert sind.
In den SDK-Prozessen werden Änderungen an dieser Liste für das Schreiben übernommen.
Die Eigenschaften des einzelen Objektes sind SourcePath (string), SourceColumn (SchemaColumn),
TargetPath (string) und TargetColumn (SchemaColumn). 


Methoden
--------

Folgende Methoden stehen im Helper direkt oder über Eigenschaften zur Verfügung.


:Helper.Cancel():

Fordert einen Abbruch der aktuellen Ausführung an.
Die Anforderung wird in SDK-Prozessen, der SDK-Verbindung und in Transformationen ausgewertet.


:Helper.SkipLoad():

Fordert das Überspringen der Lese-Operation an.
Die Anforderung wird in SDK-Prozessen ausgewertet und überspringt das Lesen der Quelldaten.


:Helper.GetParam:

Parameter:

* string Name

Rückgabewert: string

Liefert einen Parameterwert aus der Parameterliste über den Namen des Parameters.
Wenn der Parameter nicht vorhanden ist, wird eine leere Zeichenkette zurückgeliefert.


:Helper.GetParam\<T\>:

Parameter:

* string Name
* T DefaultValue = default

Rückgabewert: T

Liefert einen Parameterwert aus der Parameterliste über den Namen des Parameter in einem bestimmten Typ.
Wenn der Parameter nicht vorhanden ist, wird der DefaultValue verwendet.
Die Typangabe kann bei einem typisierten Defaultvalue auch weggelassen werden.
Abhängig vom Typ des Parameters wird der Wert oder Verweis geliefert.


:Helper.GetParamOrNull\<T\>:

Parameter:

* string Name

Rückgabewert: T

Liefert einen Parameterwert aus der Parameterliste über den Namen des Parameter in einem bestimmten Typ.
Wenn der Parameter nicht vorhanden ist, wird Null verwendet.
Diese Notation kann für explizites Nullable verwendet werden. z.B. DateTime?


:Helper.SetParam\<T\>:

Parameter:

* string Name
* T Value

Speichert einen Parameter in der Parameterliste. Sollte der Parameter bereits vorhanden sein, wird der Wert
aktualisiert.
Die Typangabe kann bei typisierten Value auch weggelassen werden.


:Helper.FieldStringToColumnObject:

Parameter:

* string FieldString

Rückgabewert: JObject

Mit dieser Methode kann eine Zeichenkette, z.B. aus einem Filter, die in Feldnotation übergeben wird, in ein JObject mit ansprechbaren Eigenschaften umgewandelt werden.


:Helper.GetDataMappingBySourceId:

Parameter:

* int ProcessId
* string SourceId

Rückgabewert: SisDataMapping

Ruft eine Datenabbildung aus der Datenbank des aktuellen Accounts über die Quell-ID ab.
Datenabbildungen sind Prozess-bezogen und enthalten eine Quell- und Ziel-Identifikation.


:Helper.GetDataMappingByTargetId:

Parameter:

* int ProcessId
* string TargetId

Rückgabewert: SisDataMapping

Ruft eine Datenabbildung aus der Datenbank des aktuellen Accounts über die Ziel-ID ab.
Datenabbildungen sind Prozess-bezogen und enthalten eine Quell- und Ziel-Identifikation.


:Helper.GetDataMappingComplementaryBySourceId:

Parameter:

* int ProcessId
* string SourceId
* string TargetObject = null

Rückgabewert: List\<SisDataMapping\>

Ruft eine Liste von Datenabbildungen entgegengerichteter Prozesse zum aktuellen Prozess aus der Datenbank 
des aktuellen Accounts über eine Quell-ID ab. Zusätzlich kann das Target-Objekt eingeschränkt werden. 
Dies kann erforderlich sein, wenn zwei unterschiedliche Objekte das gleiche Zielobjekt haben.
Die Arbeit mit komplementären Datenabbildungen ist für das Konfliktmanagement und die Zielerkennung bei
bidirektionalen Synchronisationen relevant.


:Helper.GetDataMappingParallelByTargetId:

Parameter:

* int ProcessId
* string TargetId

Rückgabewert: List\<SisDataMapping\>

Ruft eine Liste von Datenabbildungen paralleler Prozesse zum aktuellen Prozess aus der Datenbank 
des aktuellen Accounts über eine Ziel-ID ab. 
An diesen muss die Änderungsinformation des Ziels angepasst werden, da dort ansonsten ein Konflikt
erkannt wird.


:Helper.SaveDataMapping:

Parameter:

* SisDataMapping Mapping

Rückgabewert: SisDataMapping

Speichert eine neue oder aktualisiert eine bestehende Datenabbildung.


:Helper.IncreaseOwnDataMapping:

Parameter:

* SisDataMapping DataMapping
* object NewUpdatedInfoA
* object NewUpdatedInfoB
* bool OnlyA = false
* bool OnlyB = false

Diese Methode aktualisiert die Änderungsinformation von Quelle und Ziel für die aktuelle Datenabbildung.
Zum Auflösen eines Konflikts können die einzelnen Informationen gezielt per Parameter aktualisiert werden.


:Helper.IncreaseComplementaryMappings:

Parameter:

* string CurrentSourceId
* string CurrentTargetId
* object NewUpdatedInfoA
* object NewUpdatedInfoB
* bool OnlyA = false
* bool OnlyB = false

Diese Methode sucht und aktualisiert oder legt komplementäre Datenabbildungen an.
Bei Neuanlagen oder in Konfliktsituationen kann dies auch nur partiell erfolgen.


:Helper.IncreaseParallelMappings:

Parameter:

* string CurrentSourceId
* string CurrentTargetId
* object NewUpdatedInfoA
* object NewUpdatedInfoB
* bool OnlyA = false
* bool OnlyB = false

Diese Methode sucht und aktualisiert oder legt parallele Datenabbildungen an.
Bei Konfliktsituationen kann dies auch nur partiell erfolgen.


:Helper.GetProcessInfoList:

Parameter:

* int? SourceConnectionId = null
* int? TargetConnectionId = null

Rückgabewert: List\<SisProcessInfo\>

Liefert eine Liste von Informationsobjekten zu den Prozessen des aktuellen Accounts.
Die Abfrage kann auf bestimmte Verbindungen eingeschränkt werden.


:Helper.GetProcessInfoComplementary:

Parameter:

* int ProcessId

Rückgabewert: List\<SisProcessInfo\>

Liefert eine Liste von Informationsobjekten zu den komplementären Prozessen einen Prozesses.


:Helper.GetProcessInfoParallel:

Parameter:

* int ProcessId

Rückgabewert: List\<SisProcessInfo\>

Liefert eine Liste von Informationsobjekten zu den parallelen Prozessen einen Prozesses.


:Helper.InsertLog:

Parameter:

* SisLog Log

Speichert einen Protokolleintrag in der Datenbank des aktuellen Accounts.


:Helper.InsertLog:

Parameter:

* string Message
* int Level

Speichert einen Protokolleintrag in der Datenbank des aktuellen Accounts.
Mit dem Level wird der Typ des Eintrags festgelegt. 
0 = Meldung, 1 = Fehler, 2 = Warnung, 3 = Nachricht, 4 = Rückmeldung, 5 = Debug


:Helper.InsertMessage:

Parameter:

* string Message
* int Level

Speichert eine Nachricht in der Broadcast-Datenbank des aktuellen Accounts.
Diese Nachrichten werden in der Benutzeroberfläche angezeigt, aber nicht dauerhaft vorgehalten.
Mit dem Level wird der Typ des Eintrags festgelegt. 
0 = Meldung, 1 = Fehler, 2 = Warnung, 3 = Nachricht, 4 = Rückmeldung, 5 = Debug


:Helper.InvokeUrl:

Parameter:

* string Url
* string Method
* JObject Header
* string Data
* bool Base64 (default: false)

Rückgabewert: string

Diese Methode führt einen HTTP-Request aus und liefert die Antwort als Zeichenkette zurück.
Zusätzliche Header können als JObject übergeben werden. 
Einzelne Properties werden als einzelner Header-Parameter übernommen.
Mit dem Parameter Base64 werden die abgerufenen Daten binär in Base64 konvertiert und zurückgegeben.


:Helper.GetParameterList:

Parameter:

* string Name
* string ConnectionId = null
* string ProcessId = null

Rückgabewert: List\<SisParam\>

Ruft eine Parameterliste aus der internen Datenbank ab.
Jeder Parameter hat einen Namen, einen Wert und eine ID.
Zusätzlich können Parameter noch einer Verbindung oder einem Prozess zugeordnet werden.
Das ist für die Strukturierung und Bereinigung sinnvoll.


:Helper.SaveParameter:

Parameter:

* SisParam Parameter
* string ConnectionId = null
* string ProcessId = null

Speichert einen Parameter in der internen Datenbank.


:Helper.DeleteParameter:

Parameter:

* int ParameterId

Löscht einen Parameter aus der internen Datenbank.


:Helper.InvokeGetData:

Parameter:

* string ConnectionId
* string TargetObject
* List\<SisParam\> GetParams

Rückgabewert: JArray

Ruft Daten aus einer Verbindung ab.
Das Schemaobjekt wird über TargetObject festgelegt.
Die Liste der Parameter steuert die Abfrage. Dabei unterstützen nicht alle Verbindungen den gleichen Umfang an Optionen.
Übliche Namen von Parametern sind: GETDATA_ID, GETDATA_RELATED_ID, GETDATA_RELATED, GETDATA_WHERE, GETDATA_MODIFIED, GETDATA_ORDER, LAST_SYNC_DATE, LAST_SYNC_VERSION
Die Ausführung erfolgt über die Syncler API.


:Helper.InvokeSetData:

Parameter:

* string ConnectionId
* string TargetObject
* JObject JsonObject

Rückgabewert: JObject

Speichert Daten über eine Verbindung.
Das Schemaobjekt wird über TargetObject festgelegt.
Zusätzliche Parameter, wie "DELETE" (bool) können über die Eigenschaft "Params" am JsonObjekt mitgegeben werden.


:Helper.ServiceCall:

Parameter:

* string Method
* string Url
* string Data

Rückgabewert: string

Führt einen Aufruf der Syncler API aus.
Als Url muss nur der Endpunkt übergeben werden.


:Helper.InsertAction:

Parameter:

* int ProcessId
* DateTime ExecuteDate
* bool IsAdhoc
* List\<SisParam\> ActionParams

Speichert einen neuen Warteschlangeneintrag für einen Prozess.


Parameter
---------

:SisParam.Name:

Parameter Name (string)

:SisParam.Value:

Parameter Wert (object)

:SisParam.ID:

Parameter ID (int)
Wird beim Speichern in der Datenbank gesetzt.

:SisParam.GetValue():

Parameter Wert als String

:SisParam.GetValue\<T\>(DefaultValue):

Parameter Wert als Typ T oder Default

:SisParam.GetValueOrNull\<T\>():

Parameter Wert als Typ T oder Null

:SisParam.HasValue():

Parameter hat einen Wert (bool)


Datenabbildung
--------------

:SisDataMapping.ID:

Interne Datenbank ID (int)

:SisDataMapping.ProcessId:

Zugeordneter Prozess (int)

:SisDataMapping.Description:

Datensatzbeschreibung (string)

:SisDataMapping.SourceRecordId:

ID des Quelldatensatzes (string)

:SisDataMapping.TargetRecordId:

ID des Zieldatensatzes (string)

:SisDataMapping.LastSyncDate:

Letztes Datum der Synchronisation (DateTime)

:SisDataMapping.TargetIsDeleted:

Zieldatensatz wurde gelöscht (bool)

:SisDataMapping.LastSyncInfo:

Parameterliste mit Änderungs- und Zusatzinformationen (List\<SisParam\>)


Prozessbeschreibung
-------------------

:SisProcessInfo.ID:

Prozess ID (int)

:SisProcessInfo.Name:

Prozessname (string)

:SisProcessInfo.DisplayName:

Voller Prozessname (string)

:SisProcessInfo.SourceObject:

Names des Quelldatensatzes (string)

:SisProcessInfo.TargetObject:

Name des Zieldatensatzes (string)

:SisProcessInfo.SourceConnectionId:

Quellverbindung ID (int)

:SisProcessInfo.TargetConnectionId:

Zielverbindung ID (int)

:SisProcessInfo.ClientNumber:

Mandantennummer (int)

:SisProcessInfo.IsScheduled:

Zeitsteuerung ist aktiv (bool)

:SisProcessInfo.SourceType:

Typ der Quellverbindung (string)

:SisProcessInfo.TargetType:

Typ der Zielverbindung (string)

:SisProcessInfo.ProcessType:

Typ des Prozesses (string)


Protokoll
---------

:SisLog.CreatedDate:

Erstelldatum (DateTime)

:SisLog.Level:

Level der Nachricht 0 (message) - 5 (debug) (int)

:SisLog.ProcessId:

Zugeordneter Prozess (int)

:SisLog.ActionId:

Zugeordneter Warteschlangeneintrag (int)

:SisLog.RecordType:

Names des Datensatzes (string)

:SisLog.RecordId:

ID des Datensatzes (string)

:SisLog.LogMessage:

Meldung (string)