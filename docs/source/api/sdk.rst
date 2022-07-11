Der SDK Helper
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
    Der Wert wird in den SDK Prozessen, der SDK Verbindung und der Transformation ausgewertet.

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
    In den SDK Prozessen wird der Wert zurück an den Prozess gegeben und kann damit die
    Prozessausführung direkt beeinflussen.

:Helper.ForceQueryAll (bool):

    Dies ist der Prozessparameter für die Aktivierung des kompletten Lesens ohne Änderungseinschränkung.    
    In den SDK Prozessen wird der Wert zurück an den Prozess gegeben und kann damit die
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
    In den SDK Prozessen wird der Wert zurück an den Prozess gegeben und kann damit die
    Prozessausführung direkt beeinflussen.

:Helper.SourceObject (string):

    Der aktuelle Quellobjekttyp in Prozessskripten.

:Helper.TargetObject (string):

    Der aktuelle Zielobjekttyp in Prozessskripten.
    In der SDK Verbindung definiert der Wert das aktuell angeforderte Objekt.

:Helper.SourceType (string):

    Der Typ der Quellverbindung in Prozessskripten.

:Helper.TargetType (string):

    Der Typ der Zielverbindung in Prozessskripten.

:Helper.SourceSchemaObject (JObject):

    Ein Schemaobjekt zur Beschreibung des aktuellen Quellobjekttyps.
    In der SDK Verbindung definiert der Wert das aktuell angeforderte Objekt.

:Helper.TargetSchemaObject (JObject):

    Ein Schemaobjekt zur Beschreibung des aktuellen Zielobjekttyps.

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
    In den SDK Prozessen führt der Wert true zum Überspringen des Lesens aus der Quelle.

:Helper.InnerException (Exception):

    Dieser Wert wird vom Datensatzskript in den SDK Prozessen verwendet.
    Er wird als Fehlermeldung in den Prozess gegeben, wenn das Ergebnis Failed lautet.
    In diesem Fall muss ein Wert zugewiesen sein.

:Helper.GetObject (JObject):

    In den SDK Prozessen wird hier der aktuelle Datensatz an das Datensatzskript übergeben.

:Helper.GetChildObjects (JArray):

    Im SDK Prozess für geschachtelte Daten enthält dieses Array die Liste der transformierten 
    Positionsdatensätze.
    Der Objektparameter "DELETE" führt je nach Verbindung zum Löschen der Position.

:Helper.SetObject (JObject):

    Dieses Objekt repräsentiert das aktuelle Zielobjekt.
    In den SDK Prozessen wird das Zielobjekt für das Datensatzskript übergeben.
    In der SDK Verbindung und dem JSON Daten schreiben Skript ist hier das Zielobjekt enthalten. 

:Helper.Mappings (JArray):

    Diese Liste enthält alle Feldzuordnungen, die im aktuellen Prozess definiert sind.
    In den SDK Prozessen werden Änderungen an dieser Liste für das Schreiben übernommen.
    Die Eigenschaften des einzelen Objektes sind SourcePath (string), SourceColumn (SchemaColumn),
    TargetPath (string) und TargetColumn (SchemaColumn). 


Methoden
--------

Folgende Methoden stehen im Helper direkt oder über Eigenschaften zur Verfügung.


:Helper.Cancel():

Fordert einen Abbruch der aktuellen Ausführung an.
Die Anforderung wird in SDK Prozessen, der SDK Verbindung und in Transformationen ausgewertet.


:Helper.SkipLoad():

Fordert das Überspringen der Lese-Operation an.
Die Anforderung wird in SDK Prozessen ausgewertet und überspringt das Lesen der Quelldaten.


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


:Helper.GetDataMappingList:

Parameter:

* string WhereClause
* string OrderBy
* int? MaxCount
* int? StartIndex

Rückgabewert: List\<SisDataMapping\>

Ruft eine Liste von Datenabbildungen aus der Datenbank des aktuellen Accounts über eine
Where-Bedingung ab. Die Abfrage kann auch mit Paging-Parametern ausgeführt werden.


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


:Helper.InvokeUrl:

Parameter:

* string Url
* string Method
* JObject Header
* string Data

Rückgabewert: string

