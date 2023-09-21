Databyte
========

Databyte ist eine Informationsplattform für detailierte Firmendaten.
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

