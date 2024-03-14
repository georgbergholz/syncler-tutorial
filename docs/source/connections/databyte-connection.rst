Databyte
========

Databyte ist eine Informationsplattform für detaillierte Firmendaten.
Mit dieser Verbindung stehen verschiedene Funktionen der Plattform zur Verfügung, die im Folgenden beschrieben werden.

Die Verbindung erzeugt Auswahllisten und Schemaobjekte für die Bedienung.

Schemaobjekte
-------------

:companylist:

Dieses Objekt wird für Firmenlisten verwendet. Damit können vorhandene Firmenlisten abgerufen, angelegt, umbenannt oder gelöscht werden.

:companylist_copy:

Mit diesem Objekt kann eine vorhandene Firmenliste kopiert werden. 
Dazu wird der Wert "fls" mit der ID der Quelle geschrieben und die Antwort enthält die ID der Kopie im Feld "newfls".

:companylist_data:

Mit diesem Objekt wird auf den Inhalt einer Firmenliste zugegriffen.
Für das Lesen muss die ID einer Firmenliste als Filter übergeben werden.
Als Antwort wird eine Liste der Firmen-IDs im Feld "data" zurückgegeben.
Der Inhalt einer Firmenliste kann für die Überwachung von Änderungen verwendet werden.

Dieses Objekt kann auch zum hinzufügen von Firmen zu einer Liste genutzt werden.
Dafür wird das Objekt zum Schreiben verwendet.
Mit dem Feld "ssid" können Sie sich auf eine vorherige Suchanfrage beziehen.
Mit dem Feld "umfang" steuern Sie, welche Firmen hinzugefügt werden sollen.
Der Wert "2" erwartet einen Bereich mit "von" - "bis" aus dem Suchergebnis.
Der Wert "3" erwartet einen Bereich mit "bereich" für jeden x-ten Datensatz.
Der Wert "4" arbeitet unabhängig von einer Suche und fügt alle Firmen aus dem Feld "firmen" der Liste hinzu.
Alle anderen Werte fügen das gesamte Suchergebnis der Liste hinzu.

Ein Lösch-Operation leert die Liste.

:companylist_truncate:

Mit diesem Objekt kann eine vorhandene Firmenliste geleert werden. 
Dazu wird der Wert "fls" mit der ID der Liste geschrieben.

:datamatch:

Mit diesem Objekt können vorhandene Projekte abgerufen oder neue Projekte angelegt werden.
Außerdem können vorhandene Projekte gelöscht werden.
Wird das Filtern oder Suchen mit den Standard-Prozessfeldern ausgelöst, wird der Wert direkt mit dem Names des
Projektes verglichen und alle Übereinstimmungen werden zurückgegeben.


:datamatch_data:

Mit diesem Objekt werden Vergleichsdatensätze zu einem Projekt hinzugefügt.
Dieses Objekt kann mit Prozessen für die Massenverarbeitung eingesetzt werden.
Damit können bis zu 500 Datensätze mit einem Aufruf übertragen werden.

Wird dieses Objekt gelesen, ist eine Projekt-ID als Filter erforderlich.
Sollte das Projekt noch nicht gestartet sein, wird das Lesen mit einer Fehlermeldung abgebrochen.
Sollte das Projekt bereits gestartet, aber noch nicht abgeschlossen sein, 
wird der Projektstatus alle 10 Sekunden geprüft, bis das Projekt abgeschlossen und das Ergebnis abgerufen werden kann.
Dies kann manuell abgebrochen werden.

Ein vorhandenes Resultat kann nur einmalig abgerufen werden. 
Danach wird das Projekt automatisch entfernt.
Damit die Daten möglichst flexibel zur Verfügung stehen, wird das Resultat in einzelnen Datensätzen im Änderungsspeicher abgelegt.
Dies ermöglicht ein wiederholtes Lesen durch den Prozess.
Jeder Datensatz enthält dabei das Match-Ergebnis und ggf. eine Ziel-ID für die weitere Verarbeitung.
Die Datensätze werden dem aktuellem Prozess zugeordnet und zurückgegeben.

