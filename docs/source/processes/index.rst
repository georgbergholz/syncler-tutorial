Prozesse
----

Ein Prozess f�hrt eine Aufgabe aus, z.B. das �bertragen oder Synchronisieren von Daten.
Dabei k�nnen zwei Formen unterschieden werden. Der Schema-basierte und der Abfrage-basierte Prozess.
Der Prozess speichert alle Einstellungen, Transformationen und Feldzuordnung f�r eine Richtung zwischen zwei beteiligten Verbindungen.
Der Syncler sieht auch nicht genau einen Prozess f�r eine �bertragungsrichtung vor, sondern unterst�tzt eine beliebige Anzahl von Prozessen. 
Jeder Prozess wird dabei separat konfiguriert und ausgef�hrt und kann mit den anderen Prozessen indirekt �ber die Datenabbildungen interagieren, um z.B. ein Konfliktverhalten zu definieren. 
Dabei k�nnen diese Prozesse den Datenbestand separieren oder die Synchronisation erg�nzen. 
Im Fall des Erg�nzens werden zwei verkn�pfte Datens�tze mit mehreren Prozessen synchronisiert.

Es gibt z.B. Prozessvorlage f�r die Umsatz-Aktualisierung. 
In den meisten Systemen ist eine Umsatz�nderung keine �nderung der Stammdaten und l�st dadurch auch keine �nderungsgetriebene �bertragung aus. 
Damit aktuelle Umsatzzahlen angeboten werden k�nnen, �bertr�gt dieser Prozess ausschlie�lich die Umsatzzahlen f�r alle Datens�tze und erg�nzt damit die �nderungssynchronisation. 
Da das Schreiben der Umsatzzahlen eine �nderung im Zielsystem darstellt, aktualisieren Prozess die Synchronisationsinformationen von Datenabbildungen aus parallelen und komplement�ren Prozessen. 
Diese Interaktion f�hrt dazu, dass diese Prozesse ggf. keine (R�ck-) �bertragung ausf�hren oder es nicht zu falschen Konflikterkennungen kommt.

In folgenden Situationen ist eine Verteilung auf mehrere Prozesse sinnvoll.

Die bidirektionale Synchronisation ist asymmetrisch definiert.
Wenn die Feldzuordnungen zwischen den �bertragungsrichtungen abweichen, kann ein Konflikt zu inkonsistenten Daten f�hren.
Konflikte entstehen aus einer zeitgleichen �nderungen in verschiedenen Systemen und enden meist mit der Auswahl einer bestimmten �nderung und dem Verwerfen der anderen �nderung.
Damit nur einseitig synchronisierte Felder durch einen Konflikt nicht verworfen werden, kann die �bertragung dieser Felder in einen weiteren Prozess mit einer eigenen Konfliktbehandlung ausgelagert werden.

Sie ben�tigen in bestimmten Situationen unterschiedliche Filter.
Wenn z.B. der Sage CRM Account-Manager mit dem Vertreter in Sage 100 synchronisiert werden soll, aber keine Kontenanlage durch die Integration gew�nscht ist, ben�tigen Sie einen weiteren Prozess, der nur f�r Firmen mit bestehenden Kontokorrent dieses Feld zuordnet und �bertr�gt. 
Hier bietet sich ein Filter auf eine vorhandene Kontonummer an.

Sie ben�tigen in bestimmten Situationen unterschiedliche Parameter.
Jeder Prozess definiert eine Vielzahl von Parametern, die auch Datenobjekt-spezifisch sein k�nnen. 
Diese Parameter k�nnen w�hrend der Synchronisation nicht beeinflusst werden.


Schema-basierte Prozesse
----


Abfrage-basierte Prozesse
----

.. toctree::

    querybase
    querybulkbase

Synchronisationsprozesse f�r geschachtelte Daten
----


Ablauf-basierte Prozesse
----


Sonstige Prozesse
----

.. toctree::

    maintenance

Universalprozess oder spezifischer Prozess
----

Es gibt spezifische Prozesse unter den Plugins, die die System- und Objekttypen genau festlegen.
Diese Konstellation kann i.d.R. auch �ber den Universalprozess konfiguriert werden.
Die spezifischen Prozesse f�hren aber auch zus�tzliche Pr�fungen aus oder speichern weitere Daten, damit die Konsistenz im Zielsystem sichergestellt ist.
Sie sollten immer den spezifischen Prozess bevorzugt einrichten, damit es nicht zu inkonsistenten Zust�nden kommen kann.
Eine genaue Beschreibung, was der spezifische Prozess automatisch vorsieht, kann der jeweiligen Dokumentation entnommen werden.

Transformation im Detail
----

.. toctree::

    conversion/index

Prozesse im Detail
----

.. toctree::

    sync/inxmail
    sync/cas_bc

