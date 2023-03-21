Json in Spalten
===============

Diese Transformation erzeugt einzeln verwendbare Spalten auf der Basis von Json.
Im Bereich Json-Vorlage wird ein Json-Objekt eingegeben, das als Vorlage für die Daten zur Laufzeit dient.
Die Json-Vorlage kann mit der Schaltfläche "Spalten ermitteln" ausgewertet werden, wobei auch geschachtelte Strukturen berücksichtigen
Das Resultat ist eine Liste von Spalten, die unterhalb angezeigt wird.


Wenn keine Angaben zu den Json-Daten erfolgen, wird hiermit nur eine Reihe neuer Spalten ohne Wert erzeugt.
Das ist z.B. innerhalb eines Ablaufs hilfreich, um die Daten eines lesenden Prozesses verfügbar zu machen.


Sobald unter Json-Daten eine Eingabe erfolgt ist, wird dieser Bereich als Json interpretiert und die Daten in die
Spalten übernommen.
Dabei können auch Platzhalter zu anderen Spalten verwendet werden, die Json als Zeichenfolge enthalten.


Einstellungen
-------------

Folgende Parameter werden konfiguriert.

:Name:

Ist eine administrative Bezeichnung.

:Json-Vorlage:

Definiert die Struktur der Json-Daten, aus denen die neuen Spalten erzeugt werden.

:Json-Daten:

Beinhaltet Laufzeitdaten, mit denen die neuen Spalten gefüllt werden.
Es können Platzhalter mit anderen Feldern genutzt werden.
Die Struktur muss der Vorlage entsprechen.