Das kunde_id sollte mit Ihrer externen ID gefüllt werden, damit eine Ergebniszuordnung sichergestellt ist.

:datamatch_start:

Dieses Objekt startet die Projektverarbeitung.
Durch das Speichern der Projekt-ID beginnt die Verarbeitung.

:datamatch_abort:

Dieses Objekt stoppt die Projektverarbeitung.
Durch das Speichern der Projekt-ID wird die Verarbeitung abgebrochen.

:searchrequest:

Mit diesem Schema wird eine Suchanfrage formuliert und übertragen.
Die Suche wird durch das Schreiben des Objektes ausgelöst.
Das Ergebnis wird im Änderungsspeicher abgelegt und kann über die generierte ID "ssid" wieder abgerufen werden.
Hierfür wird das Schmea mit einem Filter gelesen.

:exportrequest:

Dieses Objekt fordert durch das Schreiben einen Export an.
Dieser Export wird vom Kontingent der Download-Einheiten abgezogen.
Ähnlich dem Hinzufügen von Daten zu einer Firmenliste, stehen verschiedene Optionen für die Auswahl der Exportdaten zur Verfügung.

Der Parameter "export" steuert die Informationstiefe des Exports. Abhängig von dem übergebenen Wert werden die exportierten Daten unter einem
anderen Zielschema im Änderungsspeicher abgelegt. Gültige Werte sind std, erw und pro.

Mit dem Feld "ssid" können Sie sich auf eine vorherige Suchanfrage beziehen.
Mit dem Feld "umfang" steuern Sie, welche Firmen exportiert werden sollen.
Der Wert "2" erwartet einen Bereich mit "von" - "bis" aus dem Suchergebnis.
Der Wert "3" erwartet einen Bereich mit "bereich" für jeden x-ten Datensatz.
Der Wert "4" arbeitet unabhängig von einer Suche und fügt alle Firmen aus dem Feld "firmen" der Liste hinzu.
Alle anderen Werte fügen das gesamte Suchergebnis der Liste hinzu.

Weitere Parameter sind:

* person: Anzahl Personen die pro Datensatz exportiert werden sollen (z.B. 0,1)
* zusatz: z.B. passive und schwebende Firmen mit exportieren

:exportstd:

Ein angeforderter Export mit dem Typ "std" wird unter diesem Schema im Änderungsspeicher abgelegt.
Das Lesen des Typs greift auf den Änderungsspeicher zu und liest einzelne oder alle Datensätze.
Der Prozess wird dabei nicht eingeschränkt.

:exporterw:

Ein angeforderter Export mit dem Typ "erw" wird unter diesem Schema im Änderungsspeicher abgelegt.
Das Lesen des Typs greift auf den Änderungsspeicher zu und liest einzelne oder alle Datensätze.
Der Prozess wird dabei nicht eingeschränkt.

:exportpro:

Ein angeforderter Export mit dem Typ "pro" wird unter diesem Schema im Änderungsspeicher abgelegt.
Das Lesen des Typs greift auf den Änderungsspeicher zu und liest einzelne oder alle Datensätze.
Der Prozess wird dabei nicht eingeschränkt.

:monitoringrequest:

Zum Anfordern oder Abbestellen einer Überwachung wird dieses Schema schreibend verwendet.
Überwachungen stehen im Zusammenhang zu Firmenlisten.
Beim Einlesen des Verbindungsschemas kann eine Firmenliste angegeben werden oder es wird eine bestimmt.
Zu dieser Liste werden die verfügbaren Monitor-Eigenschaften ermittelt und als Auswahlliste abgespeichert.
Die Werte dieser Auswahlliste werden als Liste mit dem Parameter "merkmale" übergeben.
Zusätzlich muss eine Firmenliste, ein Intervall und das Aktiv-Kennzeichen gesetzt werden.

