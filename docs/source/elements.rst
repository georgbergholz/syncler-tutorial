Syncler Elemente
====

Verbindungen, Prozesse und Datendienste sind die grundlegenden Elemente im Syncler für die Realisierung Ihrer Aufgaben.
Daneben gibt es noch weitere Elemente für die Koordination, Überwachung und Ausführung.

:Verbindungen:

Eine Verbindung stellt die Kommunikation mit einem externen System bereit.
Neben klassischen System wie CRM oder ERP kann sich hinter einer Verbindung aber auch der Eingang für Daten, z.B. Push-Nachrichten oder Dateien
und der Ausgang von Daten, z.B. Serienbriefe verbergen.

:Prozesse:

Ein Prozess führt eine Aufgabe aus. Dazu zählt z.B. das Übertragen oder Synchronisieren von Daten.
Für diesen Zweck verwendet ein Prozess vorhandene Verbindungen.


:Datendienste:

Ein Datendienst ist die Definition eines Berichtes. Dieser kann manuell oder automatisch erstellt werden.

:Warteschlange:

Die Ausführung von Prozessen oder Datendiensten wird mit einem Eintrag in einer Warteschlange gestartet.
Warteschlangen werden kontinierlich auf auzuführende Einträge geprüft.
Nach der Ausführung bilden die Einträge ein Protokoll der jeweiligen Ausführung.

:Protokolle:

Verbindungen, Prozesse und Datendienste erzeugen Nachrichten, die in den Protokollen gespeichert werden.
Jede Nachricht verfügt über eine Einstufung und kann noch zusätzliche Daten enthalten.

:Datenabbildungen:

Für eine kontinuierliche Synchronisation von Datensätzen werden Datenabbildungen je Datensatz und Richtung angelegt.
Die Abbildungen speichern ID-Werte, Synchronisationsinformationen und können auch Kopien des Quelldatensatzes für eine genaue Änderungsanalyse enthalten.

:Änderungsspeicher:

Der Änderungsspeicher ist ein Zwischenspeicher für Datensätze, die noch verarbeitet oder weiterverarbeitet werden müssen.
Abhängig von Prozess und Verbindung kommt der Änderungsspeicher auch in der Fehlerbehandlung oder verzögerten Übertragung zum Einsatz.

:Datensatzsperren:

Datensatzsperren werden bei der Verarbeitung erzeugt und dienen der Konfliktbehandlung.
Außerdem stellen sie die Aktualität von Daten sicher.

:Serienbrief Vorlagen:

Für die Seriendruckfunktion können Vorlagen in der Datenbank verwaltet werden.
