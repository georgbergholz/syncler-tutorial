Schemaobjekte und deren Funktion
================================

Ein Schemaobjekt ist ein benanntes Objekte zur Definition eines Datenobjektes mit Spalten, Gruppen und Meta-Informationen.
Schemaobjekte werden von Verbindungen individuell generiert und beschreiben ein Medium zur Kommunikation zwischen der Verbindung und anderen 
Komponenten, wie z.B. Prozessen.

Durch das Anlegen einer Verbindung oder durch einen Schema-Refresh produziert die Verbindung eine Liste von Schemaobjekten, die abgespeichert wird.
Innerhalb von Prozessen werden Schemaobjekte für die Definition von Transformationen und Feldzuordnungen genutzt.


Die Struktur
------------

Ein Schemaobjekt enthält eine Liste von Schemaspalten.
Eine Schemaspalte definiert eine Spalte eines Datenobjektes, welche die kleinste Informationseinheit ist.
Diese Defintion beinhaltet den Namen, den Datentyp, Angaben zu Pflichtfeld, Schreibschutz und ggf. maximaler Länge von Zeichenketten.
Die Konfiguration von Prozessen wird daneben noch mit Beschriftungen und Beschreibungen unterstützt.
Das Schemaobjekt enthält zusätzlich eine Liste von ID-Spalten.


Die Verwendung
--------------

Mit einem Schemaobjekt kann eine Lese-Anforderung an die Verbindung gestellt werden.
Durch zusätzliche Standard-Parameter, wie z.B. Filter oder Änderungsgrenzwerte, wird die Anforderung noch genauer spezifiziert.
Die Verbindung antwortet mit einem oder mehreren Datenobjekten, die durch das Schemaobjekt definiert wurden.
Nicht jedes Schemaobjekt ist für Lese-Anforderungen bestimmt. 
Manche werden ausschließlich für das Schreiben von Datenobjekten verwendet.
In solchen Fälle erfolgt dann auch nur eine leere Antwort.

Was genau beim Ausführen der Lese-Anforderung stattfindet, ist abhängig von Verbindung und Schemaobjekt.
In der Regel werden Daten aus dem externen System gelesen und zu dem angeforderten
Datenobjekt oder Datenobjekten zusammengesetzt.
Bei bestimmten Szenarien wird auch nur aus dem Änderungsspeicher gelesen, da dort bereitgestellte Daten erwartet werden.

