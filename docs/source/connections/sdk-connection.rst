﻿Universal-SDK-Verbindung
========================

Diese Verbindung stellt eine Entwicklungsplattform für die Anbindung von individuellen Systemen bereit.
Für die grundlegenden Funktionen einer Verbindungen können C# Skripte entwickelt werden, die dann
zur Ausführungszeit angewendet werden.
Dazu gehört das Erstellen eines Datenschemas, das Lesen von Daten, das Schreiben von Daten und das Ausführen
einer Abfrage.

Die Verbindung kann mit den Universalprozessen verwendet werden, es stehen aber auch SDK-Prozesse zur Verfügung,
um auch an dieser Stelle zusätzlich Code einbringen zu können.

In einer On-premises Installation unterliegt die Ausführung von Skripten keiner Einschränkung.
In der Cloud wird die Speichernutzung und die Ausführungsdauer beschränkt.
Sollte das Skript die Limits überschreiten, wird es mit einer Fehlermeldung abgebrochen.

Die verfügbaren Bibliotheken sind identisch zur Transformation "C# Code Script".
Siehe :doc:`/api/sdk`

Die Verbindung unterstützt einen generischen code-based OAuth-Grant-Flow.
Der erzeugte Code steht in Skripten als Parameter "OAuthCode" zur Verfügung.
Nach der Ausführung des Schema-Skriptes wird er wieder in der Verbindung gespeichert.
Damit kann der Code für das Abrufen eines Refresh-Token verwendet und nachträglich entfernt werden.

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
				},
				"floors": {
					"title": "Floors",
					"type": "array",
					"ischildlist": false,
					"items": {
						"title": "Floors",
						"type": "object",
						"properties": {
							"appartments": {
								"title": "Appartments",
								"type": "number"
							},
							"renter": {
								"title": "Renter",
								"type": "number"
							}
						}
					}
				},
				"colors": {
					"title": "Colors",
					"type": "array"
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

Das Lesen von Schema-basierten Daten wird von dem JSON-Daten lesen Skript implementiert.
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
Eine Unterscheidung ist mittels Helper.GetParam\<bool\>("GetQuerySchema") möglich.


:Schreiben von Daten:

Das Schreiben von Daten wird von dem JSON-Daten schreiben Skript implementiert.
Das aktuell zu schreibende Objekt wird in Helper.SetObject bereitgestellt.
Der Rückgabewert der Methode sollte das Objekt mit ggf. generierte ID oder aktuellem Änderungsdatum sein.
Diese beiden Informationen werden dann vom Prozess ausgewertet und z.B. für Datenabbildungen verwendet.


Einstellungen
-------------

Die Verbindung verfügt nur über wenig Parameter, da alles von den Skripten getragen wird.
Damit Zugangsdaten aber nicht sichtbar in den Skripten enthalten sein müssen, gibt es folgende
Werte, die dann in den Helper-Parametern zur Verfügung stehen.

:Authentifizierung URL:

Platzhalter für eine URL. Parameter 'Url'

:Benutzername:

Platzhalter für einen Benutzernamen. Parameter 'Username'

:Passwort:

Platzhalter für ein Passwort, welches besonders geschützt wird.
Das externe Auslesen oder Kopieren des Wertes wird nicht unterstützt.
Parameter 'Password'

:Authorization Url:

Platzhalter für eine URL. Parameter 'OAuthUrl'
Diese Url wird für die OAuth-Authorization verwendet.

:Account ID:

Platzhalter für eine Account ID. Parameter 'OAuthAccountId'

:Client ID:

Platzhalter für eine Client ID. Parameter 'OAuthClientId'

:Secret:

Platzhalter für ein Secret. Parameter 'OAuthSecret'

:Redirect Url:

Platzhalter für eine Redirect Url. Parameter 'OAuthRedirectUrl'
Diese Url wird für die OAuth-Authorization verwendet und automatisch an die Authorization Url in kodierter Form angehängt.

:API URL:

Damit zur Authentifizierung eine abweichende URL gepflegt werden kann.
Parameter 'ApiUrl'

:API Key:

Parameter 'ApiKey'


Beispiele
---------

:doc:`/api/example_salesviewer`
