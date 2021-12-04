Abfrage-Prozesse
================

Abfrage-Prozesse basieren nicht auf einem global bekannten Datenschema, welche durch Verbindungen bereitsgestellt werden.
Ein Abfrage-Prozess erzeugt ein lokales Datenschema, das aus einer spezifischen Abfrage generiert wird.

Parameter
---------



Abfrage und Ziel
----------------


Transformation
--------------




Änderungsspeicher
-----------------

Da der Prozess eine Abfrage für die Gesamtheit der Daten definiert, ist er nicht in der Lage, gezielt einen einzelnen Datensatz nachzuladen.
Sollte dies aber in Folge eines Fehlers oder einer notwendigen Wiederholung erforderlich werden, wird der Änderungsspeicher eingesetzt.
Der Prozess legt dort für diesen Fall den Datensatz ab, damit er in einer späteren Verarbeitung wieder zur Verfügung steht.

Für dieses Verhalten steht ein Parameter zur Verfügung, der das Resultat beeinflusst.
Wenn "Immer den Änderungsspeicher" aktiviert wird, wird die Kopie direkt nach dem Lesen abgespeichert und steht später unverändert zur Verfügung.
Das führt allerdings auch zu einem größeren Verbrauch an Datenbankspeicher und kann die Performance beeinflussen.
Sollte der Parameter nicht aktiv sein, kann der Prozess nur auf eine ggf. transformierte Version des Datensatzes zugreifen und diese wird dann im Änderungsspeicher abgelegt.
Bei einer späteren Ausführung ist der Prozess nicht mehr in der Lage, dies zu unterscheiden, weshalb die Transformation dieses Datensatzes erneut ausgeführt wird.
Das muss bei der Planung der Transformation berücksichtigt werden.
Ggf. sollten Felder vor der irreversiblen Veränderung kopiert werden.
Es ist auch nicht empfohlen, die Transformation für diese Datensätze zu überspringen, da hier u.a. auch externe Systeme abgefragt werden, was zu einem anderen Resultat führen kann.