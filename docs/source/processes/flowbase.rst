﻿Ablauf-basierte Prozesse
========================

Der Universal Ablauf Prozess bietet die Möglichkeit verschiedene Prozesse zu kombinieren und in 
einer definierten Reihenfolge ausführen zu lassen.
Auch die gezielte Ausführung von Datendiensten und der Versand des Resultats können damit eingebunden werden.

Die Verkettung von Prozessen ist auch über Nachfolgeprozesse möglich, wobei die Kombinierbarkeit allerdings
eingeschränkt ist. Für die Ausführung von zwei Prozessen ist der Nachfolgeprozesse meist aber einfacher zu
konfigurieren.

Der Ablauf führt selbst keine Datenabfragen oder Transformationen durch.
Dies wird durch separat definierte Prozesse umgesetzt, welche durch den Ablauf gesteuert werden.

Folgende Standard-Aufgaben werden durch den Ablauf übernommen.

- Bereitstellung der Zeitsteuerung per Warteschlange
- gesammelte Fehlerbehandlung der ausgeführten Prozesse
- Aktivierung einer initialen Ausführung aller zugeordneten Prozesse
- Unterstützung einer Adhoc-Verfügbarkeit

Der Kern des Ablaufs sind die Ablaufschritte.
Diese definieren die spezifische Aufgabe und werden in der angegebenen Reihenfolge ausgeführt.
Es stehen verschiedene Typen von Schritten zur Verfügung.

- Das Ausführen eines Prozesses
- Das Ausführen eines Datendienstes

Trotz das der Ablauf einen eigenen Warteschlangeneintrag hat, werden denoch manuelle Warteschlangeneinträge 
für die ausgeführten Prozesse angelegt.
Dies stellt sicher, dass die Ausführung konsistent protokolliert werden kann und Standard-Mechanismen 
des Prozesses, wie die Fehlerbehandlung, möglich sind und individuell konfiguriert werden können.

Der Warteschlangeneintrag des Ablaufs bündelt dabei die einzelnen Ausführung mit Verweisen und einer summierten Statistik.


Adhoc-Ausführung
----------------

Am Ablauf kann über die Einstellungen "Quell-Verbindung" und "Quell-Objekt" der Ausgang eine Adhoc-Ausführung
definiert werden. Der Ablauf ist dabei der Empfänger dieser Anforderung, aber nicht der ausführende Prozess.
Bei der Abarbeitung der einzelnen Schritte werden Prozesse, die manuell ausgeführt werden sollen und eine identische 
Quell-Verbindung sowie Quell-Objekt haben, Adhoc ausgeführt.
Alle weiteren Prozesse, die ebenfalls der Quell-Verbindung und dem Quell-Objekt zugeordnet sind, werden mit identischem
Verhalten ausgeführt.
Alle weiteren Prozesse werden gemäß der Konfiguration ausgeführt.

Damit ist es möglich eine Kette von Aufgaben oder mehrere Adhoc-Übertragungen ausführen zu lassen.


Ausführen eines Prozesses
-------------------------

Der auszuführende Prozess muss bereits vorhanden sein, damit er in einem Ablauf ausgewählt werden kann.
Außer Abläufen selbst stehen alle vorhandenen Prozesse zur Verfügung.

Folgende Parameter können in diesem Schritt definiert werden.

**Name**

Dieser Name wird den einzelnen Meldungen des ausgeführten Prozesses vorangestellt.

**Prozess ausführen**

Hier wird der Prozess für die Ausführung festgelegt.

**Daten aus Prozess**

Die Kombination von Prozessen ermöglicht die Weiterverwendung von Quell- und Zieldaten der bereits 
ausgeführten Prozesse im Ablauf.
Dafür stehen folgende Optionen zur Auswahl.

"Quelldaten unverändert übernehmen" wählt die Quelldaten direkt nach dem Lesen und vor der Transformation aus.
Sollte die Transformation bei einzelnen Datensätzen zu Fehlern führen, werden diese zurückgestellt.
Auch mittels Zweitfilter ausgeschlossene Datensätze werden nicht weiterverarbeitet. 
Für Abfrage-basierte Prozesse setzt dies die Definition von ID-Feldern voraus. 

