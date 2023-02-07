Verknüpfungen zwischen Objekttypen im Universalprozess
======================================================

Wenn verschiedene Objekttypen zwischen System synchronisiert werden, müssen zwischen diesen unter Umständen auch Verknüpfungen übertragen werden.
Das kann zum Beispiel die Beziehung zwischen Firma und Kontakt oder zwischen Kontakt und Verkaufschance sein.
Die spezialisierten Prozesse leisten dies in der Regel automatisch und eine zusätzliche Konfiguration ist nicht erforderlich.
Bei der Übertragung von unbekannten Objekttypen oder Konstellation mit dem Universalprozess muss dies aber in die Konfiguration aufgenommen werden.

Grundlegend können dabei zwei Ansätze unterschieden werden.

Verknüpfungen auf der Basis von Datenabbildungen
------------------------------------------------

Wenn Objekttypen mit der Unterstützung von Datenabbildungen synchronisiert werden, steht bereits eine Abbildungsvorschrift von Quell-ID zu Ziel-ID zur Verfügung.
Bei bekannten Objekttypen mit einem Schema ist das auch die Regel.
Bei Prozessen für nicht reproduzierbaren Daten, sogenannte Abfrageprozesse, muss dies erst gezielt eingestellt werden.

Sobald eine Datenabbildung existiert, kann durch eine Transformation die ID für das Zielsystem ermittelt und als neues Feld bereitgestellt werden.
Dieses Feld wird dann dem Zielfeld zugeordnet.

Für die Einrichtung gehen Sie wie folgt vor.

Wechseln Sie in den Bereich Transformation und fügen Sie dort eine neue Transformation "Datenabbildung abfragen" hinzu.
Jeder Prozess legt eine eigenen Datenabbildung an.
Bei bidirektionalen Synchronisationen gibt es mindestens zwei Prozesse mit jeweils einer Datenabbildung.
Dabei sind die ID-Werte vertauscht, da diese nur anonym als Quell- und Ziel-ID behandelt werden.

Wählen Sie im Feld Prozess einen Prozess aus, der den zu verknüpfenden Objekttyp überträgt.
Nun können Sie festlegen, ob Sie die Quell- oder Ziel-ID des Prozesses für die Suche verwenden möchten.
Im Suchfeld tragen Sie nun einen Platzhalter für ein Quellfeld ein.
Dies sollte die ID des zu verknüpfenden Datensatzes aus dem Quellsystem enthalten.
Sie können nun noch einen Präfix für die abgefragten Daten definieren, damit diese besser lesbar sind.
Es werden automatisch drei Felder den Quelldaten hinzugefügt.
SourceId und TargetId enthalten die Quell- und Ziel-ID der Datenabbildung.
TargetIsDeleted ist ein Wahrheitswert, der durch Synchronisation gesetzt wird, falls das Ziel nicht mehr auffindbar ist.
Je nachdem welche Richtung der ausgewählte Prozess zwischen den Systemen beschreibt, enthält SourceId oder TargetId den Wert, den Sie dem Zielfeld zuordnen müssen.

Datenabbildungen enthalten nicht ausschließlich Feldwerte.
Bei System mit mehreren ID-Feldern je Datensatz ist der Wert die Feldnotation der ID-Felder.
Diese Transformation führt immer einen vollständigen Vergleich durch.
In diesem Fall muss der Suchwert der Feldnotation entsprechen und direkt mit mehreren Platzhalten konstruiert werden.

Der Weg über Datenabbildungen sollte bevorzugt werden, sofern er angewendet werden kann.
Es werden keine zusätzlichen Abfragen in den beteiligten Systemen ausgeführt und die Suche in der eigenen Datenbank ist auch performanter.
Außerdem erhalten Sie ein eindeutiges Ergebnis.


Verknüpfungen auf der Basis von Suchen
--------------------------------------

Wenn keine Datenabbildungen zur Verfügung stehen, kann die passende Ziel-ID auch auf der Basis eine Suche im Zielsystem ermittelt werden.
Dabei muss das Zielsystem aber auch entsprechende Suchen oder Abfragen unterstützen.

