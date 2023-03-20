Json in Spalten
===============

Diese Transformation erzeugt einzeln verwendbare Spalten auf der Basis von Json.
Die Json-Vorlage kann mittels Schaltfläche "Spalten ermitteln" ausgewertet werden.
Dabei werden neue Spalten generiert, die auch geschachtelte Strukturen berücksichtigen.


Wenn keine Angaben zu den Json-Daten erfolgen, wird hiermit nur eine Reihe neuer Spalten ohne Wert erzeugt, die z.B.
innerhalb eines Ablaufs mit den Daten eines lesenden Prozesses gefüllt werden können.


Sobald unter Json-Daten etwas angegeben wird, wird dieser Bereich als Json interpretiert und die Daten in die
Spalten übernommen.
Dabei können auch Platzhalter zu anderen Spalten verwendet werden, die Json als Zeichenfolge enthalten.