"Quelldaten transformiert übernehmen" wählt die Quelldaten nach der Transformation aus.
Fehler und Zweitfilter schließen hier ebenfalls Datensätze wieder aus.
Da das Zwischenspeichern der transformierten Daten nicht automatisch das Quell-Schema des folgenden Prozesses
verändert, müssen dort ggf. Parameter mit leeren Werten angelegt werden, damit Nicht-Standard-Felder zur Verfügung stehen.
Solange der Parameter keinen Wert hat, wird dem Datensatz auch nicht zugewiesen und die vorhandenen Daten 
können weiterverwendet werden.
Zu beachten ist außerdem, dass bei geschachtelten Daten nur die Transformationen der Hauptobjektes übernommen werden können.
Transformationen oder Filter an Positionen werden nicht zwischengespeichert.

"Keine Daten übernehmen" überspringt diese Funktion.
Da die Daten Prozess-bezogen zwischengespeichert werden, führt eine wiederholte Ausführen des selben Prozesses
zum Überschreiben des vorangegangenen Ergebnisses. Mit dieser Option kann dies verhindert werden.

Zieldaten werden bei den ersten beiden Optionen ebenfalls zwischengespeichert. Es ist allerdings von den beteiligten
Systemen abhängig, welche Daten hier zur Verfügung stehen. Die Verarbeitung kann z.B. entkoppelt erfolgen oder nur 
Basisinformationen zurückliefern.

**Daten aus Vorgänger**

Hier wird ein Prozess aus den vorangegangenen Schritten ausgewählt, dessen Quell- oder Zieldaten im aktuellen
Prozess verwendet werden sollen.
Im ersten Schritt des Ablauf steht deshalb nichts zur Verfügung.
Sollte die Ausführungsart "Prozess manuell ausführen" eingestellt sein, wird dieser Wert nicht benötigt.

**Ausführungsart**

Dies steuert die Art der Prozessausführung.

"Prozess manuell ausführen" entspricht dabei einer normalen Prozessausführung. Diese kann noch mit weiteren Parametern
beeinflusst werden. Der Adhoc-Start des Ablaufs würde dies mit Adhoc übersteuern.

"Prozess direkt mit Quelldaten aus Vorgänger ausführen" startet den Prozess mit den zwischengespeicherten Daten.
Der Prozess führt keine eigene Datenabfrage aus, mit Ausnahme von ggf. konfigurierten Fehlerwiederholungen oder Wiederholungen.
Dieser werden eigenständig gelesen, da sie in den aktuellen Quelldaten nicht mehr vorhanden sind.
Diese Option steht nur zur Verfügung, wenn beide Prozesse identische Quell-Verbindungen und Quell-Objekte haben.

"Prozess direkt mit Zieldaten aus Vorgänger ausführen" startet den Prozess mit den zwischengespeicherten Daten.
Der Prozess führt keine eigene Datenabfrage aus, mit Ausnahme von ggf. konfigurierten Fehlerwiederholungen oder Wiederholungen.
Dieser werden eigenständig gelesen, da sie in den aktuellen Zieldaten nicht mehr vorhanden sind.
Diese Option steht nur zur Verfügung, wenn beide Prozesse in Quell- und Zielverbindung, sowie Quell- und Zielobjekt
aufeinander abgestimmt sind.
Außerdem bleibt zu berücksichtigen, dass auch nicht jeder Prozess über vollständige Zieldaten verfügt.

"Prozess für jeden Quelldatensatz aus Vorgänger und einem ausgewerteten Filter ausführen" führt für jeden Quelldatensatz
eine modifizierte Datenabfrage aus und die gesammelten Daten werden verarbeitet.
Diese Funktion setzt die Definition eines Filters mit Platzhaltern in ##-Schreibweise voraus.
Auch können nicht alle Prozesse einen Filter auswerten. Dies ist meistens der Fall, wenn im Prozess auch kein Quellfilter 
definiert werden kann.
Bei dieser Option müssen Verbindungen und Objekte nicht aufeinander abgestimmt sein.