:postbox:

Alle Überwachungen senden ggf. eine Nachricht in die Postbox, sobald eine Änderung zu einem Merkmal erkannt wurde.
Jede Nachricht kann eine Liste von Merkmalen und Firmen enthalten.
Diese Daten werden geschachtelt bereitgestellt.
Außerdem steht eine Zusammenstellung aller betroffenen Firmen-IDs bereit.

Wenn eine Nachricht mit dem Parameter "confirm" gespeichert wird, gilt sie als bestätigt und wird nicht erneut gelesen.


Die Suche nach Firmen
---------------------

Für die Suche nach Firmen wird das Schemaobjekt "searchrequest" verwendet.
Die Suche ist hier als Auftrag und nicht als Lesen von Daten umgesetzt.
Dies hat den Vorteil, dass komplexe Suchanfragen einfach durch Feldzuordnungen formuliert werden können.
Nutzen Sie das Schemaobjekt "searchrequest" zum Schreiben z.B. mittels eines Universalprozesses.

Das Objekt verfügt über verschiedene Bereich, wie firma, anschrift oder branche.
Jeder Bereich ist mehrfach vorhanden. Eine Zuordnung in verschiedenen Instanzen wird als Oder-Suche interpretiert.
Zuordnungen innerhalb eines Bereiches sind Und-verknüpft.
Verschiedene Bereiche sind ebenfalls Und-verknüpft.

Ordnen Sie "firma.1.firma" den gewünschten Suchnamen zu.
Ordnen Sie "anschrift.1.ort" und "anschrift.2.ort" jeweils einen Stadtnamen zu.
Das Resultat ist eine Suche des Firmennamen in beiden Orten (Oder-Beziehung).

Das Ergebnis der Suche wird im Änderungsspeicher abgelegt und kann von dort durch einen Folgeprozess oder Ablaufschritt verarbeitet werden.
Es wird ein geschachteltes Objekt gespeichert, mit den gekürzten Firmendaten als Liste.
Mit der "ssid" kann das Suchergebnis für Firmenlisten oder Exporte verwendet werden.
Außerdem werden alle IDs der gefundenen Firmen als Feld bereitgestellt.


Hinzufügen von Firmen zu einer Liste
------------------------------------

Um Firmen einer Firmenliste hinzuzufügen wird das Schemaobjekt "companylist_data" schreibend verwendet.
Die Quelle der Daten kann eine vorangegangene Suche oder eine vorhandene Auflistung von Firmen-IDs sein.

Mit dem Feld "ssid" können Sie sich auf eine vorherige Suchanfrage beziehen.
Mit dem Feld "umfang" steuern Sie, welche Firmen hinzugefügt werden sollen.
Der Wert "2" erwartet einen Bereich mit "von" - "bis" aus dem Suchergebnis.
Der Wert "3" erwartet einen Bereich mit "bereich" für jeden x-ten Datensatz.
Der Wert "4" arbeitet unabhängig von einer Suche und fügt alle Firmen aus dem Feld "firmen" der Liste hinzu.
Alle anderen Werte fügen das gesamte Suchergebnis der Liste hinzu.

Kombinieren Sie zwei Prozesse innerhalb eines Ablaufes.
Der erste Prozess führt eine Suche aus. (siehe "Die Suche nach Firmen")
Es kann sich um einen Universalprozess mit individueller Datenquelle oder um einen reinen Schreibprozess handelt, 
wo die Suchkriterien im Prozess definiert werden.

Der zweite Prozess ist ein Universalprozess mit "searchrequest" als Quelle und "companylist_data" als Ziel.
Mittels Parameter und Feldzuordnungen können Sie die gewünschte Datenübernahme definieren.

