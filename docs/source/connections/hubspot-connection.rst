HubSpot
=======

HubSpot ist ein CRM-System für die Bereiche Marketing, Vertrieb, Kundenservice und Content-Management.
Für die Verbindung wird die HubSpot REST API eingesetzt.
Um diese verwenden zu können, müssen folgende Einrichtungsschritte ausgeführt werden.

Für den Zugriff auf HubSpot können Sie mit einer privaten oder öffentlichen App arbeiten.

Für die Nutzung der privaten App führen Sie bitte folgende Schritte aus.
Rufen Sie mit administrativen Rechten das Einstellungsmenü in Ihrem Account auf.
Im Bereich Integrationen müssen Sie eine private App erstellen.
Klicken Sie dazu unter "Private Apps" auf "Private App erstellen".
Vergeben Sie einen Namen in den grundlegenden Informationen.
Unter "Bereiche" müssen Sie die Berechtigungen für die App konfigurieren.
Nur freigegebene Bereiche und Funktionen können genutzt werden.


Funktionen
----------

:Schema ermitteln:

Das Schema der Verbindung wird über die Web-API ermittelt.
Dafür werden die Properties der einzelnen Objekttypen abgerufen.


:Lesen von Schema-basierten Daten:
 
Das Lesen von Datensätzen erfolgt über die Web-API.
Einzelne Datensätze werden direkt abgerufen.
Listen von Datensätzen werden über die Search-Funktion abgerufen.
Im Where-Parameter kann hierfür das Json für die filterGroups übergeben werden.

.. code-block:: json

    {
        "filterGroups":[
            {
                "filters":[
                    {
                        "propertyName": "firstname",
                        "operator": "EQ",
                        "value": "Alice"
                    }
                ]
            }
        ]
    }

Wenn der Filter kein gültiges Json enthält, wird der übergebene Wert als query-Parameter für die Suche verwendet.
Dieser wird in verschiedenen Standardfeldern des Objektes gesucht.

Die Search-Funktion kann nur maximal 10.000 Datensätze zurückliefern.
Sollten Sie mehr Datensätze abrufen wollen, lassen Sie den Where-Parameter im Prozess leer und verwenden Sie stattdessen den zweiten Filter des Prozesses.

:Lesen von Abfrage-basierten Daten:

Diese Funktion wird nicht unterstützt.