"Prozess für jeden Zieldatensatz aus Vorgänger und einem ausgewerteten Filter ausführen" führt für jeden Zieldatensatz
eine modifizierte Datenabfrage aus und die gesammelten Daten werden verarbeitet.
Diese Funktion setzt die Definition eines Filters mit Platzhaltern in ##-Schreibweise voraus.
Auch können nicht alle Prozesse einen Filter auswerten. Dies ist meistens der Fall, wenn im Prozess auch kein Quellfilter 
definiert werden kann.
Bei dieser Option müssen Verbindungen und Objekte nicht aufeinander abgestimmt sein.

**Filter für Ausführung**

Dieser Wert übersteuert den Filter des Prozesses in der aktuellen Ausführung, wenn "Prozess manuell ausführen" eingestellt ist.
Nicht alle Prozesse können einen Filter auswerten. Dies ist meistens der Fall, wenn im Prozess auch kein Quellfilter 
definiert werden kann.
Außerdem definiert dies den Filter mit Platzhaltern für die Abfrage zu zwischengespeicherten Daten.
Der Syntax muss den Anforderungen der jeweiligen Quell-Verbindung genügen.
Sollte es sich um einen Abfrage-Prozess handelt, wird ggf. in der Abfrage der Platzhalter #FlowFilter# mit diesem Filter ersetzt.
Bei der Verarbeitung von zwischengespeicherten Daten wird die Abfrage für jeden Datensatz wiederholt.

**Bedingung für Ausführung**

Diese logische Bedingung in SQL-Notation wird je zwischengespeicherten Datensatz ausgeführt. Dabei werden ##-Platzhalter
mit den aktuellen Daten ersetzt.
Falls die Bedingung nicht erfüllt wird, wird der Datensatz übersprungen.

**Das Lesen der Quelldaten soll nicht mit dem Änderungsgrenzwert des Prozesses eingeschränkt werden**

Dies entspricht der Ausführungsoption "Immer alle Datensätze abfragen" eines Prozess und übersteuert diese Einstellung.

**Ablauf beenden, wenn der aktuelle Prozess keine Daten liefert**

Wenn der aktuelle Prozess keine Daten erhält, wird der Ablauf hier gestoppt.

**Fehlerbehandlung**

Generell kann eine Datensatz-bezogene Fehlerbehandlung am Prozess oder am Ablauf eingestellt werden.
Mit dieser Einstellung kann der Ablauf gestoppt werden, falls der Prozess nicht erfolgreich beendet wird.
Dies kann auch der Fall sein, falls die Vebrindungsprüfung bereits fehlschlägt.

Die Optionen sind "Ablauf abbrechen" und "Ablauf fortsetzen".

**Felder kopieren**

Mittels Feldnotation können hiermit Daten aus dem Zielobjekt in das zwischengespeicherte Quellobjekt übertragen werden.
Diese stehen dann in den folgenden Prozessen zur Verfügung und können z.B. mittels leerem Parameter nutzbar gemacht werden.

Ausführen eines Datendienstes
-----------------------------

Datendienste sind ein Werkzeug für die Generierung eines tabellenorientierten Berichts.
Diese könnten mit dem ERP-Fokus verwendet, zeitgesteuert gespeichert oder zeitgesteuert versendet werden.
Dieser Ablaufschritt ermöglicht das Versenden des Berichts als Email-Anhang.
Zusätzlich besteht die Möglichkeit den Emailinhalt festzulegen und zu personalisieren.
Die Fehlerbehandlung dieses Typs erfolgt über den Änderungsspeicher, auf den im Warteschlangendatensatz des Ablaufs
verwiesen wird. Je nach Einstellung werden dies Daten ausgelesen und für den Datendienst verwendet.

Folgende Parameter können in diesem Schritt definiert werden.

**Name**

Dieser Name wird den einzelnen Meldungen des ausgeführten Datendienstes vorangestellt.
Außerdem wird er als Email-Betreff verwendet, wenn keiner definiert wurde.

**Datendienst ausführen**

Hier wird der Datendienst für die Ausführung festgelegt. Dieser wird nicht zum Speichern von Daten ausgeführt,
sondern ausschließlich für den Versand eines Bericht, unabhängig von den Einstellungen des Datendienstes.

**Daten aus Vorgänger**

