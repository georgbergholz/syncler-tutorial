Datensatzsperren
================

Datensatzsperren werden bei der Verarbeitung erzeugt und dienen der Konfliktbehandlung.
Außerdem stellen sie die Aktualität von Daten sicher.
Sobald ein Datensatz verarbeitet wird, wird der Quelldatensatz gesperrt. 
Sollte diese Sperre bereits existieren und keine  oder neuere Änderungsinformtion enthalten, wird die Verarbeitung zurückgestellt.
Wenn es sich um eine Aktualisierung handelt, wird auch das Ziel gesperrt.
Sollte diese Sperre bereits existieren und keine  oder neuere Änderungsinformtion enthalten, wird die Verarbeitung zurückgestellt.
Nach Abschluss der Verarbeitung wird die Sperre mit den aktuellen Änderungsinformationen aktualisiert.
Dies ermöglicht es anderen Prozessen zu prüfen, ob ihre bereits gelesenen Daten noch aktuell sind.
Datensatzsperren bleiben über die Ausführung des Prozesses hinaus noch 60 Minuten gespeichert, damit die überkreuzte Ausführungen verschiedener Prozesse diese zur Verfügung hat.
