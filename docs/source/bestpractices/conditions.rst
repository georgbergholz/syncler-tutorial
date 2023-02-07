Formulierung von Bedingungen und Formeln
========================================

An verschiedenen Stellen in Prozessen und Transformationen können Bedingungen oder Formeln definiert werden.
Der Syntaxt dafür ist an SQL angelehnt, weißt aber ein paar Besonderheiten auf.

Im Folgenden wird der Syntax und seine Funktion erläutert.

Eine formulierte Bedingung muss einen Wahrheitswert zurückliefern.
Eine Formel kann aber auch andere Werte, wie Zahlen oder Zeichenketten generieren.




Folgende Vergleichsoperatoren können verwendet werden.

	<

	>

	<=

	>=

	<>

	=

	IN

	LIKE


Folgende arithmetische Operatoren können verwendet werden.

	+ (addition)

	- (subtraction)

	* (multiplication)

	/ (division)

	% (modulus)


Für die Verbindung von Zeichenketten wird + verwendet.

Als Platzhalterzeichen wird * verwendet.

	"ItemName LIKE '*product*'"

	"ItemName LIKE '*product'"

	"ItemName LIKE 'product*'"


