CAS - Dynamics Business Central (Draft)
===============================


BC Kunden nach CAS Firma
----

Die Übertragung wird nur ausgeführt, wenn es bereits eine Datenabbildung zwischen dem Kontakt des Kunden und einer Firma gibt.
Sollte keine direkte Datenabbildung existieren, wird eine neue Datenabbildung für den aktuellen Kunden und der Firma des Kontaktes angelegt.
Deshalb steht keine Übereinstimmungsregel zur Verfügung.

CAS Firma nach BC Kunden
----

Bei der Neuanlage eines Kunden wird von der API automatisch ein neuer Kontakt angelegt.
Da dies nicht steuerbar ist, kann der ggf. bereits vorhandene Kontakt der Firma nicht direkt zugeordnet werden.
Aus diesem Grund wird der neue Kontakt direkt wieder gelöscht und eine Beziehung zwischen dem neuen Kunden und dem vorhandenen Kontakt hergestellt.

Die Übertragung wird nur ausgeführt, wenn es bereits eine Datenabbildung zu einem Kontakt gibt.

In Business Central ist nur ein Kunde je Kontakt zugelassen. 
Deshalb steht keine Übereinstimmungsregel zur Verfügung. 
Allerdings kann mit dem Verhalten für keine Übereinstimmung die Neuanlage gesteuert werden.
Wenn Datensatz angelegt werden soll, können nur Änderungen übertragen werden.
Sollte sich keine Datenabbildung finden oder ableiten lassen, wird nach Geschäftsbeziehungen gesucht.
Eine gefundene Geschäftsbeziehung wird direkt für die Zuordnung verwendet.
Ansonsten wird von einer Neuanlage ausgegangen.

Die Kundennummer wird nach erfolgreicher Übertragung in das Feld SIS_ACCOUNT# zurückgeschrieben und steht damit unmittelbar zur Verfügung.



CAS Ansprechpartner nach Dynamics BC Kontakt
--------------------------------------------


