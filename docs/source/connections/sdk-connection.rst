Universal SDK
=============

Diese Verbindung stellt eine Entwicklungsplattform für die Anbindung von individuellen Systemen bereit.
Für die grundlegenden Funktionen einer Verbindungen können C# Skripte entwickelt werden, die dann
zur Ausführungszeit angewendet werden.
Dazu gehört das Erstellen eines Datenschemas, das Lesen von Daten, das Schreiben von Daten und das Ausführen
einer Abfrage.

Die Verbindung kann mit den Universalprozessen verwendet werden, es stehen aber auch SDK Prozesse zur Verfügung,
um auch an dieser Stelle zusätzlich Code einbringen zu können.

In einer On-premises Installation unterliegt die Ausführung von Skripten keiner Einschränkung.
In der Cloud wird die Speichernutzung und die Ausführungsdauer beschränkt.
Sollte das Skript die Limits überschreiten, wird es mit einer Fehlermeldung abgebrochen.

Die verfügbaren Bibliotheken sind identisch zur Transformation "C# Code Script".
Siehe :doc:`/api/sdk`

Funktionen
----------

:Schema ermitteln:

Das Schema wird von dem JSON Schema Skript generiert.
Die Vorlage für das Skript enthält eine Methode Execute, die beim Abrufen des Schemas ausgeführt wird,
und das Datenschema in JSON zurückgeben muss.
Das Skript muss ein JSON-Array mit JSON-Schemaobjekten zurückliefern (https://json-schema.org/). 
Für die Primärschlüssel fügen Sie bitte ein String-Array "uniqueidentifier" mit den Feldnamen hinzu (vgl. required).
Der Feldname für eine Aktualisierungsinformation wird mit der Eigenschaft "updated" definiert.

.. code-block:: json

    [
		{
			"title": "address",
			"properties": {
				"street": {
					"title": "Street",
					"type": "string",
					"maxLength": 60,
					"description": "Hint for user"
				},
				"housenumber": {
					"type": "integer",
					"title": "Housenumber"
				},
				"addressid": {
					"type": "integer",
					"title": "Record ID",
					"readOnly": true
				},
				"updateddate": {
					"title": "Updated at",
					"type": "string",
					"format": "date-time",
					"description": "Last updated date"
				},
				"country": {
					"title": "Land",
					"type": "string",
					"enum": [
						"DE",
						"AT",
						"CH"
					]
				},
				"geo": {
					"title": "Coordinates",
					"type": "object",
					"properties": {
						"lat": {
							"title": "Latitude",
							"type": "number"
						},
						"lng": {
							"title": "Longitude",
							"type": "number"
						}
					}
				}
			},
			"required": [
				"street"
			],
			"updated": "updateddate",
			"uniqueidentifier": [
				"addressid"
			]
		}
	]


:Lesen von Schema-basierten Daten:

Das Lesen von Schema-basierten Daten wird von dem JSON Daten lesen Skript implementiert.
Über die Helper-Bibliothek stehen alle Parameter der aktuellen Anfrage zur Verfügung.
Das aktuelle Schema ist in Helper.TargetObject zu finden.
Wenn die Seitenweise-Verarbeitung aktiviert ist, wird dieses Skript so oft ausgeführt, bis es keine Daten mehr
liefert. Die maximal Anzahl von Aufrufen ist auf 50 beschränkt.
Die aktuelle Seitennummer steht im Helper zur Verfügung.
Die Methode Execute muss ein Array von Objekten gemäß Datenschema in JSON zurückliefern.


:Lesen von Abfrage-basierten Daten:

Das Lesen von Schema-basierten Daten wird von dem JSON Abfrage Skript implementiert.
Das Verfahren ist weitestgehend identisch zum Lesen von Schema-basierten Daten.
Das Skript wird sowohl für die Erzeugung des Abfrage-Schema, als auch für die Abfrage selbst verwendet.
Eine Unterscheidung ist mittels Helper.GetParam<bool>("GetQuerySchema") möglich.


:Schreiben von Daten:

Das Schreiben von Daten wird von dem JSON Daten schreiben Skript implementiert.
Das aktuell zu schreibende Objekt wird in Helper.SetObject bereitgestellt.
Der Rückgabewert der Methode sollte das Objekt mit ggf. generierte ID oder aktuellem Änderungsdatum sein.
Diese beiden Informationen werden dann vom Prozess ausgewertet und z.B. für Datenabbildungen verwendet.


Einstellungen
-------------

Die Verbindung verfügt nur über wenig Parameter, da alles von den Skripten getragen wird.
Damit Zugangsdaten aber nicht sichtbar in den Skripten enthalten sein müssen, gibt es folgende
Werte, die dann in den Helper-Parametern zur Verfügung stehen.

:Authentifizierung URL:

Platzhalter für eine URL.

:Benutzername:

Platzhalter für einen Benutzernamen.

:Passwort:

Platzhalter für ein Passwort, welches besonders geschützt wird.
Das externe Auslesen oder Kopieren des Wertes wird nicht unterstützt.


Beispiele
---------

:Schema erzeugen:

.. code-block:: csscript

	using System;
	using System.Collections.Generic;
	using SIS;
	using SIS.PublicTypes;
	using Newtonsoft.Json.Linq;

	public class SalesViewerSchema
	{
		// SDK helper
		public SisHelper Helper { get; set; }

		// Your operation to return json data
		public string Execute()
		{
			JArray Response = new JArray();

			//Company
			JObject Company = new JObject();
			Company.Add("title", "company");
			Company.Add("properties", new JObject());
			Company.Add("uniqueidentifier", new JArray() { "id" });
			(Company["properties"] as JObject).Add("id", new JObject() { { "type", "string" }, { "title", "ID of company" } });
			(Company["properties"] as JObject).Add("name1", new JObject() { { "type", "string" }, { "title", "Name of company" } });
			(Company["properties"] as JObject).Add("email", new JObject() { { "type", "string" }, { "title", "E-Mail address of company" } });
			(Company["properties"] as JObject).Add("city", new JObject() { { "type", "string" }, { "title", "City of company" } });

			//Visit
			JObject Visit = new JObject();
			Visit.Add("title", "visit");
			Visit.Add("properties", new JObject());
			Visit.Add("updated", "lastActivityAt");
			Visit.Add("uniqueidentifier", new JArray() { "id" });
			(Visit["properties"] as JObject).Add("id", new JObject() { { "type", "integer" }, { "title", "ID of Session visit" } });
			(Visit["properties"] as JObject).Add("lastActivityAt", new JObject() { { "type", "string" }, { "format", "date-time" }, { "title", "Session visit last activity at" } });
			(Visit["properties"] as JObject).Add("url", new JObject() { { "type", "string" }, { "title", "URL of the session visit" } });

			Response.Add(Company);
			Response.Add(Visit);
			return Response.ToString();
		}
	}