Diese Methode für einen HTTP-Request aus und liefert die Antwort als Zeichenkette zurück.
Zusätzliche Header können als JObject übergeben werden. 
Einzelne Properties werden als einzelner Header-Parameter übernommen.








:Helper.GetParameterList(string WhereClause = null):

Get parameters from your database (List<SisParam>)

:Helper.SaveParameter(SisParam Parameter, string ConnectionId = null, string ProcessId = null):

Save parameter to your database

:Helper.DeleteParameter(int? ParameterId = null, string WhereClause):

Delete parameter from your database

:Helper.GetConnectionList(bool WithSchemaObjects = true, string WhereClause = null):

Get your connections (JArray)

:Helper.InvokeGetData(string ConnectionId, string TargetObject, List<SisParam> GetParams):

Invoke get data (JArray)

:Helper.InvokeSetData(string ConnectionId, string TargetObject, JObject JsonObject):

Invoke set data (JObject)


:Helper.ServiceCall(string Method, string Url, string Data):

Invoke Syncler service (string)

:Helper.InsertAction(int ProcessId, DateTime ExecuteDate, bool IsAdhoc, List<SisParam> ActionParams):

Save new process action to your database

:Helper.GetDataFromSource(string SchemaObjectName, List<SisParam> GetParams):

Get data from source connection (JArray)

:Helper.GetDataFromTarget(string SchemaObjectName, List<SisParam> GetParams):

Get data from target connection (JArray)

:Helper.GetDataFromConnection(string SchemaObjectName, List<SisParam> GetParams, int ConnectionId):

Get data from connection (JArray)

:Helper.SetDataToSource(string SchemaObjectName, JObject DataObject, List<SisParam> SetParams):

Set data to source connection (JObject)

:Helper.SetDataToTarget(string SchemaObjectName, JObject DataObject, List<SisParam> SetParams):

Set data to target connection (JObject)

:Helper.SetDataToConnection(string SchemaObjectName, JObject DataObject, List<SisParam> SetParams, int ConnectionId):

Set data to connection (JObject)

:Helper.FillByMappings(JObject SourceObject, JObject TargetObject, JArray Mappings (JObject):

Fill target object by source object and mappings (JObject)


:SisParam.Name:

Parameter name (string)

:SisParam.Value:

Parameter value (object)

:SisParam.ID:

Parameter ID (int). If taken from database.

:SisParam.GetValue():

Parameter value as string

:SisParam.GetValue<T>(DefaultValue):

Parameter value as type T or default

:SisParam.GetValueOrNull<T>():

Parameter value as type T or null

:SisParam.HasValue():

Parameter has value (bool)

:SisDataMapping.ID:

Database ID of data mapping (int)

:SisDataMapping.ProcessId:

Assigned process (int)

:SisDataMapping.Description:

Readable description (string)

:SisDataMapping.SourceRecordId:

ID or IDs of source record (string)

:SisDataMapping.TargetRecordId:

ID or IDs of target record (string)

:SisDataMapping.LastSyncDate:

Last access by sync (DateTime)

:SisDataMapping.TargetIsDeleted:

Target is missing or deleted (bool)

:SisDataMapping.LastSyncInfo:

List of parameters to store updated info (List<SisParam>)

:SisProcessInfo.ID:

Process id (int)

:SisProcessInfo.Name:

Process name (string)

:SisProcessInfo.DisplayName:

Full process name (string)

:SisProcessInfo.SourceObject:

Source object name (string)

:SisProcessInfo.TargetObject:

Target object name (string)

:SisProcessInfo.SourceConnectionId:

Source connection id (int)

:SisProcessInfo.TargetConnectionId:

Target connection id (int)

:SisProcessInfo.ClientNumber:

Client number (int)

:SisProcessInfo.IsScheduled:

Scheduling is active (bool)

:SisProcessInfo.SourceType:

Type of source connection (string)

:SisProcessInfo.TargetType:

Type of target connection (string)

:SisProcessInfo.ProcessType:

Type of process (string)

:SisLog.CreatedDate:

Created date (DateTime)

:SisLog.Level:

Level of message 0 (message) - 5 (debug) (int)

:SisLog.ProcessId:

Related process id (int)

:SisLog.ActionId:

Related queued action id (int)

:SisLog.RecordType:

Related record type (string)

:SisLog.RecordId:

Related record id (string)

:SisLog.LogMessage:

Message (string)