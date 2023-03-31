Übertragungen und Prozessfilter
===============================

Wenn Felder zwischen System übertragen werden, die gleichzeitig den Filter für die Übertragung beeinflussen, muss die Konfiguration geplant werden.
Wenn zum Beispiel nur aktive Firmen aus dem CRM in das ERP übertragen werden sollen, aber der Status "inaktiv" synchronisiert werden muss, blockieren sich diese
Anforderung.

Der Prozessfilter wird eine Firma, die auf "inaktiv" geändert wird, komplett ausschließen und damit kann dieser Status nicht übertragen werden.
Auf der anderen Seite sollen aber inaktive Firmen auch nicht als neue Daten im ERP angelegt werden.

Zur Auflösung dieser Situation sind zwei Varianten möglich.

Variante 1
----------

Der Status wird nicht als Filter verwendet und damit wird das Inaktiv-Kennzeichen in jedem Fall übertragen.
Sollten die System aber über unterschiedliche Datenbestände verfügen, werden dadurch auch bereits inaktive Firmen als neue Datensätze übertragen.
Wenn dies nicht gewünscht ist, sollte Variante 2 verwendet werden.

Variante 2
----------

Bei dieser Umsetzung bleibt der Prozessfilter bestehen und der Prozess überträgt nur aktive Firmen.
Damit jetzt aber auch das Inaktiv-Kennzeichen übertragen werden kann, wird ein zusätzlicher Prozess eingerichtet.
Dieser filtert auf inaktive Firmen und darf keine neuen Datensätze anlegen.
Dies kann mit dem Parameter "Verhalten bei keiner Übereinstimmung" erreicht werden.
Der Prozess muss auch nur das Statusfeld zuordnen.

Beide Prozesse arbeiten kontinuierlich und auf der Basis von Änderungen.
Unbekannte bzw. neue inaktive Firmen werden nicht in das ERP übernommen.
Für bekannte Firmen kann der Status "inaktiv" übertragen werden.
Eine weitere Übertragung findet ab da nicht mehr statt.
