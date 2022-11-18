Universal SDK Prozesse
======================

Die Universal SDK Verbindung dient der Entwicklung einer Anbindung eines fremden Systems zum Lesen, Schreiben oder Ausführen von Abfragen.

Die Universal SDK Prozesse sind unabhängig von dieser Verbindung und können mit jeder beliebigen Verbindung verwendet werden.

Es stehen zwei grundlegende Prozess-Plugins zur Verfügung.

Universal Prozess (SDK)
-----------------------

Dies ist ein einfache Universalprozess für die Übertragung eines Datenobjektes zwischen zwei Systemen.
Es stehen die Bereiche Transformation und Zuordnungen zur Verfügung.
Außerdem gibt es drei Skripte, die im Anschluss erläutert werden.

Aufbauend auf diesem Prozess gibt es noch eine Variante für Sage CRM, die eine gezielte Nachbearbeitung von Stammdaten
für eine konsistente Datenstruktur beinhaltet.
Der Einsatz wird bei der Arbeit mit Personen empfohlen.

Universal Sync Prozess für geschachtelte Daten (SDK)
----------------------------------------------------

Dies ist ein Universalprozess für die Übertragung von geschachtelten Datentypen zwischen zwei Systemen.
Es stehen die Bereiche Transformation und Zuordnungen für den Kopfdatensatz und die Positionsdatensätze zur Verfügung.
Außerdem gibt es drei Skripte, die im Anschluss erläutert werden.

Universal Abfrageprozess (SDK)
------------------------------

Bei diesem Prozess-Plugin handelt es sich um einen klassischen Abfrageprozess für die Verwendung mit Universal SDK Verbindung.
Der Prozess selbst bietet keine zusätzlichen Skript-Möglichkeiten.

SDK Skripte
-----------

Für die Prozess-Plugins Universal Prozess (SDK) und Universal Sync Prozess für geschachtelte Daten (SDK) können
zusätzliche Skripte definierte werden, die an bestimmten Punkten der Verarbeitung ausgeführt werden.
In allen Skripten steht der SDK Helper zur Verfügung, der die Schnittstelle zwischen Prozess, Daten und Skript realisiert.

Das "Prozess ausführen" Skript wird zu Beginn der Prozessausführung gestartet und läuft noch vor dem Lesen von Daten.
Das Skript kann dabei den Filter, das Abrufen aller Datensätze und den zweiten Filter überschreiben.
Auch werden alle Parameter aus dem Helper in den Prozess übernommen und stehen dadurch auch in der Quellverbindung beim Lesen von Daten zur Verfügung.
Mit SkipLoading kann das eigentliche Lesen auch übersprungen werden.

Das "Datensatz Verarbeitung" Skript wird für jeden gelesenen Datensatz einzeln ausgeführt.
Die Ausführung findet direkt vor dem Füllen und Schreiben des Zielobjektes statt.
Transformationen, Konfliktprüfung, Übereinstimmungssuche und die Neuanlagebedingung wurden zu diesem Zeitpunkt bereits ausgeführt.
Falls der Datensatz dabei übersprungen wurde, wird das Skript nicht ausgeführt.
Über den Helper stehen das Quellobjekt (GetObject), das Zielobjekt (SetObject) und die Feldzuordnungen (Mappings) zur Verfügung
und können verändert werden.
Die Skript-Methode kann folgende Werte zurückgeben, die dann die weitere Verarbeitung beeinflussen können.

* cancelled (die gesamte Verarbeitung wird abgebrochen)
* skipped (aktueller Datensatz wird übersprungen)
* failed (InnerException wird ausgewertet und Datensatz wird mit diesem Fehler abgebrochen)
* repeat (der aktuelle Datensatz wird wiederholt)
* success

Für den Universal Sync Prozess für geschachtelte Daten (SDK) bietet das Skript auch Zugriff auf die Positionsliste (GetChildObjects).
Da die Positionsliste nach der Skript-Ausführung komplett übernommen wird, können so auch Positionen hinzugefügt oder entfernt werden.

Das "Prozess abschließen" Skript wird beim Abschluss der Prozessausführung gestartet.
Dieses Skript kann die aktuelle Verarbeitung nicht mehr beeinflussen, aber andere Prozesse starten, oder die Prozessparameter für die Änderungsgrenzwerte verändern.

