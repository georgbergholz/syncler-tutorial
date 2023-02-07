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

	IN (Auflistung)

	LIKE


Folgende arithmetische Operatoren können verwendet werden.

	\+ (Addition)

	\- (Subtraktion)

	\* (Multiplikation)

	/ (Division)

	% (Modulo)


Für die Verbindung von Zeichenketten wird \+ verwendet.

Als Platzhalterzeichen in LIKE-Vergleichen wird \* verwendet.

	\'#ItemName#\' LIKE \'\*product\*\'

	\'#ItemName#\' LIKE \'*product\'

	\'#ItemName#\' LIKE \'product\*\'


Folgende Funktionen stehen zur Verfügung.

	LEN(\'#ItemName#\')

	IIF(\'#ItemName#\' <> \'\', \'nicht leer\', \'leer\')

	TRIM(\'#ItemName#\')

	SUBSTRING(\'#ItemName#\', start, length)