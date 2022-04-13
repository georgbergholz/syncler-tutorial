Prozesse (Draft)
========

Ein Prozess realisiert eine Aufgabe, z.B. das Synchronisieren von Daten oder das Auslösen einer Benachrichtigung.
Dabei haben Prozesse je nach Einsatzgebiet unterschiedliche Parameter und Konfigurationsmöglichkeiten.
Diese Typen lassen sich grundlegend unterscheiden.

.. toctree::
    :titlesonly:
    
    schemabase
    querybase
    querybulkbase
    multichild
    flowbase

Es gibt auch noch weitere Prozesse, die nicht zu diesen Typen passen.

.. toctree::
    :titlesonly:
    
    maintenance
    msteams


Für eine Synchronisation speichert der Prozess alle Einstellungen, Transformationen und Feldzuordnungen für eine Richtung 
zwischen zwei beteiligten Verbindungen und Objekten.
Das Konzept sieht auch nicht genau einen Prozess für eine Übertragungsrichtung vor, sondern unterstützt eine beliebige Anzahl von Prozessen.
Jeder Prozess wird dabei separat konfiguriert und ausgeführt und kann mit den anderen Prozessen indirekt über die Datenabbildungen interagieren, 
um z.B. ein Konfliktverhalten zu definieren. 
Dabei können diese Prozesse den Datenbestand separieren oder die Synchronisation ergänzen. 
Im Fall des Ergänzens werden zwei verknüpfte Datensätze mit mehreren Prozessen synchronisiert.
Syncler übernimmt dabei die Orchestrierung der Prozesse.

Es gibt z.B. Prozessvorlage für die Umsatz-Aktualisierung. 
In den meisten Systemen ist eine Umsatzänderung keine Änderung der Stammdaten und löst dadurch auch keine änderungsgetriebene 
Übertragung aus. 
Damit aktuelle Umsatzzahlen angeboten werden können, überträgt dieser Prozess ausschließlich die Umsatzzahlen für alle Datensätze 
und ergänzt damit die Änderungssynchronisation. 
Da das Schreiben der Umsatzzahlen eine Änderung im Zielsystem darstellt, aktualisieren Prozess die Synchronisationsinformationen von 
Datenabbildungen aus parallelen und komplementären Prozessen. 
Diese Interaktion führt dazu, dass diese Prozesse ggf. keine (Rück-) Übertragung ausführen oder es nicht zu falschen Konflikterkennungen kommt.

In folgenden Situationen ist eine Verteilung auf mehrere Prozesse sinnvoll.

:Die bidirektionale Synchronisation ist asymmetrisch definiert:

Wenn die Feldzuordnungen zwischen den Übertragungsrichtungen abweichen, kann ein Konflikt zu inkonsistenten Daten führen.
Konflikte entstehen aus einer zeitgleichen Änderungen in verschiedenen Systemen und enden meist mit der Auswahl einer bestimmten Änderung und dem 
Verwerfen der anderen Änderung.
Damit nur einseitig synchronisierte Felder durch einen Konflikt nicht verworfen werden, kann die Übertragung dieser Felder in einen weiteren Prozess 
mit einer eigenen Konfliktbehandlung ausgelagert werden.

Dies kann auch mit einem Prozess und dem Speichern des Datensatzes in der Datenabbildung zusammen mit dem Konfliktverhalten "Nur Quelländerungen übertragen" 
realisiert werden. Dadurch werden aber auch mehr Daten in der Syncler Datenbank gespeichert, damit eine Änderungserkennung auf Feldebene möglich ist.

:Sie benötigen in bestimmten Situationen unterschiedliche Filter:

Wenn z.B. der Sage CRM Account-Manager mit dem Vertreter in Sage 100 synchronisiert werden soll, ist ein Kontokorrent erforderlich, da der Vertreter 
dort gespeichert wird. Wenn aber keine Kontenanlage durch die Integration gewünscht ist, 
benötigen Sie einen weiteren Prozess, der nur für Firmen mit bestehenden Kontokorrent dieses Feld zuordnet und überträgt. 
Hier bietet sich ein Filter auf eine vorhandene Kontonummer an.

:Sie benötigen in bestimmten Situationen unterschiedliche Parameter:

Jeder Prozess definiert eine Vielzahl von Parametern, die auch Datenobjekt-spezifisch sein können. 
Diese Parameter können während der Synchronisation nicht beeinflusst werden.


Universalprozess oder spezifischer Prozess
------------------------------------------

Es gibt spezifische Prozesse unter den Plugins, die die System- und Objekttypen genau festlegen.
Diese Konstellation kann i.d.R. auch über den Universalprozess konfiguriert werden.
Die spezifischen Prozesse führen aber auch zusätzliche Prüfungen aus oder speichern weitere Daten, damit die Konsistenz im Zielsystem sichergestellt ist.
Sie sollten immer den spezifischen Prozess bevorzugt einrichten, damit es nicht zu inkonsistenten Zuständen kommen kann.
Eine genaue Beschreibung, was der spezifische Prozess automatisch vorsieht, kann der jeweiligen Dokumentation entnommen werden.

Siehe Integrationsszenarien


