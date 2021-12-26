Syncler Elemente
====

Verbindungen, Prozesse und Datendienste sind die grundlegenden Elemente im Syncler für die Realisierung Ihrer Aufgaben.
Daneben gibt es noch weitere Elemente für die Koordination, Überwachung und Ausführung.

Verbindungen
----

Eine Verbindung stellt die Anbindung eines externen Systems oder Funktion bereit.
Sie speichert Zugangsdaten und Einstellungen und realisiert eine einheitliche Schnittstelle für andere Elemente des Synclers.
Neben klassischen System wie CRM oder ERP kann sich hinter einer Verbindung auch der Eingang für Daten, z.B. Push-Nachrichten oder Dateien
und der Ausgang von Daten, z.B. Serienbriefe verbergen.
Zu den Kernaufgaben zählt das Lesen von Daten, das Schreiben von Daten und das Ermitteln eines Datenschemas.
Beim Lesen von Daten können zwei Methoden unterschieden werden, die aber nicht jede Verbindung auch implementieren muss.
Daten können auf der Basis eines Schemas oder auf der Basis einer Abfrage gelesen werden.
Auch beim Speichern von Daten können zwei Methoden unterschieden werden, die ebenfalls nicht von jeder Verbindung bereitgestellt werden müssen.
Daten werden Schema-basiert einzeln oder als Bulk gespeichert.
Außerdem stellen manche Verbindungen zusätzliche Funktionen, wie z.B. eine Preisfindung bereit.
Durch das Speichern einer neuen Verbindung oder das Speichern einer bestehenden Verbindung mit aktivierter Checkbox "Schema aktualisieren" ruft der Syncler das Schema des Systems ab und speichert es in ihrer Syncler-Datenbank.
Dieses Datenschema ist die Arbeitsgrundlage für die Konfiguration von Schema-basierten Prozessen und wird aus Performance-Gründen zwischengespeichert.
Sollten Sie das Datenschema ändern, z.B. durch das Anlegen neuer Felder, müssen Sie diese Änderung über die Aktualisierung des Verbindungsschemas dem Syncler bekannt machen, damit Sie diese verwenden können.
Hier finden Sie weitere Informationen zu vorhandenen Verbindungsarten. :doc:`/connections/index`

Prozesse
----

Ein Prozess führt eine Aufgabe aus, z.B. das Übertragen oder Synchronisieren von Daten.
Dabei können zwei Formen unterschieden werden. Der Schema-basierte und der Abfrage-basierte Prozess.
Der Prozess speichert alle Einstellungen, Transformationen und Feldzuordnung für eine Richtung zwischen zwei beteiligten Verbindungen.
Der Syncler sieht auch nicht genau einen Prozess für eine Übertragungsrichtung vor, sondern unterstützt eine beliebige Anzahl von Prozessen. 
Jeder Prozess wird dabei separat konfiguriert und ausgeführt und kann mit den anderen Prozessen indirekt über die Datenabbildungen interagieren, um z.B. ein Konfliktverhalten zu definieren. 
Dabei können diese Prozesse den Datenbestand separieren oder die Synchronisation ergänzen. 
Im Fall des Ergänzens werden zwei verknüpfte Datensätze mit mehreren Prozessen synchronisiert.

Es gibt z.B. Prozessvorlage für die Umsatz-Aktualisierung. 
In den meisten Systemen ist eine Umsatzänderung keine Änderung der Stammdaten und löst dadurch auch keine änderungsgetriebene Übertragung aus. 
Damit aktuelle Umsatzzahlen angeboten werden können, überträgt dieser Prozess ausschließlich die Umsatzzahlen für alle Datensätze und ergänzt damit die Änderungssynchronisation. 
Da das Schreiben der Umsatzzahlen eine Änderung im Zielsystem darstellt, aktualisieren Prozess die Synchronisationsinformationen von Datenabbildungen aus parallelen und komplementären Prozessen. 
Diese Interaktion führt dazu, dass diese Prozesse ggf. keine (Rück-) Übertragung ausführen oder es nicht zu falschen Konflikterkennungen kommt.

In folgenden Situationen ist eine Verteilung auf mehrere Prozesse sinnvoll.

Die bidirektionale Synchronisation ist asymmetrisch definiert.
Wenn die Feldzuordnungen zwischen den Übertragungsrichtungen abweichen, kann ein Konflikt zu inkonsistenten Daten führen.
Konflikte entstehen aus einer zeitgleichen Änderungen in verschiedenen Systemen und enden meist mit der Auswahl einer bestimmten Änderung und dem Verwerfen der anderen Änderung.
Damit nur einseitig synchronisierte Felder durch einen Konflikt nicht verworfen werden, kann die Übertragung dieser Felder in einen weiteren Prozess mit einer eigenen Konfliktbehandlung ausgelagert werden.

