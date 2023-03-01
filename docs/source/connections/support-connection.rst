Support-Datenbank
=================

Diese Verbindung ermöglich den Zugriff auf die Support-Datenbank.
Hierbei handelt es sich um ein zusätzliches Feature, das aktiviert werden muss.

Siehe :doc:`/common/supportdatabase`


Funktionen
----------

:Schema ermitteln:

Das Schema wird automatisch über die vorhandenen Tabellen in der Support-Datenbank erstellt.
Zusätzlich kann ein geschachtelteter Datentyp definiert werden.


:Lesen von Schema-basierten Daten:

Das Lesen von Schema-basierten Daten in Universalprozessen wird unterstützt.
Für das gezielte Lesen einzelner Datensätze muss die Tabelle über eine ID-Spalte verfügen.


:Lesen von Abfrage-basierten Daten:

Das Lesen von Abfrage-basierten Daten wird per SQL-Verbindung realisiert.


:Schreiben von Daten:

Das Schreiben von einzelnen Datensätzen erfolgt basierend auf Schema-Objekten.
Daneben können auch SQL-Anweisungen mit speziellen Prozessen ausgeführt werden.


:Schreiben von Bulk-Daten:

Das Schreiben von Bulk-Importen wird unterstützt.



Einstellungen
-------------

Für die Verwendung dieser Verbindung sind keine Angaben erforderlich.
Für geschachteltete Datentypen können folgende Einstellungen verwendet werden.

:Select-Anweisung für Hauptobjekt:

Diese Abfrage ist die Basis für das Schemaobjekt "Mainobject".

:Select-Anweisung für geschachteltete Objekte:

Diese Abfrage definiert die Listenobjekte im "Mainobject". Mittels Platzhalter in Rautenschreibweise werden Daten aus dem Hauptobjekt für die Abfrage eingefügt.

:Optionale ID-Felder des Hauptobjektes:

Sollte es nicht möglich sein, die ID-Felder des Hauptobjektes zu ermitteln, können diese ggf. kommagetrennt angegeben werden. 
Dies ist für die Verwendung in Prozessen erforderlich.