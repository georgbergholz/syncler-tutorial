Nachfolgeprozesse
-----------------

Mit Nachfolgeprozessen k�nnen Sie einzelne Prozesse in eine Abfolge bringen, um z.B. verschiedene Ziele anzusprechen.

Der ausgew�hlte Nachfolgeprozess wird mit einem Warteschlangeneintrag vom Typ "Nachfolger" gestartet und erh�lt zus�tzlich einen Verwis auf den aktuellen Warteschlangeneintrag.
Im aktuellen Warteschlangeneintrag wird vermerkt, welche Datens�tze erfolgreich oder mit einer Warnung verarbeitet wurden.
Nur diese Datens�tze werden vom Nachfolger verarbeitet.

Ein Schema-basierter Prozess kann nur Daten an einen Schema-basierten Prozess �bergeben. In den meisten F�llen muss dabei auch das Quellobjekt identisch sein.

Ein Abfrage-basierter Prozess kann nur Daten an einen Abfrage-basierten Prozess �bergeben.
Dabei kann festgelegt werden, ob die Daten selbst oder die ID-Werte per Datenabbildung �bergeben werden.
Ohne ID-Felder in den Quelldaten wird immer der �nderungsspeicher verwendet. 
Wenn ID-Felder angegeben wurden...


Beim �nderungsspeicher, ohne die Datenabbildung, muss im Nachfolger das ID-Feld angegeben, sonst h�lt er das f�r eine ChangedGuid und findet nichts