Sie benötigen in bestimmten Situationen unterschiedliche Filter.
Wenn z.B. der Sage CRM Account-Manager mit dem Vertreter in Sage 100 synchronisiert werden soll, aber keine Kontenanlage durch die Integration gewünscht ist, benötigen Sie einen weiteren Prozess, der nur für Firmen mit bestehenden Kontokorrent dieses Feld zuordnet und überträgt. 
Hier bietet sich ein Filter auf eine vorhandene Kontonummer an.

Sie benötigen in bestimmten Situationen unterschiedliche Parameter.
Jeder Prozess definiert eine Vielzahl von Parametern, die auch Datenobjekt-spezifisch sein können. 
Diese Parameter können während der Synchronisation nicht beeinflusst werden.

Hier finden Sie weitere Informationen zu Prozessen und deren Verwendung. :doc:`/processes/index`

Datendienste
----

Ein Datendienst ist die Definition eines Berichtes und wird dazu verwendet, Informationen aus einem entfernten System aufzubereiten.
Datendienste können manuell durch eine Benutzer aufgerufen oder automatisch mit einer Warteschlange ausgeführt werden.
Dabei können die Informationen im Kontext einer Synchronisierung stehen, oder auch komplett unabhängig von der Synchronisation sein.
Die Ausführung eines Datendienstes kann das Resultat speichern oder per Email versenden.

Warteschlange
----

Die Ausführung von Prozessen oder Datendiensten wird mit einem Aktionseintrag in einer Warteschlange gestartet.
Es gibt jeweils eine Warteschlange für Prozesse und für Datendienste. 
Deren Abarbeitung kann separat über die Einstellungen gestartet oder gestoppt werden.

Warteschlangen werden kontinuierlich auf auzuführende Aktionen geprüft.
Nach der Ausführung bilden die Einträge ein Protokoll der jeweiligen Ausführung und speichern die gesammelten Statusinformation.
Für die Fehlerbehandlung werden historische Einträge auch genutzt, um fehlgeschlagene Verarbeitungen zu wiederholen.

Folgende Typen von Aktionen werden bei Prozessen unterschieden.

:Manuell:

Startet den Prozess einmalig mit den gleichen Parametern wie für eine zeitgesteuerte Ausführung.
Nachfolgerprozesse werden gestartet, aber eine Fehlerbehandlung über einen weiteren Aktionsdatensatz ist nicht vorgesehen.

:Einzelübertragung:

Startet die gezielte Verarbeitung eines Datensatzes durch den Prozess. 
Eine Fehlerwiederholung wird abhängig von der Konfiguration mit weiteren Aktionsdatensätzen realisiert.

:Geplant:

Ist die zeitgesteuerte Ausführung eines Prozesses. 
Die Anlage des nächsten geplanten Aktionsdatensatzes wird vom Prozess durchgeführt. 
Dieser berücksichtigt dabei die Einstellung zur Fehlerbehandlung.

:Nachfolger:

Bilden eine Prozesskette, wo der 1. Prozess die Zielmenge des folgenden Prozesses einschränkt. 
Dabei wird auf den Aktionsdatensatz des Vorgängers zugegriffen.

:Wiederholung:

Stellt eine Fehlerbehandlung dar, bei der aufgetretene Fehler die Ausführung sofort wiederholen soll. 
Die zeitliche Differenz beträgt dabei immer drei Minuten.

:Wiederherstellen:

Ruft die Rollback-Funktion eines Prozesses zu einen Sicherungsdatensatz auf. 
Diese Funktion steht nicht für alle Prozesse zur Verfügung.


Folgende Typen von Aktionen werden bei Datendiensten unterschieden.

:Manuell:

Startet den Datendienst einmalig mit den gleichen Parametern wie für eine zeitgesteuert Ausführung.

:Einzelübertragung:

Startet die Verarbeitung einer Datenabbildung durch den Datendienst.

:Geplant:

Ist die zeitgesteuerte Ausführung eines Datendienstes. 
Die Anlage des nächsten geplanten Aktionsdatensatzes wird vom Datendienst durchgeführt. 
Dieser berücksichtigt dabei die Einstellung zur Fehlerbehandlung.

:Wiederholung: 

Stellt eine Fehlerbehandlung dar, bei der aufgetretene Fehler die Ausführung sofort wiederholen soll. 
Die zeitliche Differenz beträgt dabei immer drei Minuten.


Protokolle
----

Verbindungen, Prozesse und Datendienste erzeugen Nachrichten, die in den Protokollen gespeichert werden.
Jede Nachricht verfügt über eine Einstufung und kann noch zusätzliche Daten enthalten.

Folgende Stufen werden unterschieden.

:Meldung:

Sind nicht kategorisierbare Nachrichten des Synclers.

:Fehler:

Sind Ausnahmen, unter denen die aktuelle Aufgabe nicht beendet werden konnte.

:Warnung:

Kennzeichnen anormale Situationen, in denen die aktuelle Aufgabe dennoch beendet werden kann. 
Manche dieser Situationen benötigen Vorgaben für die gewünschte Reaktion. Zum Beispiel: Konfliktmanagement

:Nachricht:

Wird bei Informationen für den Administrator eingesetzt. 

:Rückmeldung: 

