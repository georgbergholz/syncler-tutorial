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




�nderungsspeicher
-----------------

Da der Prozess eine Abfrage f�r die Gesamtheit der Daten definiert, ist er nicht in der Lage, gezielt einen einzelnen Datensatz nachzuladen.
Sollte dies aber in Folge eines Fehlers oder einer notwendigen Wiederholung erforderlich werden, wird der �nderungsspeicher eingesetzt.
Der Prozess legt dort f�r diesen Fall den Datensatz ab, damit er in einer sp�teren Verarbeitung wieder zur Verf�gung steht.

F�r dieses Verhalten steht ein Parameter zur Verf�gung, der das Resultat beeinflusst.
Wenn "Immer den �nderungsspeicher" aktiviert wird, wird die Kopie direkt nach dem Lesen abgespeichert und steht sp�ter unver�ndert zur Verf�gung.
Das f�hrt allerdings auch zu einem gr��eren Verbrauch an Datenbankspeicher und kann die Performance beeinflussen.
Sollte der Parameter nicht aktiv sein, kann der Prozess nur auf eine ggf. transformierte Version des Datensatzes zugreifen und diese wird dann im �nderungsspeicher abgelegt.
Bei einer sp�teren Ausf�hrung ist der Prozess nicht mehr in der Lage, dies zu unterscheiden, weshalb die Transformation dieses Datensatzes erneut ausgef�hrt wird.
Das muss bei der Planung der Transformation ber�cksichtigt werden.
Ggf. sollten Felder vor der irreversiblen Ver�nderung kopiert werden.
Es ist auch nicht empfohlen, die Transformation f�r diese Datens�tze zu �berspringen, da hier u.a. auch externe Systeme abgefragt werden, was zu einem anderen Resultat f�hren kann.