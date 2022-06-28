Sage Bäurer b7
==============

Bei Sage Bäurer b7 handelt es sich um eine ERP-Software für Produktion und Handel im Mittelstand.

Die Anbindung erfolgt mittels Azure Service Bus.
Damit dies genutzt werden kann, muss das ERP-System entsprechend konfiguriert werden.

Die Besonderheit bei diesem Verfahren ist die entkoppelte Kommunikation.
Daten können nicht direkt abgefragt, sondern müssen per Nachricht angefordert werden.
Als Resultat wird die Antwort als Nachricht abgestellt und muss abgerufen werden.

Es stehen spezifische Prozesse für die Synchronisation mit Sage CRM und Zoho CRM inklusive Vorlagen zur Verfügung.
Weitere Systeme können per Universalprozesse angebunden werden, wobei nicht alle Parameter durch die Verbindung 
ausgewertet werden können. z.B. Filterangaben
Auch kann mit einem Universalprozess kein begonnener Initialsync fortgesetzt werden. Dieser muss dann immer komplett
neugestartet werden. 


Funktionen
----------

:Schema ermitteln:

    Die Ermittlung des Schemas erfolgt mit einer Anfragenachricht.
    Die Antwort enthält die verfügbaren Objekte und deren Felddefinition.
    Speziell das Kunden- und Lieferantenobjekt werden noch weiter unterteilt für Personen und Anschriften aufbereitet.
    Außerdem können vorhandene Auswahllisten (awl) abgefragt werden.

:Laden von Quelldaten:

    Daten können initial auf einem Schema basierend angefordert werden.
    Per Prozess-Parameter wird dieser Vorgang eingeleitet.
    Sollte dies mehrmals erfolgen, wird vor jedem Anfordern die Warteschlange geleert. 
    Dies kann einige Zeit in Anspruch nehmen.
    Eine weiterer Prozessparameter ermöglich auch die Wiederaufnahme der initialen Übertragung, ohne die Warteschlange zu leeren.
    Änderungen werden durch das ERP in einem eigenen Topic abgestellt und von dort abgefragt.
    Datensätze können auch einzeln angefordert werden.
    Außerdem besteht die Möglchkeit SQL-Abfragen einzusetzen.
    Je Anforderung von Daten erfolgt mit einer entkoppelten Nachricht. 
    Die Anforderung wird als Nachricht versendet.
    Danach wird eine definierte Zeit auf die Antwort gewartet.
    Sollte das ERP die Nachrichten nicht verarbeiten, kann es zum Timeout kommen.

:Laden von Schema-basierten Daten:

    Jedes Schema stellt einen UseCase dar.
    Das ERP stellt Änderungen in einem eigenen Topic selbstständig ab und 
    die Verbindung prüft bei Prozessausführung, ob Nachrichten vorhanden sind.
    Mehrfach gelesene Nachrichten im Service Bus führen zu einer Dead-Letter-Situation.
    Damit dies vermieden wird, werden alle verfügbaren Daten beim Lesen von Nachrichten verarbeitet, 
    unabhängig vom jeweiligen Prozess, der das Lesen ausgelöst hat.
    Gelesene Nachrichten werden deshalb in den Änderungsspeicher übernommen, falls es einen 
    definierten Prozess für dieses Objekt gibt.
    Die Prozesse arbeiten von da an über den Änderungsspeicher, um z.B. eine individuelle Fehlerbehandlung zu ermöglichen.
    Bei OUT-Nachrichten zu Änderungen kann dem Element s_aktion (Ausprägungen: NONE, INS, UPD, DEL) 
    die Art der Änderung entnommen werden.

:Laden von Abfrage-basierten Daten:

    Der UseCase SQLQuery ermöglich das Ausführen von SELECT-Anweisungen.

:Schreiben von Daten:

    Für das Schreiben von Daten werden ebenfalls Nachrichten erzeugt und abgestellt.
    Da zu diesem Zeitpunkt nicht sicher ist, ob und wann die Aktion ausgeführt wird, wird sie unter 
    Vorbehalt als erfolgreich gewertet.
    Am Ende einer Prozessausführung werden Responses des ERPs aus der Warteschlange abgerufen.
    Die Antworten werden mit den aktuellen Datensätzen abgeglichen.
    Sollte die Antwort zu einer früheren Nachricht gehören, wird das als zusätzliches Resultat 
    in der Prozessausführung behandelt.
    Speziell bei der Neuanlage wird über die CorrelationID der Nachricht eine Beziehung zum Quelldatensatz hergestellt, 
    da die Kommunikation mit dem ERP nicht direkt erfolgt.
    Das Löschen wird nicht unterstützt.

:Schreiben von Bulk-Daten:

    Diese Funktion wird nicht unterstützt.


Einstellungen
-------------

Folgende Einstellungen müssen bereitgestellt werden.

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

Das Objekt Rechnung wird wegen seiner zusätzlichen Vorgangsunterteilung in mehrere Objekt je Vorgang durch die
Verbindung aufgetrennt.

Speziell zu Belegen gibt es noch weitere Funktionalitäten.
Siehe :doc:`/sync/b7_belege`
