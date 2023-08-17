Kuehne + Nagel
==============

Kuehne + Nagel bietet als Logistikunternehmen eine Schnittstelle zum Abrufen des Frachtstatus.
Mit dieser Verbindung können aktuell Container-Informationen abgerufen und verarbeitet werden.

Die Kuehne und Nagel Verbindung bietet ein Schemaobjekt für die Conatiner-Information und unterstützt auch Abfragen zu diesen Daten.

Für die Einrichtung werden die Anwendungszugangsdaten benötigt.
Melden Sie sich im Portal an und rufen Sie den Menüpunkt "My Applications" auf.
Hier finden Sie die vorhandenen Anwendungen.
Übertragen Sie die Zugangsdaten (user, password, client-id, client-secret) in die gleichnamigen Felder der Verbindung.



Funktionen
----------

:Schema ermitteln:

Die Verbindung stellt automatisch die Objekte containerInfo zur Verfügung.

:Lesen von Schema-basierten Daten:

Das Lesen wird nur mit einem Filter unterstützt.
Dieser muss aus zwei Informationen bestehen, die durch ein Semikolon getrennt sind.
Der erste Wert legt den "referenceType" fest.
Der zweite Wert muss den Wert enthalten.
Als Referenz-Typen stehen folgende zur Verfügung:

* ALL_CUSTOMER_REFERENCES
* SPECIFIC_CUSTOMER_REFERENCE
* BILL_OF_LADING
* DELIVERY_LOCATION
* TRACKING_NUMBER
* CONTAINER_NUMBER

Eine Abfrage eines Container wird wie folgt formuliert.

CONTAINER_NUMBER;ABCD12345

Eine Abfrage aller Kundenreferenzen würde wie folgt formuliert werden.

ALL_CUSTOMER_REFERENCES;%

:Lesen von Abfrage-basierten Daten:

Diese Funktion arbeitet wie das schema-basierte Lesen.
Die Abfrage wird auch mit zwei Werten formuliert.

Damit kann die Abfrage flexibel in Transformationen genutzt werden, um vorhandene Datensätze mit Conatiner-Informationen anzureichern.

:Schreiben von Daten:

Diese Funktion wird nicht unterstützt.


Einstellungen
-------------

Für den Zugriff muss der Benutzername, das Passwort, die Client-ID und der Geheimschlüssel festgelegt werden.

