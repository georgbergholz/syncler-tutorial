Sage B�urer b7
==============

Bei Sage B�urer b7 handelt es sich um eine ERP-Software f�r Produktion und Handel im Mittelstand.

Die Anbindung erfolgt mittels Azure Service Bus.
Damit dies genutzt werden kann, muss das ERP-System entsprechend konfiguriert werden.
Die Besonderheit bei diesem Verfahren ist die entkoppelte Kommunikation.
Daten k�nnen nicht direkt abgefragt, sondern m�ssen per Nachricht angefordert werden.
Als Resultat wird die Antwort als Nachricht abgestellt und muss aktiv abgerufen werden.

F�r den Syncler m�ssen folgende Daten bereitgestellt werden.

:Service Bus Endpunkt:

Die URL des Nachrichtendienstes wird mit der Kundennummer vervollst�ndigt.
```
sb://sb-#####-b7-crm.servicebus.windows.net/
```

:Kundenkennzeichen:

Die Eingabe folgt diesem Schema und beginnt mit der Kundennummer.
```
#####.xxxxx
```

:Mandant:

Damit wird an der Verbindung gekennzeichnet, welcher ERP-Mandant angesprochen werden soll.
F�r eine Mehrmandanten-Integration wird je Mandant eine Verbindung eingerichtet.

:SharedAccessKey Name:

Dieser Wert geh�rt zu den Zugangsdaten.

:SharedAccessKey Lesen:

Dieser Wert geh�rt zu den Zugangsdaten.

:SharedAccessKey Schreiben:

Dieser Wert geh�rt zu den Zugangsdaten.

:SharedAccessKey Initialisierung:

Dieser Wert geh�rt zu den Zugangsdaten.

:Timeout Verbindung:

Mit dieser Angabe kann das Standardtimeout f�r die Azure Verbindung angepasst werden. 
Die Angabe erfolgt in Millisekunden und das Minimum und Standardwert sind 100000. 
Eine Anpassung des Standardwertes ist nur dann erforderlich, wenn Abfragen mit einem Timeout-Fehler abgebrochen werden.

:Timeout Nachrichten:

Mit dieser Angabe kann das Standardtimeout f�r die Azure-Abfragen angepasst werden. 
Die Angabe erfolgt in Millisekunden und das Minimum und Standardwert sind 5000.

UseCases
--------

F�r die Kommunikation sind verschiedene UseCases definiert.
Neben den verf�gbaren Objekten wird damit auch die Art und das System festgelegt.

```
UC.SageCRM.Schema.REQ
UC.SageCRM.AllCustomers.REQ
UC.Sageb7.AllCustomers.RESP
UC.SageCRM.Selection.REQ
UC.SageCRM.Customer.REQ
UC.Sageb7.Customer.RESP
UC.SageCRM.SqlQuery.REQ
```

Folgende Objekte werden unterst�tzt.

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
Dabei werden auch Datenstrukturen in ihre Bestandteile zerlegt, damit diese gezielt in der Integration verwendet werden k�nnen.

Der Kunde wird z.B. immer als komplexes Objekt mit allen Ansprechpartnern und Adressen bereitgestellt.
Diese Bestandteile werden aus dem Schema und sp�ter den Daten herausgel�st und im Syncler einzeln verwendet.

Daten lesen
-----------

Es gibt verschiedene M�glichkeiten Daten zu lesen.
Das ERP wird �nderungen direkt abstellen, die von der Verbindung dann nur noch gelesen werden m�ssen.
Die Verbindung kann einzelne Datens�tze anfordern, welche nach der Verarbeitung durch das ERP abgestellt werden.
Mit einem speziellen UseCase kann die initiale Synchronisation angefordert werden.
Dadurch werden alle Daten des ERP-System f�r ein bestimmtes Objekt abgestellt.
Per Prozess-Parameter wird dieser Vorgang eingeleitet.
Sollte dies mehrmals erfolgen, wird vor jedem Anfordern die Warteschlange geleert. 
Dies kann einige Zeit in Anspruch nehmen.

Mit einem weiteren Prozess-Parameter kann ein initiale Anforderung aber auch fortgesetzt werden.
M�glich ist, dass die erste Anforderung zu einem Timeout gef�hrt hat, die Daten aber dennoch aufbereitet werden.
Dann sollte die initiale �bertragung fortgesetzt werden.

Mehrfach gelesene Nachrichten im Service Bus f�hren zu einer Dead-Letter-Situation.
Damit dies vermieden wird, werden alle verf�gbaren Daten beim Lesen von Nachrichten verarbeitet, unabh�ngig vom jeweiligen Prozess, der das Lesen ausgel�st hat.
Gelesene Nachrichten werden deshalb in den �nderungsspeicher �bernommen, falls es einen definierten Prozess f�r dieses Objekt gibt.
Sobald der Prozess ausgef�hrt wird, findet er diese Daten und beginnt mit der Verarbeitung.
Dies gilt auch f�r zusammengesetzte Objekte wie den Kunden. 
Anschriften und Ansprechpartner werden im �nderungsspeicher zwischengespeichert, bis der jeweilige Prozess ausgef�hrt wird.

Bei OUT-Nachrichten zu �nderungen kann dem Element s_aktion (Auspr�gungen: NONE, INS, UPD, DEL) die Art der �nderung entnommen werden.

F�r Abfrage-basierte Verarbeitungen k�nnen auch direkte SQL-Anfragen definiert werden.
Hier wird ein Oracle SELECT-Statement erwartet.

Daten schreiben
---------------



Konventionen
------------

:Messages mit einer Messagesize > 256 KB:

Da eine Message die maximale Gr��e von 256KB nicht �berschreiten darf, muss sie gesplittet werden. 
In den Splitts werden die Properties

* SplitNumber (int32) � Nummer des aktuellen Splitts
* SplitTotalNumber (int32) � Gesamtzahl der Splitts 

zur Kennzeichnung der Teile verwendet.
Vor der Verarbeitung m�ssen die Splitts zur Gesamtnachricht zusammengesetzt werden.
Splitts k�nnen bei allen Nachrichten auftreten, auch beim Bereitstellen des Schemas.

:Mehrere Antworten zu einer Anfrage:

Zu einer Anfrage kann es mehrere Antwortnachrichten geben (z.B. n Rechnungen zu einem Auftrag).
Zur Kennzeichnung werden die Properties

* ResultRecord (int32) � Nummer der aktuellen Antwort
* ResultTotalRecords (int32) � Gesamtzahl der Antworten

verwendet. 
Eine Antwort kann ggf. aus mehreren Splitts bestehen. 
Jede, ggf. aus Splitts zusammengesetzte Antwort, enth�lt ein g�ltiges Datenobjekt.

:Zuordnung von Antworten zum System der Anfrage:
Damit im Falle von Antworten zu Anfragen in der Definition der Subscription auf das anfragende System Bezug genommen werden kann, wird die neue Property

* CorrelationSysID (string) � Name des anfragenden Systems (entspricht SysId aus Anfrage)
 
verwendet. 
�ber die Property CorrelationId kann der Bezug zur Nachricht der Anfrage hergestellt werden.
