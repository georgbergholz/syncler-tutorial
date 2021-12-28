Sage Bäurer b7
==============

Bei Sage Bäurer b7 handelt es sich um eine ERP-Software für Produktion und Handel im Mittelstand.

Die Anbindung erfolgt mittels Azure Service Bus.
Damit dies genutzt werden kann, muss das ERP-System entsprechend konfiguriert werden.
Die Besonderheit bei diesem Verfahren ist die entkoppelte Kommunikation.
Daten können nicht direkt abgefragt, sondern müssen per Nachricht angefordert werden.
Als Resultat wird die Antwort als Nachricht abgestellt und muss aktiv abgerufen werden.

Für den Syncler müssen folgende Daten bereitgestellt werden.

:Service Bus Endpunkt:

Die URL des Nachrichtendienstes wird mit der Kundennummer vervollständigt.

.. code-block:: none

sb://sb-#####-b7-crm.servicebus.windows.net/


:Kundenkennzeichen:

Die Eingabe folgt diesem Schema und beginnt mit der Kundennummer.

.. code-block:: none

#####.xxxxx


:Mandant:

Damit wird an der Verbindung gekennzeichnet, welcher ERP-Mandant angesprochen werden soll.
Für eine Mehrmandanten-Integration wird je Mandant eine Verbindung eingerichtet.

:SharedAccessKey Name:

Dieser Wert gehört zu den Zugangsdaten.

:SharedAccessKey Lesen:

Dieser Wert gehört zu den Zugangsdaten.

:SharedAccessKey Schreiben:

Dieser Wert gehört zu den Zugangsdaten.

:SharedAccessKey Initialisierung:

Dieser Wert gehört zu den Zugangsdaten.

:Timeout Verbindung:

Mit dieser Angabe kann das Standardtimeout für die Azure Verbindung angepasst werden. 
Die Angabe erfolgt in Millisekunden und das Minimum und Standardwert sind 100000. 
Eine Anpassung des Standardwertes ist nur dann erforderlich, wenn Abfragen mit einem Timeout-Fehler abgebrochen werden.

:Timeout Nachrichten:

Mit dieser Angabe kann das Standardtimeout für die Azure-Abfragen angepasst werden. 
Die Angabe erfolgt in Millisekunden und das Minimum und Standardwert sind 5000.

UseCases
--------

Für die Kommunikation sind verschiedene UseCases definiert.
Neben den verfügbaren Objekten wird damit auch die Art und das System festgelegt.

.. code-block:: none

UC.SageCRM.Schema.REQ
UC.SageCRM.AllCustomers.REQ
UC.Sageb7.AllCustomers.RESP
UC.SageCRM.Selection.REQ
UC.SageCRM.Customer.REQ
UC.Sageb7.Customer.RESP
UC.SageCRM.SqlQuery.REQ


Folgende Objekte werden unterstützt.

* Customer - kunde
* Supplier - lieferant
* Part - teil
* ProductFamily - produktgruppe
* Project - projekt
* SalesOpp - vc
* Invoice - rechnung
* Order - auftrag
* Offer - angebot
* Selection - awl

Schema
------

Es kann die Bereitstellung des Datenschemas angefordert werden.
Die Antwort wird verarbeitet und in die Syncler-Form gebracht.
Dabei werden auch Datenstrukturen in ihre Bestandteile zerlegt, damit diese gezielt in der Integration verwendet werden können.

Der Kunde wird z.B. immer als komplexes Objekt mit allen Ansprechpartnern und Adressen bereitgestellt.
Diese Bestandteile werden aus dem Schema und später den Daten herausgelöst und im Syncler einzeln verwendet.

Daten lesen
-----------

Es gibt verschiedene Möglichkeiten Daten zu lesen.
Das ERP wird Änderungen direkt abstellen, die von der Verbindung dann nur noch gelesen werden müssen.
Die Verbindung kann einzelne Datensätze anfordern, welche nach der Verarbeitung durch das ERP abgestellt werden.
Mit einem speziellen UseCase kann die initiale Synchronisation angefordert werden.
Dadurch werden alle Daten des ERP-System für ein bestimmtes Objekt abgestellt.
Per Prozess-Parameter wird dieser Vorgang eingeleitet.
Sollte dies mehrmals erfolgen, wird vor jedem Anfordern die Warteschlange geleert. 
Dies kann einige Zeit in Anspruch nehmen.

Mit einem weiteren Prozess-Parameter kann ein initiale Anforderung aber auch fortgesetzt werden.
Möglich ist, dass die erste Anforderung zu einem Timeout geführt hat, die Daten aber dennoch aufbereitet werden.
Dann sollte die initiale Übertragung fortgesetzt werden.

Mehrfach gelesene Nachrichten im Service Bus führen zu einer Dead-Letter-Situation.
Damit dies vermieden wird, werden alle verfügbaren Daten beim Lesen von Nachrichten verarbeitet, unabhängig vom jeweiligen Prozess, der das Lesen ausgelöst hat.
Gelesene Nachrichten werden deshalb in den Änderungsspeicher übernommen, falls es einen definierten Prozess für dieses Objekt gibt.
Sobald der Prozess ausgeführt wird, findet er diese Daten und beginnt mit der Verarbeitung.
Dies gilt auch für zusammengesetzte Objekte wie den Kunden. 
Anschriften und Ansprechpartner werden im Änderungsspeicher zwischengespeichert, bis der jeweilige Prozess ausgeführt wird.

Bei OUT-Nachrichten zu Änderungen kann dem Element s_aktion (Ausprägungen: NONE, INS, UPD, DEL) die Art der Änderung entnommen werden.

Für Abfrage-basierte Verarbeitungen können auch direkte SQL-Anfragen definiert werden.
Hier wird ein Oracle SELECT-Statement erwartet.

Daten schreiben
---------------



Konventionen
------------

:Messages mit einer Messagesize > 256 KB:

Da eine Message die maximale Größe von 256KB nicht überschreiten darf, muss sie gesplittet werden. 
In den Splitts werden die Properties

* SplitNumber (int32) – Nummer des aktuellen Splitts
* SplitTotalNumber (int32) – Gesamtzahl der Splitts 

zur Kennzeichnung der Teile verwendet.
Vor der Verarbeitung müssen die Splitts zur Gesamtnachricht zusammengesetzt werden.
Splitts können bei allen Nachrichten auftreten, auch beim Bereitstellen des Schemas.

:Mehrere Antworten zu einer Anfrage:

Zu einer Anfrage kann es mehrere Antwortnachrichten geben (z.B. n Rechnungen zu einem Auftrag).
Zur Kennzeichnung werden die Properties

* ResultRecord (int32) – Nummer der aktuellen Antwort
* ResultTotalRecords (int32) – Gesamtzahl der Antworten

verwendet. 
Eine Antwort kann ggf. aus mehreren Splitts bestehen. 
Jede, ggf. aus Splitts zusammengesetzte Antwort, enthält ein gültiges Datenobjekt.

:Zuordnung von Antworten zum System der Anfrage:
Damit im Falle von Antworten zu Anfragen in der Definition der Subscription auf das anfragende System Bezug genommen werden kann, wird die neue Property

* CorrelationSysID (string) – Name des anfragenden Systems (entspricht SysId aus Anfrage)
 
verwendet. 
Über die Property CorrelationId kann der Bezug zur Nachricht der Anfrage hergestellt werden.