Der Ablauf führt den ersten Prozess manuell aus.
Der zweite Prozess wird mit den Zieldaten des Vorgängers ausgeführt. Diese entsprechen dem Ergebnis der Suchanfrage.
Nach Abschluss des Ablaufs ist die Suche der Firmenliste hinzugefügt worden.

Zur Auswahl der Firmenliste ist die ID einer Liste erforderlich.
Diese kann fest per Transformation oder durch andere Vorgängerprozesse bereitgestellt werden.


Der Export von Firmen und Übertragung in ein externes System
------------------------------------------------------------

Ähnlich wie dem Hinzufügen von Daten zu einer Firmenliste muss dem Export eine Auswahl von Daten vorangehen.
Hier besteht ebenfalls die Möglichkeit eine Suche auszuführen oder ein Suchergebnis zu verwenden.
Es kann aber auch direkt mit einer ID-Liste gearbeitet werden, die z.B. durch ein externes System vorgehalten wird.
Ebenso kann die ID-Liste einer Überwachungsnachricht zu Änderungen an Merkmalen entnommen werden.

In diesem Beispiel soll eine Suchanfrage genutzt werden.

Kombinieren Sie drei Prozesse innerhalb eines Ablaufes.
Der erste Prozess führt eine Suche aus. (siehe "Die Suche nach Firmen")
Es kann sich um einen Universalprozess mit individueller Datenquelle oder um einen reinen Schreibprozess handelt, 
wo die Suchkriterien im Prozess definiert werden.

Der zweite Prozess ist ein Universalprozess mit "searchrequest" als Quelle und "exportrequest" als Ziel.
Mittels Parameter und Feldzuordnungen können Sie die gewünschte Datenübernahme definieren.

Mit dem Feld "ssid" können Sie sich auf eine vorherige Suchanfrage beziehen.
Mit dem Feld "umfang" steuern Sie, welche Firmen hinzugefügt werden sollen.
Der Wert "2" erwartet einen Bereich mit "von" - "bis" aus dem Suchergebnis.
Der Wert "3" erwartet einen Bereich mit "bereich" für jeden x-ten Datensatz.
Der Wert "4" arbeitet unabhängig von einer Suche und fügt alle Firmen aus dem Feld "firmen" der Liste hinzu.
Alle anderen Werte fügen das gesamte Suchergebnis der Liste hinzu.

Zusätzlich muss noch die Informationstiefe mit "export" festgelegt werden.
Dies entscheidet darüber, mit welchem Quellschema im dritten Schritt gearbeitet wird.

Das Resultat des zweiten Prozesses sind exportierte Datensätze im Änderungsspeicher.
Der dritte Prozess auf der Basis eines Universalprozesses hat als Quelle das festgelegte Exportschema und als Ziel
ein beliebiges externes System.


Eine Data-Match mit vorhandenen Daten
-------------------------------------

Neben der Suche nach Firmen mittels Kriterien kann auch ein Abgleich mit Ihren Daten erfolgen.
Diese werden in der Firmendatenbank gesucht und als Reultat wird eine oder mehrere potetnielle Treffer zurückgeliefert.
Mit den so generierten ID-Abbildungen können Firmenliste gefüllt oder Export zur Anreicherung und Aktualisierung Ihres
Datenbestandes durchgeführt werden.

Wir unterteilen das Beispiel in zwei Bereiche. Der erste hier beschriebene Bereich beschreibt die Durchführung des Data-Matchings 
bis zum Erhalt der IDs.
Der zweite Bereichsind Folgeaktivitäten, die bereits im vorangegangenen beschrieben wurden.

Für das Data-Matching kombinieren wir 4 Prozesse in einem Ablauf.
Die Anzahl ist hier höher, da kleiner Zwischenschritte notwendig sind.

