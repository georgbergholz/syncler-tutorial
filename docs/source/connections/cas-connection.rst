CAS genesisWorld und SmartWe
============================

Diese beiden CRM-Systeme können durch ihre fast identische REST API mit dem selben Plugin angesteuert werden.
Schema-basierte und Abfrage-basierte Datenzugriffe werden über die REST API implementiert.
Für Abfragen wird der spezifische SQL-Syntax von CAS verwendet, der zusätzliche Funktionen für Dossier, Verknüpfungen 
und Filter bereitstellt.

Es stehen spezifische Prozesse für die Synchronisation mit Sage b7, Microsoft Dynamics Business Central,
Sage 100, Sage X3 und Mailing-Anbietern inklusive Vorlagen zur Verfügung.
Weitere Systeme können per Universalprozesse angebunden werden.

Funktionen
----------

:Schema ermitteln:

    Das Schema der Verbindung wird über die REST API ermittelt.
    Basis sind die verfügbaren Datenobjekte.
    Zusätzlich wird das Schema noch für die Abfrage von Benutzern und Verknüpfungen erweitert.
    Das Schema für DOCUMENT und EMAILSTORE wird um das Feld FileContent erweitert. Base64 Daten, die 
    zugewiesen werden, werden in CAS abgelegt oder archiviert.
    Das Schema von APPOINTMENT, TODO und GWPHONECALL wird um die Listen LinkToAddress, LinkToGWOpportunity
    bzw. Participants erweitert. Speziell Participants ist dabei eine geschachtelte Liste.
    Diese Daten stehen auch beim Lesen zur Verfügung.
    Das Schema für GWOPPORTUNITY und BSVOUCHER wird um eine Positionsliste erweitert, die in der Sortierung
    die Gruppen berücksichtigt.
    Das Schema von GWDISTRIBUTION wird um eine geschachtelete Liste für ADDRESS-Verweise erweitert.

:Laden von Quelldaten:

    Mit Ausnahme von Einzeldaten werden alle Abfragen per query ausgeführt und ergänzt.
    Für genesisWorld wird das Statement um TEAMFILTER(Objektname; CASLOGGEDINUSER, CASPUBLICRECORDS, CASEXTERNALACCESS) 
    erweitert.
    Bei der Verwendung von Abfrage-Prozessen muss dies manuell erfolgen, da das Ergebnis ansonsten eine
    Vervielfälltigung der Daten sein kann.

:Laden von Schema-basierten Daten:

:Laden von Abfrage-basierten Daten:

:Schreiben von Daten:

:Schreiben von Bulk-Daten:


Einstellungen
-------------


Besonderheiten
--------------

Das Schema der verfügbaren Datenobjekte wird automatisch um die Objekte Permission, LinkTo und LinkFrom erweitert.
Diese unsortierten Listen bieten die Möglichkeit Berechtigungen und Verknüpfungen zu setzen oder Berechtigungen auszulesen.
Da es sich hier um 1:n verknüpfte Informationen handelt, die unsortiert bereitgestellt werden, müssen beim Lesen alle
Gruppen berücksichtigt werden.
Beim Aktualisieren von Berechtigungen wird über die RIGHTOWNERGGUID nach vorhandenen Zuordnungen gesucht. 
Die Verknüpfungen werden durch einen separaten API Aufruf festgelegt.

Das Zuweisen einer leeren Guid für Link-Ziele überspringt die Anlage.

Für die Archivierung von Emails kann das Objekt "EMAILSTORE" verwendet werden.
Dieses verfügt über ein Feld "FileContent". Wenn Sie dort eine Email im EML-Format als Base64 Zeichenkette zuweisen, wird die Email im CAS archiviert.
Die restlichen Felder können für zusätzliche Daten, wie z.B. Verknüpfungen verwendet werden.
Die Archivierung wird nur mit neuen Datensätzen ausgeführt. Sollte es sich um einen bekannten Datensatz handelt, wird die Archivierung übersprungen.