Hier wird ein Prozess aus den vorangegangenen Schritten ausgewählt, dessen Quell- oder Zieldaten im aktuellen
Datendienst verwendet werden sollen.
Sollte die Ausführungsart "Datendienst manuell ausführen" eingestellt sein, wird dieser Wert nicht benötigt.
Dann wird der Datendienst einmalig ausgeführt und versendet.

**Ausführungsart**

Dies steuert die Art der Datendienstausführung.

"Datendienst manuell ausführen" entspricht dabei einer normalen Ausführung für den Versand eines Berichts.
Die Abfrage des Datendienstes wird einmalig ausgeführt und das Resultat wird versendet.

"Datendienst für jeden Quelldatensatz aus Vorgänger und einer ausgewerteten Abfrage ausführen" führt für jeden Quelldatensatz
eine modifizierte Datenabfrage aus und die gesammelten Daten werden als Anhang versendet.
Diese Funktion setzt die Definition eines Filters mit Platzhaltern in ##-Schreibweise voraus.
Der Filter wird über den Platzhalter #FlowFilter# in die Datendienstabfrage eingefügt.

"Datendienst für jeden Zieldatensatz aus Vorgänger und einer ausgewerteten Abfrage ausführen" führt für jeden Zieldatensatz
eine modifizierte Datenabfrage aus und die gesammelten Daten werden als Anhang versendet.
Diese Funktion setzt die Definition eines Filters mit Platzhaltern in ##-Schreibweise voraus.
Der Filter wird über den Platzhalter #FlowFilter# in die Datendienstabfrage eingefügt.

**Bedingung für Ausführung**

Diese logische Bedingung in SQL-Notation wird je zwischengespeicherten Datensatz ausgeführt. Dabei werden ##-Platzhalter
mit den aktuellen Daten ersetzt.
Falls die Bedingung nicht erfüllt wird, wird der Datensatz übersprungen.

**Filter für Ausführung**

Dieser Wert wird für jeden Datensatz ausgewertet und über den Platzhalter #FlowFilter# in die Abfrage des Datendienstes
eingefügt.

**Ablauf beenden, wenn der aktuelle Datendienst keine Daten liefert**

Wenn die Abfrage des aktuellen Datendienstes keine Daten erhält, wird der Ablauf hier gestoppt.

**Empfängeradresse**

Empfänger des generierten Berichts. Mehrfachnennungen werden mit Semikolon getrennt.
#-Platzhalter werden für jeden Datensatz ersetzt. Dies gilt nicht für die manuelle Ausführung.

**CC Adresse**

Kopie-Empfänger des generierten Berichts. Mehrfachnennungen werden mit Semikolon getrennt.
#-Platzhalter werden für jeden Datensatz ersetzt. Dies gilt nicht für die manuelle Ausführung.

**BCC Adresse**

Blindkopie-Empfänger des generierten Berichts. Mehrfachnennungen werden mit Semikolon getrennt.
#-Platzhalter werden für jeden Datensatz ersetzt. Dies gilt nicht für die manuelle Ausführung.

**Betreff**

Betreff der generierten Email. #-Platzhalter werden für jeden Datensatz ausgewertet.

**Vorlage für Nachrichten**

Hier kann eine Html- oder Text-Vorlage aus den Serienbriefvorlagen ausgewählt werden.
Je nach Format der Vorlage wird dann eine Html- oder Text-Email versendet.
Bevor Sie diesen Wert auswählen können, muss die Vorlage über den Serienbriefbereich gespeichert werden.

**Email Verbindung**

Der Versand von Datendiensten kann nicht über den Syncler-Smtp erfolgen.
Es muss eine Email Verbindung mit Smtp-Angaben eingerichtet werden.
In der Email Verbindung wird auch der Absender für den Versand definiert.
Mit diesem Wert wählen Sie die gewünschte Verbindung aus.

**Fehlerbehandlung**

Mit dieser Einstellung kann der Ablauf gestoppt werden, falls der Datendienst nicht erfolgreich ausgeführt und versendet wird.
Die Optionen sind "Ablauf abbrechen" und "Ablauf fortsetzen".


Versand von E-Mails
-------------------