Der erste Prozess kann ein Universalprozess oder Schreibprozess sein. Seine Aufgabe ist die Anlage eines neuen Projektes.
Projekte sind der Rahmen des Data-Matchs und werden nach Abschluss automatisch wieder entfernt.
Als Ziel wird das Schema "datamatch" verwendet. Es muss ein Name und ein Typ für die Art des Vergleichs angegeben werden.
Durch das Schreiben wird eine ID generiert, die in den folgenden Schritt benötigt wird.
Deshalb muss dieser Wert im Ablaufschritt in die Quelldaten übernommen werden.

Der zweite Prozess überträgt die Stammdaten aus Ihrem System. Als Ziel wird das Schema "datamatch_data" verwendet.
Dieses wird auch in Bulk-Prozessen unterstützt, was die Übertragung deutlich beschleunigt.
Sie müssen in diesem Prozess mindestens den Firmennamen und die Anschrift übermitteln.
Die "kunde_id" Spalte können Sie für Ihre System-ID verwenden, damit Sie die Resultate später zuordnen können.
Auch die Projekt-ID muss hier zugeordnet werden. Mittels Parameter und Abfrage-Platzhalter kann diese im Ablauf übernommen werden.

Nachdem alle Daten in das Projekt übertragen wurden, muss dieses gestartet werden, damit der Abgleich durchgeführt wird.
Für diese Aktion steht das Schema "datamatch_start" zur Verfügung. Durch eine Schreibaktion mit der Projekt-ID wird der Vorgang gestartet.
Abhängig von der Anzahl der Daten und ggf. Projekten benötigt der mehrere Minuten für die Durchführung.

Der vierte Prozess verwendet das Schema "datamatch_data" zum Lesen und muss hierfür die Projekt-ID als Filter übergeben.
Das Lesen der Daten wartet auf den Abschluss des Projektes. Dieser wird alle 10 Sekunden geprüft, bis das Projekt abgeschlossen wurde.
Nach Abschluss werden die Daten mit dem Match-Ergebnis abgerufen und in den Änderungsspeicher mit einem Prozessbezug gespeichert.
Dieser Abruf ist nur einmal möglich. Ein erneutes Lesen wird nur die Daten aus dem Änderungsspeicher liefern.
Der vierte Prozess kann nun die generierten IDs zurück in Ihr System schreiben und Sie können diese für Folgeaktivitäten nutzen.

Nur der erste Prozess wird im Ablauf manuell ausgeführt.
Der Prozess für die Datenübertragung benötigt die Projekt-ID. Bei einer manuellen Ausführung muss diese extern bereitstehen.
Sie können den Prozess aber auch mit den Vorgängerdaten als Filter nutzen, um die ID im Ablauf zu übergeben.
Der Projektstart kann direkt die Daten des ersten Prozesses wiederverwenden.
Der letzte Prozess verwendet die Daten des ersten als Filter, damit das Projekt gezielt abgerufen werden kann.

Das Überwachen von Merkmalsänderungen
-------------------------------------

Die Basis dieser Überwachung ist eine gefüllte Firmenliste. Der Weg dorthin ist oben bereits beschrieben.
Als nächstes müssen die Merkmale einmalig abonniert werden.
Verwenden Sie dafür die Angaben aus der Auswahlliste "Monitoring" und das Schema "monitoringrequest".
Sobald die gewünschten Merkmale aktiviert wurden, kann ein Prozess für das Abrufen der Nachrichten eingerichtet werden.
Das kleinste Intervall der Überwachung ist ein Tag.

Verwenden Sie als Quellschema "postbox". Da die Nachricht bereits eine vollständige ID-Liste enthält, kann als Zielschema bereits ein "exportrequest" eingestellt werden.
Damit eine Nachricht nur einmal verarbeitet wird, nutzen Sie die Rückschreiben-Funktion und übergeben ein "true" für das Feld "confirm".
Das Schreiben des "exportrequest" füllt wieder den Änderungsspeicher, welcher dann mit einem weiteren Prozess abgearbeitet wird.


