Datenabbildungen
================

Für eine kontinuierliche Synchronisation von Datensätzen werden Datenabbildungen je Datensatz und Richtung angelegt.
Die Abbildungen speichern ID-Werte, Synchronisationsinformationen und können auch Kopien des Quelldatensatzes für eine genaue Änderungsanalyse enthalten.
Des weiteren werden Datenabbildungen für das Konfliktmanagement verwendet. 
Aus diesem Grund wird auch für jeden Prozess eine eigene Datenabbildung erzeugt, da die Prozesse keine direkte Beziehung untereinander haben. 
Die letzte Funktion ist die Verwaltung von Löschkennzeichen, die ein unerwünschtes erneutes Anlegen nach einer einseitigen Löschung vermeiden.

Der grundlegende Ablauf bei der Arbeit mit Datenabbildungen ist folgender.
Ein Prozess wird ausgeführt und wählt seine Quelldaten aus, die im Anschluss noch transformiert werden. 
Danach beginnt die Bearbeitung der einzelnen Datensätze. 
Zu jedem Quelldatensatz wird eine vorhandene Datenabbildung für diesen Prozess gesucht. 
Wenn dabei nichts gefunden wurde, wird die Suche auf parallele und komplementäre Prozesse ausgeweitet.
Diese Beziehung wird durch die verwendeten Verbindungen und die laufende Mandantennummer gebildet.
Sollte auch dies erfolglos sein, wird ggf. eine Übereinstimmungssuche ausgeführt. 
Wenn selbst diese kein Resultat liefert, geht der Syncler von einer Neuanlage aus und erzeugt ggf. eine neue Datenabbildung.

Sollte eine bestehende Abbildung für diesen Prozess gefunden werden, wird das Löschkennzeichen geprüft. 
Wenn dieses gesetzt ist, wird der Datensatz nicht weiter verarbeitet. 
Anderenfalls werden die Aktualisierungsinformationen, falls vorhanden, ausgewertet. 
Dabei wird zuerst die Quelle gegen die Aktualisierungsinformation der Quelle aus der Datenabbildung verglichen.

Falls diese identisch sind, wird davon ausgegangen, dass der Datensatz synchron ist und die Bearbeitung wird abgebrochen.
Dieser Mechanismus verhindert ein "Ping-Pong" der Prozesse, da eine Aktualisierung durch Prozess A als Auslöser für den komplementären Prozess B gilt.
Als nächstes wird die Datenabbildung mit dem Ziel verglichen. 
Sollte aus einem der Vergleiche ein Konflikt entstehen, wird die Konfliktlösung angewendet.
Sollte die Synchronisation durchgeführt werden, wird die eigene Datenabbildung aktualisiert. 
Abhängig von einer ggf. angewendeten Konfliktlösung werden auch parallele und komplementäre Datenabbildungen aktualisiert. 
Dies geschieht aber nur einseitig, damit diese Prozesse den Datensatz nicht als synchron behandeln und keinen Konflikt feststellen.
