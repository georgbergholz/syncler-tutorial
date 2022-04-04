Nachfolgeprozesse (Draft)
=================

Mit Nachfolgeprozessen können Sie einzelne Prozesse in eine Abfolge bringen, um z.B. verschiedene Ziele anzusprechen.

Der ausgewählte Nachfolgeprozess wird mit einem Warteschlangeneintrag vom Typ "Nachfolger" gestartet und erhält zusätzlich einen Verwis auf den aktuellen Warteschlangeneintrag.
Im aktuellen Warteschlangeneintrag wird vermerkt, welche Datensätze erfolgreich oder mit einer Warnung verarbeitet wurden.
Nur diese Datensätze werden vom Nachfolger verarbeitet.

Ein Schema-basierter Prozess kann nur Daten an einen Schema-basierten Prozess übergeben. In den meisten Fällen muss dabei auch das Quellobjekt identisch sein.

Ein Abfrage-basierter Prozess kann nur Daten an einen Abfrage-basierten Prozess übergeben.
Dabei kann festgelegt werden, ob die Daten selbst oder die ID-Werte per Datenabbildung übergeben werden.
Ohne ID-Felder in den Quelldaten wird immer der Änderungsspeicher verwendet. 
Wenn ID-Felder angegeben wurden...


Beim Änderungsspeicher, ohne die Datenabbildung, muss im Nachfolger das ID-Feld angegeben, sonst hält er das für eine ChangedGuid und findet nichts

