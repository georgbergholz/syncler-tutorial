Der SDK Helper
==============

Der Helper ist in Skripten der Kommunikationsweg zur Anwendung und stellt darüberhinaus
unterstützende Funktionen zur Verfügung.
Parameter aus Verbindung und Prozessen können damit ausgetauscht werden.

Neben dem Helper und einigen .Net Basisfunktionen steht auch noch die Bibliothek Newtonsoft.Json zur
Verfügung, die vorallem das Lesen und Erzeugen von Json-Daten stark vereinfacht.

Alle Eigenschaften und Funktion des Helper beziehen sich immer auf die aktuelle Instanz.



:Helper.ClientID:

Your client id (string)

:Helper.ClientSecret:

Your client secret (string)

:Helper.Database:

Your database

:Helper.ServiceUrl:

Syncler service url (string)

:Helper.ServiceToken:

Your Syncler service token (string)

:Helper.ServiceExpireDate:

Your Syncler service expire date (DateTime)

:Helper.Proxy:

This connection proxy (WebProxy)

:Helper.Params:

Parameter list (List<SisParam>)

:Helper.IsCancelled:

Your cancel request (bool)

:Helper.ConnectionId:

This connection id (int)

:Helper.ProcessId:

This process id (int)

:Helper.ClientNumber:

Client number of process (int)

:Helper.WhereClause:

Where clause of process (string)

:Helper.ForceQueryAll:

Query all source records (bool)

:Helper.ConflictAction:

Conflict action from properties (string)

:Helper.ErrorAction:

Error action from properties (bool)

:Helper.ClientWhereClause:

Search query for existing records (string)

:Helper.DublettActionNoMatch:

Action for empty search result (string)

:Helper.DublettActionOneMatch:

Action for one record found (string)

:Helper.DublettActionMultipleMatches:

Action for multiple records found (string)

:Helper.SecondWhereClause:

Second where clause used after transformation (string)

:Helper.SourceObject:

This process source object name (string)

:Helper.TargetObject:

This process source object name (string)

:Helper.SourceType:

This process source connection type (string)

:Helper.TargetType:

This process target connection type (string)

:Helper.SourceSchemaObject:

This process source data schema (JObject)

:Helper.TargetSchemaObject:

This process target data schema (JObject)

:Helper.Statement:

This connection parsed query statement (string)

:Helper.Action:

This process action object (JObject)

:Helper.Page:

This connection reading page (int)

:Helper.SkipLoading:

This process skip default load methods (bool)

:Helper.InnerException:

This connection inner exception of set data (Exception)

:Helper.GetObject:

This process record source data object (JObject)

:Helper.SetObject:

This connection set data object

:Helper.Mappings:

Array of field mappings from properties (JArray)

:Helper.Database.Select(string SourceObject, string WhereClause, string OrderBy):

Your database select (DataTable)

:Helper.Database.ExecuteReader(string Statement):

Your database select (DataTable)

:Helper.Database.Insert(DataTable Data):

Your database insert (DataTable)

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

Message (string)")