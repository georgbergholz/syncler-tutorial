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

:Helper.ClientID (string): 

    Die Client ID des Account, welche z.B. für die Anmeldung an der API erforderlich ist.
    Wird von der Methode ServiceCall verwendet.

:Helper.ClientSecret (string):

    Der Geheimschlüssel des Account, welche z.B. für die Anmeldung an der API erforderlich ist.
    Wird von der Methode ServiceCall verwendet.

:Helper.Database (SQL Client):

    Ein Datenbank-Client für die Datenbank des Accounts. Ein direkter Zugriff ist nicht erforderlich.
    Wird von den Funktionen des Helpers verwendet.

:Helper.ServiceUrl (string):

    Die Url der Syncler API, mit der das Skript diese Aufrufen kann.
    Wird von den Methoden ServiceCall, InvokeGetData und InvokeSetData verwendet.

:Helper.ServiceToken (string):

    Der Access-Token der Syncler API.
    Wird z.B. von der Methode ServiceCall verwendet.

:Helper.ServiceExpireDate (DateTime):

    Das Gültigkeitsdatum des Access-Token der Syncler API.
    Wird von der Methode ServiceCall verwendet.

:Helper.Params (List SisParam):

    Liste von generischen Parametern aus Name und Wert.
    Wird von den Die Methoden GetParam und SetParam verwendet.
    Initial wird diese Liste mit Parametern aus dem Prozess, der Anforderung und der Verbindung gefüllt.

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

:Helper.Database.Select:

Parameter:
- string SourceObject
- string WhereClause
- string OrderBy

Rückgabewert: DataTable

Für eine Select-Anweisung auf der Datenbank des aktuellen Accounts aus.


:Helper.Database.ExecuteReader:

Parameter:
- string Statement

Rückgabewert: DataTable

Für ein Select-Statement auf der Datenbank des aktuellen Accounts aus.


:Helper.Database.Insert:

Parameter:
- DataTable Data

Rückgabewert: DataTable

Speichert die Daten in der Datenbank des aktuellen Accounts.
Die Antwort enthält auch generierte ID-Werte.


:Helper.Database.Delete(string TableName, string WhereClause):

Your database delete (int)

:Helper.Database.Update(DataTable Data, string WhereClause):

Your database update

:Helper.Cancel():

Cancel after execute

:Helper.SkipLoad():

Skip process default load methods

:Helper.GetParam(string Name):

Get parameter value as string by name from list

:Helper.GetParam<T>(string Name, T DefaultValue = default):

Get parameter value as type T or default by name from list

:Helper.GetParamOrNull<T>(string Name):

Get parameter value as type T or null by name from list

                
:Helper.SetParam(string Name, string Value):

Update or insert parameter to list

:Helper.SetParam<T>(string Name, T Value):

Update or insert parameter with value type T to list

:Helper.GetDataMappingBySourceId(int ProcessId, string SourceId):

Get data mapping by process and source id (SisDataMapping)

:Helper.GetDataMappingByTargetId(int ProcessId, string TargetId):

Get data mapping by process and target id (SisDataMapping)

:Helper.GetDataMappingList(string WhereClause, string OrderBy, int? MaxCount, int? StartIndex):

Get data mapping list by query (List<SisDataMapping>)

:Helper.GetDataMappingComplementaryBySourceId(int ProcessId, string SourceId, string TargetObject = null):

Get data mapping for complementary process by this process and this source id (List<SisDataMapping>)

:Helper.GetDataMappingParallelByTargetId(int ProcessId, string TargetId):

Get data mapping for parallel process by this process and this source id (List<SisDataMapping>)

:Helper.SaveDataMapping(SisDataMapping Mapping):

Insert or update data mapping (SisDataMapping)

:Helper.IncreaseOwnDataMapping(SisDataMapping DataMapping, object NewUpdatedInfoA, object NewUpdatedInfoB, bool OnlyA = false, bool OnlyB = false):

Increase own updated info

:Helper.IncreaseComplementaryMappings(string CurrentSourceId, string CurrentTargetId, object NewUpdatedInfoA, object NewUpdatedInfoB, bool OnlyA = false, bool OnlyB = false):

Increase complementary updated info

:Helper.IncreaseParallelMappings(string CurrentSourceId, string CurrentTargetId, object NewUpdatedInfoA, object NewUpdatedInfoB, bool OnlyA = false, bool OnlyB = false):

Increase parallel updated info

:Helper.GetProcessInfoList(int? SourceConnectionId = null, int? TargetConnectionId = null):

Your processes (List<SisProcessInfo>)

:Helper.GetProcessInfoComplementary(int ProcessId):

Your complemtary processes (List<SisProcessInfo>)

:Helper.GetProcessInfoParallel(int ProcessId):

Your parallel processes (List<SisProcessInfo>)

:Helper.InsertLog(SisLog Log):

Save log to your database

:Helper.InsertLog(string Message, int Level):

Save simple log to your database

:Helper.InvokeUrl(string Url, string Method, JObject Header, string Data)):

Invoke url (string)

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

:Helper.ServiceLogin():

Syncler service login (bool)

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