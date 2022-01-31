Sage CRM
========

Beschreibung

Funktionen
----------

:Schema ermitteln:

:Laden von Quelldaten:

:Laden von Schema-basierten Daten:

:Laden von Abfrage-basierten Daten:

:Schreiben von Daten:

:Schreiben von Bulk-Daten:

	Diese Funktion wird nicht unterstützt.


Einstellungen
-------------


Besonderheiten
--------------

Die Kommunikation erfolgt über den SOAP Webservice des CRMs.
Dieser bringt einige Besonderheiten mit sich.

	Auswahlfelder werden nicht als Code / DB-Wert zurückgegeben, sondern als Übersetzung in der Standardsprache des CRMs.
	Dies gilt nicht für den Feldtyp "Intelligente Auswahl". Dieser liefert den Code / DB-Wert des Feldes zurück.

	Felder werden ohne den DB-Präfix verwendet. 
	Dadurch stehen Felder mit einer Zahl nach dem Präfix im Namen nicht zur Verfügung, 
	da dies zu einem unerlaubten Namen im XML führen würde.

	Felder mit dem Kürzel "sp_" im Namen führen zu einer kompletten Ablehnung der Entität. 
	Ursache ist wahrscheinlich eine vermutete SQL-Injektion.

	Wird einem Kommunikationsdatensatz ein CRM-Benutzer als Organisator zugewiesen, wird sichergestellt, 
	dass dieser auch als Benutzer zugewiesen ist.


