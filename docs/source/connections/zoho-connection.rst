Die Zoho CRM Verbindung
=======================


.. image:: /images/zoho-api-console.png
  :width: 800
  :alt: API-Konsole

Beschreibung

Funktionen
----------

:Schema ermitteln:

:Laden von Quelldaten:

:Laden von Schema-basierten Daten:

:Laden von Abfrage-basierten Daten:

:Schreiben von Daten:

:Schreiben von Bulk-Daten:

	Diese Funktion wird nicht unterstützt.


Einstellungen
-------------


Besonderheiten
--------------

Wenn Daten per Transformation geladen werden, wird der Filter als Search Criteria übergeben.
Eine Ausnahme stellen Photos dar.
Hier wird eine Feldnotation aus Modulname und Modul-ID erwartet.

	RelationModule|:|Accounts|;|RelationId|:|23456789|;|

Das Photo steht dann als Base64 zur Verfügung und kann z.B. in Serienbriefen genutzt werden.