Der Versand von Emails kann bereits mit Prozessen realisiert werden.
Dieser Schritt vereinfacht das und bietet die Möglichkeit der einfachen Kombination.
Der Versand setzt immer das Vorhandensein von zwischengespeicherten Daten voraus.
Per Bedingung können einzelne Datensätze ausgeschlossen werden.
Für die restlichen Datensätze wird der Versand, ähnlich den Datendiensten, durchgeführt.
Die Fehlerbehandlung dieses Typs erfolgt über den Änderungsspeicher, auf den im Warteschlangendatensatz des Ablaufs
verwiesen wird. Je nach Einstellung werden dies Daten ausgelesen und für den Datendienst verwendet.

Folgende Parameter können in diesem Schritt definiert werden.

**Name**

Dieser Name wird den einzelnen Meldungen des Schrittes vorangestellt.
Außerdem wird er als Email-Betreff verwendet, wenn keiner definiert wurde.

**Daten aus Vorgänger**

Hier wird ein Prozess aus den vorangegangenen Schritten ausgewählt, dessen Quell- oder Zieldaten im aktuellen
Versand verwendet werden sollen.

**Ausführungsart**

Dies steuert die Art des Versands.

"Versand mit Quelldaten aus Vorgänger ausführen" startet den Versand mit den zwischengespeicherten Daten.

"Versand mit Zieldaten aus Vorgänger ausführen" startet den Versand mit den zwischengespeicherten Daten.

**Bedingung für Ausführung**

Diese logische Bedingung in SQL-Notation wird je zwischengespeicherten Datensatz ausgeführt. Dabei werden ##-Platzhalter
mit den aktuellen Daten ersetzt.
Falls die Bedingung nicht erfüllt wird, wird der Datensatz übersprungen.

**Empfängeradresse**

Empfänger der generierten Email. Mehrfachnennungen werden mit Semikolon getrennt.
#-Platzhalter werden für jeden Datensatz ersetzt.

**CC Adresse**

Kopie-Empfänger der generierten Email. Mehrfachnennungen werden mit Semikolon getrennt.
#-Platzhalter werden für jeden Datensatz ersetzt.

**BCC Adresse**

Blindkopie-Empfänger der generierten Email. Mehrfachnennungen werden mit Semikolon getrennt.
#-Platzhalter werden für jeden Datensatz ersetzt.

**Betreff**

Betreff der generierten Email. #-Platzhalter werden für jeden Datensatz ausgewertet.

**Vorlage für Nachrichten**

Hier kann eine Html- oder Text-Vorlage aus den Serienbriefvorlagen ausgewählt werden.
Je nach Format der Vorlage wird dann eine Html- oder Text-Email versendet.
Bevor Sie diesen Wert auswählen können, muss die Vorlage über den Serienbriefbereich gespeichert werden.

**Email Verbindung**

Der Versand von Emails kann nicht über den Syncler-Smtp erfolgen.
Es muss eine Email Verbindung mit Smtp-Angaben eingerichtet werden.
In der Email Verbindung wird auch der Absender für den Versand definiert.
Mit diesem Wert wählen Sie die gewünschte Verbindung aus.

**Fehlerbehandlung**

Mit dieser Einstellung kann der Ablauf gestoppt werden, falls der Versand nicht erfolgreich ausgeführt und versendet wird.
Die Optionen sind "Ablauf abbrechen" und "Ablauf fortsetzen".


Das Lesen von Quelldaten
------------------------

Die meisten Prozess sind für die Verarbeitung von Quelldaten und das Schreiben von Zieldaten ausgerichtet.
In einem Ablauf kann es aber auch die Aufgabe des reinen Lesens von Daten geben, da in den folgenden Schritten
auf diesen Pool zugegriffen wird oder das Schreiben der Quelldaten nicht im ersten Schritt erfolgen soll.
Für diesen Zweck kann ein Prozess definiert werden, der keine Feldzuordnungen enthält.
Oder es wird der Prozess "Universal Ablauf - Daten lesen" dafür eingerichtet.
Dieser Prozess verfügt über Parameter für das Lesen von Daten und kann diese auch transformieren.
Eine weitere Verarbeitung wird nicht ausgeführt.


Das könnte Sie interessieren.
:doc:`/bestpractices/flow_examples`
