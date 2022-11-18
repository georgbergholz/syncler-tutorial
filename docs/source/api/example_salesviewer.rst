Anbindung SalesViewer API
=========================

Die API von SalesViewer (https://salesviewer.github.io/salesviewer-api/definition) verfügt nur über 
einen Endpunkt, der gebündelt 3 Informationen übermittelt, die Sitzung, der Besuch und die Firma.
In dieser geschachtelten Konstellation können die Daten durch die REST API Verbindung nicht einzeln 
ausgewertet werden.
Um die Daten voneinander zu trennen und als einzelne Objekte auslesbar zu machen,
kommt hier die SDK Verbindung zum Einsatz.
Folgende Skripte zeigen beispielhaft den Ansatz und die Funktionsweise.


:JSON Schema Skript:

Dieses Skript erzeugt ein fest definiertes Schema für die 3 Objekte.
Da die Daten nur über ein Änderungsdatum an der Session verfügen, wird dieser Wert an die anderen
Objekte kopiert. Damit ist auch hier eine Abfrage nach Änderungen indirekt möglich.


.. code-block:: C#

    using SIS;
    using Newtonsoft.Json.Linq;

    public class SalesViewerSchema
    {
        // SDK-Helper
        public SisHelper Helper { get; set; }

        // Your operation to return json data
        public string Execute()
        {
            //Company Schema
            JObject Company = new JObject();
            Company.Add("title", "company");
            Company.Add("uniqueidentifier", new JArray() { "id" });

            //Company Eigenschaften
            JObject CompanyProperties = new JObject();
            Company.Add("properties", CompanyProperties);

            CompanyProperties.Add("id", new JObject() { { "type", "string" }, { "title", "ID of company" } });
            CompanyProperties.Add("name", new JObject() { { "type", "string" }, { "title", "Name of company" } });
            CompanyProperties.Add("city", new JObject() { { "type", "string" }, { "title", "City of company" } });
            CompanyProperties.Add("zip", new JObject() { { "type", "string" }, { "title", "Zip Code of company" } });
            CompanyProperties.Add("street", new JObject() { { "type", "string" }, { "title", "Street of company" } });
            CompanyProperties.Add("phone", new JObject() { { "type", "string" }, { "title", "Phone Number of company" } });
            CompanyProperties.Add("email", new JObject() { { "type", "string" }, { "title", "E-Mail address of company" } });
            CompanyProperties.Add("url", new JObject() { { "type", "string" }, { "title", "URL of website" } });
            CompanyProperties.Add("countryCode", new JObject() { { "type", "string" }, { "title", "Country Code" } });
            CompanyProperties.Add("isCustomer", new JObject() { { "type", "boolean" }, { "title", "IsCustomer" } });
            CompanyProperties.Add("lastActivityAt", new JObject() { { "type", "string" }, { "format", "date-time" }, { "title", "Session company last activity at" } });

            CompanyProperties.Add("sector", new JObject() { { "type", "object" }, { "title", "Sector" }, { "properties", new JObject(){
                { "id", new JObject(){ { "type", "string" }, { "title", "ID" } } },
                { "name", new JObject(){ { "type", "string" }, { "title", "Name" } } }
            } }});

            //Änderungsdatum
            Company.Add("updated", "lastActivityAt");

            //Visit Schema
            JObject Visit = new JObject();
            Visit.Add("title", "visit");
            Visit.Add("uniqueidentifier", new JArray() { "id" });

            //Visit Eigenschaften
            JObject VisitProperties = new JObject();
            Visit.Add("properties", VisitProperties);

            VisitProperties.Add("id", new JObject() { { "type", "integer" }, { "title", "ID of Session visit" } });
            VisitProperties.Add("sessionGuid", new JObject() { { "type", "string" }, { "title", "GUID of Session" } });
            VisitProperties.Add("startedAt", new JObject() { { "type", "string" }, { "format", "date-time" }, { "title", "Session visit started at" } });
            VisitProperties.Add("lastActivityAt", new JObject() { { "type", "string" }, { "format", "date-time" }, { "title", "Session visit last activity at" } });
            VisitProperties.Add("url", new JObject() { { "type", "string" }, { "title", "URL of the session visit" } });
            VisitProperties.Add("referer", new JObject() { { "type", "string" }, { "title", "Referer" } });

            //Änderungsdatum
            Visit.Add("updated", "lastActivityAt");

            //Session
            JObject Session = new JObject();
            Session.Add("title", "session");
            Session.Add("uniqueidentifier", new JArray() { "guid" });

            //Session Eigenschaften
            JObject SessionProperties = new JObject();
            Session.Add("properties", SessionProperties);

            SessionProperties.Add("guid", new JObject() { { "type", "string" }, { "title", "GUID of Session" } });
            SessionProperties.Add("companyID", new JObject() { { "type", "string" }, { "title", "ID of the company" } });
            SessionProperties.Add("startedAt", new JObject() { { "type", "string" }, { "format", "date-time" }, { "title", "Session visit started at" } });
            SessionProperties.Add("lastActivityAt", new JObject() { { "type", "string" }, { "format", "date-time" }, { "title", "Session visit last activity at" } });
            SessionProperties.Add("referer", new JObject() { { "type", "object" }, { "title", "Referer" }, { "properties", new JObject(){
                { "url", new JObject(){ { "type", "string" }, { "title", "URL" } } },
                { "medium", new JObject(){ { "type", "string" }, { "title", "Medium" } } },
                { "source", new JObject(){ { "type", "string" }, { "title", "Source" } } },
                { "term", new JObject(){ { "type", "string" }, { "title", "Term" } } }
            } }});
            SessionProperties.Add("campaign", new JObject() { { "type", "boolean" }, { "title", "Campaign" } });

            //Änderungsdatum
            Session.Add("updated", "lastActivityAt");

            JArray Response = new JArray
            {
                Company,
                Visit,
                Session
            };

            return Response.ToString();
        }
    }

:JSON Daten lesen Skript:

Dieses Skript liest Daten aus der SalesViewer API.
Dabei findet eine Unterscheidung nach dem angeforderten Objekttyp statt.
Außerdem wird die API in Pages abgefragt und bei Bedarf mit einem Änderungsdatum weiter eingeschränkt.
Das Besondere bei diesem Skript ist die Prüfung auf Duplikate in den Firmendaten.
Technisch ist die Company der Session untergeordnet und kann deshalb mehrfach auftreten.
Um dies in einer Anforderung zu unterbinden, wird eine Liste von bereits erhaltenen Firmen-IDs geführt.
Durch das Paging wird dieses Skript mehrfach je Seite aufgerufen und jede lokale Variable würde ihren
Wert verlieren. Um Daten über Pages hinweg verfügbar zu haben, wird die Liste als Parameter im Helper-Objekt
speichert. Diese bleibt bei jedem Aufruf innerhalb einer Anforderung durch einen Prozess identisch.

.. code-block:: C#

    using System;
    using SIS;
    using Newtonsoft.Json.Linq;
    using System.Collections.Generic;

    public class SalesViewerGetData
    {
        // SDK-Helper
        public SisHelper Helper { get; set; }

        // Your operation to return json data
        public string Execute()
        {
            JArray Result = new JArray();

            //Url definieren
            string API_Key = "";
            string Url = "https://www.salesviewer.com/api/sessions.json?apiKey=" + API_Key;

            //Abfrage enthält Änderungsanforderung
            if (!string.IsNullOrEmpty(Helper.GetParam("GETDATA_MODIFIED")))
                Url += "&from=" + Helper.GetParam<DateTime>("GETDATA_MODIFIED").ToString("yyyy-MM-dd HH:mm:ss");

            //Helper übergibt Page-Number
            Url += "&page=" + Helper.Page;
            Url += "&pageSize=50";

            //Service abrufen
            string ServiceResponse = Helper.InvokeUrl(Url, "GET", null, null);

            if (!string.IsNullOrEmpty(ServiceResponse))
            {
                JObject ResponseObject = JObject.Parse(ServiceResponse);

                foreach (JObject SessionObject in ResponseObject["result"] as JArray)
                {
                    //Firma wurde angefordert
                    if (Helper.TargetObject == "company")
                    {
                        if (SessionObject.ContainsKey("company"))
                        {
                            //Firma kann mehrfach enthalten sein. Duplikate sollen über Pages hinweg vermieden werden. Helper bietet übergreifenden Storage
                            if (string.IsNullOrEmpty(Helper.GetParam("COMPANY_ID")))
                                Helper.SetParam("COMPANY_ID", new List<string>());

                            var CompanyIdList = Helper.GetParam("COMPANY_ID", new List<string>());

                            JObject Company = SessionObject["company"] as JObject;
                            string CompanyId = Company["id"].ToString();

                            if (!CompanyIdList.Contains(CompanyId))
                            {
                                string lastActivityAt = SessionObject["lastActivityAt"].ToString();
                                Company.Add("lastActivityAt", lastActivityAt);
                                Result.Add(Company);

                                CompanyIdList.Add(CompanyId);
                            }
                        }
                    }

                    //Visit wurde angefordert
                    if (Helper.TargetObject == "visit")
                    {
                        if (SessionObject.ContainsKey("visits"))
                        {
                            string SessionGuid = SessionObject["guid"].ToString();
                            JArray VisitArray = SessionObject["visits"] as JArray;

                            foreach (JObject Visit in VisitArray)
                            {
                                Visit.Add("sessionGuid", SessionGuid);

                                string lastActivityAt = SessionObject["lastActivityAt"].ToString();
                                Visit.Add("lastActivityAt", lastActivityAt);

                                Result.Add(Visit);
                            }
                        }
                    }

                    //Session wurde angefordert
                    if (Helper.TargetObject == "session")
                    {
                        string CompanyId = (SessionObject["company"] as JObject)["id"].ToString();
                    
                        JObject ResultSessionObject = new JObject(SessionObject);
                        //CompanyId aus Unterobjekt kopieren
                        ResultSessionObject.Add("companyID", CompanyId);

                        //überflüssige Daten entfernen
                        ResultSessionObject.Remove("company");
                        ResultSessionObject.Remove("visits");
                        ResultSessionObject.Remove("interests");
                    
                        Result.Add(ResultSessionObject);
                    }
                }
            }

            return Result.ToString();
        }
    }