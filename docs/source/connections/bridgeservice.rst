Die SQL- und Dateibrücke
========================

Hierbei handelt es sich um eine zusätzliche API, die separat installiert werden muss.
Die API ermöglicht das Ausführung von SQL Abfragen und das Herunterladen von Dateien, ohne direkte
SQL Verbindung oder Dateisystemzugriff.

Mittels einer Installationsroutine wird die API als Windowsdienst eingerichtet.
Zusätzlich steht eine Administrationsanwendung zur Verfügung, um die Zugangsdaten, die Url und den Port der API 
einzustellen. Eine Verwendung über einen Reverse Proxy ist ebenfalls möglich.
Bei der Url und dem Port handelt es sich um lokale Daten, die vom Dienst abgehört werden.
Diese können sich den öffentlichen Angaben im Syncler unterscheiden, abhängig von der Infrastruktur.

Es findet keine weitere Datenspeicherung von Zugangsdaten auf diesem System statt.

Im Syncler an den betreffenden Verbindungen werden die Zugangsdaten zur API eingerichtet.
Ab da finden alle direkten SQL- oder Dateizugriffe über die API statt.

Für den Zugriff auf die API wird ein Anmeldeverfahren und eine dynamische Verschlüsselung angewendet.
Alle SQL Zugangsdaten werden beim API Zugriff dynamisch verschlüsselt und an die API gesendet.

Je nach Art des Einsatzes stellt die API dann die SQL-Verbindung her und führt die Abfrage aus 
oder liest eine Datei ein.
Das Resultat wird an die aufrufende Verbindung übergeben.