Es stehen zwei Transformationen für die Abfrage von Daten zur Verfügung.
Die Transformation "Daten abfragen" unterstützt eine Suche im aktuellem Quell- oder Zielsystem auf der Basis von Schemaobjekten.
Die Transformation "Abfrage ausführen" führt ein Abfrage-Statement mit einer beliebigen Verbindung aus. 
Diese Funktion ist vergleichbar mit einem Abfrageprozess, was vom jeweiligen System unterstützt werden muss.

Im Folgenden wird die Umsetzung mit der Transformation "Daten abfragen" beschrieben. 
Diese Variante ist einfacher und wird von den meisten Verbindungen unterstützt.
Sie müssen im Bereich "Verbindung" festlegen, ob die Suche im Quell- oder Zielsystem erfolgen soll.
In unserem Fall wollen wir eine ID für das Zielsystem ermitteln und suchen deshalb die Daten im Zielsystem.
Als nächstes wird unter "Tabelle" das Schema ausgewählt, mit dem gesucht werden soll.
Im Bereich "Filter" formulieren Sie eine für das System korrekte Suchbedingung.
Das kann ein SQL- oder OData-Syntax sein. Manche System wie zum Beispiel Zoho verwenden auch einen eigenen Syntax (siehe SearchRecord).
Da die Funktion nur einen Datensatz zurückliefert und die Suche unter Umständen mehrere Treffer generiert, kann mit "Sortieren nach" noch eine Reihenfolge festgelegt werden, sofern das System dies unterstützt.

Nun wählen Sie die Ergebnisspalten aus, die mit dem festgelegten Präfix in die Quelldaten aufgenommen werden.
Für eine Verknüpfung sollte hier das ID-Feld ausgewählt werden.

Diese Transformation ist hauptsächlich für die Anreicherung von Daten gedacht und für dieses Szenario unnötig aufwändig.
Zusätzliche Abfragen erhöhen die Ausführungsdauer und produzieren ggf. auch API-Verbräuche.
Außerdem besteht auch die Gefahr, dass die verwendete Suche keine eindeutigen Daten liefert.
Dies kann noch optimiert werden, indem die Quell-ID des verwendeten Objekttyps ebenfalls im Zielsystem als Referenz gespeichert wird.


Abhängigkeiten in der Ausführung
--------------------------------

Die beschriebenen Verfahren ermöglichen die Übertragung von Beziehungen sobald die entsprechenden Daten zur Verfügung stehen.
Da Prozesse aber meistens zeitgesteuert und unabhängig ausgeführt werden, ist dies nicht automatisch gewährleistet.

Falls die Firma später als die Kontakte übertragen wird, kann diese nicht verknüpft werden und eine nachträgliche Verknüpfung ist nicht oder nur erschwert möglich.
Deshalb sollten Sie für diesen Fall die Funktion der "Vorbedingung für Neuanlage" einsetzen.
Diese steht für die meisten Universal- und Abfrageprozesse zur Verfügung.

In diesem Feld wird eine logische Bedingung im SQL-Syntax formuliert, die Platzhalter für Quelldaten beinhalten kann und für jeden Datensatz einzeln ausgewertet wird.
Diese Bedingung prüft das abgerufene Feld auf einen vorhandenen Wert.

	'#GDM_TargetId#' <> ''

Sollte die Transformation keine Daten ermitteln können, ist das Feld leer und die Bedingung nicht erfüllt.
In diesem Fall wird der Datensatz zurückgestellt und in der nächsten Ausführung wiederholt.
Das funktioniert nur im Zusammenhang mit einer zeitgesteuerten Ausführung.
Die Anzahl an Wiederholungen wird mit dem Parameter "Maximale Anzahl an fortlaufenden Wiederholungen" eingestellt.
Nach Erreichen dieses Limits wird der Datensatz nicht weiter wiederholt, da davon ausgegangen wird, dass die Bedingung nicht erfüllbar ist.
Wählen Sie die Anzahl so, dass der betreffende Prozess den Datensatz für die Verknüpfung auch sicher übertragen kann.
Durch unterschiedliche Laufzeiten oder Intervalle in der Prozessausführung ist eine einmalige Wiederholung schnell überschritten.