Sind Ausgaben zum aktuellem Stand der Aufgabenbearbeitung.

:Debugging: 

Maximiert die Protokollierung bis hin zur kompletten Aufzeichnung von Inhalten der Kommunikation mit Endsystemen.
Diese Stufe wird nicht gespeichert, sondern nur im Monitoring ausgegeben.

Datenabbildungen
----

Für eine kontinuierliche Synchronisation von Datensätzen werden Datenabbildungen je Datensatz und Richtung angelegt.
Die Abbildungen speichern ID-Werte, Synchronisationsinformationen und können auch Kopien des Quelldatensatzes für eine genaue Änderungsanalyse enthalten.
Des weiteren werden Datenabbildungen für das Konfliktmanagement verwendet. 
Aus diesem Grund wird auch für jeden Prozess eine eigene Datenabbildung erzeugt, da die Prozesse keine direkte Beziehung untereinander haben. 
Die letzte Funktion ist die Verwaltung von Löschkennzeichen, die ein unerwünschtes erneutes Anlegen nach einer einseitigen Löschung vermeiden.

Der grundlegende Ablauf bei der Arbeit mit Datenabbildungen ist folgender.
Ein Prozess wird ausgeführt und wählt seine Quelldaten aus, die im Anschluss noch transformiert werden. 
Danach beginnt die Bearbeitung der einzelnen Datensätze. 
Zu jedem Quelldatensatz wird eine vorhandene Datenabbildung für diesen Prozess gesucht. 
Wenn dabei nichts gefunden wurde, wird die Suche auf parallele und komplementäre Prozesse ausgeweitet.
Diese Beziehung wird durch die verwendeten Verbindungen und die laufende Mandantennummer gebildet.
Sollte auch dies erfolglos sein, wird ggf. eine Übereinstimmungssuche ausgeführt. 
Wenn selbst diese kein Resultat liefert, geht der Syncler von einer Neuanlage aus und erzeugt ggf. eine neue Datenabbildung.

Sollte eine bestehende Abbildung für diesen Prozess gefunden werden, wird das Löschkennzeichen geprüft. 
Wenn dieses gesetzt ist, wird der Datensatz nicht weiter verarbeitet. 
Anderenfalls werden die Aktualisierungsinformationen, falls vorhanden, ausgewertet. 
Dabei wird zuerst die Quelle gegen die Aktualisierungsinformation der Quelle aus der Datenabbildung verglichen.

Falls diese identisch sind, wird davon ausgegangen, dass der Datensatz synchron ist und die Bearbeitung wird abgebrochen.
Dieser Mechanismus verhindert ein "Ping-Pong" der Prozesse, da eine Aktualisierung durch Prozess A als Auslöser für den komplementären Prozess B gilt.
Als nächstes wird die Datenabbildung mit dem Ziel verglichen. 
Sollte aus einem der Vergleiche ein Konflikt entstehen, wird die Konfliktlösung angewendet.
Sollte die Synchronisation durchgeführt werden, wird die eigene Datenabbildung aktualisiert. 
Abhängig von einer ggf. angewendeten Konfliktlösung werden auch parallele und komplementäre Datenabbildungen aktualisiert. 
Dies geschieht aber nur einseitig, damit diese Prozesse den Datensatz nicht als synchron behandeln und keinen Konflikt feststellen.

Änderungsspeicher
----

Der Änderungsspeicher ist ein Zwischenspeicher für Datensätze, die noch verarbeitet oder weiterverarbeitet werden müssen.
Abhängig von Prozess und Verbindung kommt der Änderungsspeicher auch in der Fehlerbehandlung oder verzögerten Übertragung zum Einsatz.

Datensatzsperren
----

Datensatzsperren werden bei der Verarbeitung erzeugt und dienen der Konfliktbehandlung.
Außerdem stellen sie die Aktualität von Daten sicher.
Sobald ein Datensatz verarbeitet wird, wird der Quelldatensatz gesperrt. 
Sollte diese Sperre bereits existieren und keine  oder neuere Änderungsinformtion enthalten, wird die Verarbeitung zurückgestellt.
Wenn es sich um eine Aktualisierung handelt, wird auch das Ziel gesperrt.
Sollte diese Sperre bereits existieren und keine  oder neuere Änderungsinformtion enthalten, wird die Verarbeitung zurückgestellt.
Nach Abschluss der Verarbeitung wird die Sperre mit den aktuellen Änderungsinformationen aktualisiert.
Dies ermöglicht es anderen Prozessen zu prüfen, ob ihre bereits gelesenen Daten noch aktuell sind.
Datensatzsperren bleiben über die Ausführung des Prozesses hinaus noch 60 Minuten gespeichert, damit die überkreuzte Ausführungen verschiedener Prozesse diese zur Verfügung hat.


Serienbrief Vorlagen
----

Für die Seriendruckfunktion können Vorlagen in der Datenbank verwaltet werden.
Durch einen Prozess oder die API kann bei Ausführung eines Seriendrucks diese Vorlage verwendet werden.
