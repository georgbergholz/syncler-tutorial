Die Entwicklung eines Verbindungsplugins in .Net
================================================

Jedes Verbindungsplugin wird durch eine Klasse implementiert, die von ConnectionBase ableitet.
Die Klasse wird in einer .Net Bibliothek entwickelt, die das SynclerCommon Assembly einbindet.
Bereitgestellt wird die DLL der Bibliothek in den connections Verzeichnissen der Installation.
Diese werden nur beim Start des Systems eingelesen.

In der Basisklasse werden virtuelle Methoden definiert, die in den Verbindungsplugins individuell implementiert werden.
Diese Methoden dienen der Steuerung des Verbindungsplugins.
Bei der Planung eines Verbindungsplugins müssen diese Berührungspunkte mit der Syncler Umgebung berücksichtigt werden.

Auch stehen Eigenschaften bereit, die verwendet werden könnnen.
Unter anderen werden Objekte für den Zugriff auf die Konfiguration, die aktuelle Datenbank und Übersetzungen bereitgestellt.


Die Benutzeroberfläche für die Konfiguration der Verbindung wird durch Attribute an der Klasse und den Eigenschaften definiert.
Die Page-Attribute an der Klasse aktivieren bestimmte Konfigurationsseiten.
Mit 'PageCommon' wird die Konfiguration von Eigenschaften aktiviert.
Eigenschaften können mit Attributen beschriftet und kategorisiert werden.
Auch Anleitungstexte lassen sich so platzieren.
Für alle Texte können Übersetzungscodes aus den erweiterbaren XML-Übersetzungsdateien genutzt werden.

* LocalizedCategory: übersetzte Kategorie
* LocalizedDisplayName: übersetzte Beschriftung
* LocalizedDescription: übersetzte Anleitung

Mit weiteren Attributen kann die Konfiguration noch detailierter definiert werden.

* CommaSeparatedValues: komma-separierte Daten
* JsonFormat: Legt ein Schema für JSON-Daten fest
* KeyValueList: Liste von Name-Wert-Paaren in Feldnotation
* LocalizedEnumDescription: für die Übersetzung von Enumerations
* Multiline: mehrzeiliger Wert
* OnlyMaster: Eigenschaft steht nur On-premises zur Verfügung
* Required: Es muss ein Wert festgelegt werden
* RequiresSchemaRefresh: Eine Änderung erzwingt ein Schema-Refresh




-------


folgendes kann implementiert werden.
die konfiguration basiert auf eigenschaften und seiten.
mit page attributen an der klasse werden die angezeigten formulare festgelegt.
alle eigenschaften können mit attributen für die allgemeine konfiguration vorbereitet werden.
die validierung der konfiguration und der startbedingungen werden mit der validate methode umgesetzt. diese wird beim speichern und bei jedem prozessstart ausgeführt. eine zurückgegebene null steht für ein positives resultat. eine zurückgegebene exception bricht die aktion ab und liefert die fehlermeldung zurück.
die validate methode wird bei direkten getdate, getquerydata oder setdata aufrufen nicht automatisch ausgeführt.