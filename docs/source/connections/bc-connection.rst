Microsoft Dynamics Business Central
===================================

Microsoft Dynamics Business Central ist ein Warenwirtschaftssystem für kleine und mittlere Unternehmen.

Diese Verbindung unterstützt die bidirektionale Synchronisation von Entitäten der REST API, welche im ERP-System
konfiguriert werden können.

Die Synchronisation mit CRM-Systemen verwendet in der Regel die Kontakte als Basis.
Diese gehören nicht in allen Installationen zu den Standard-Endpunkten und müssen über eine API Page 
bereitgestellt werden.
Für eine Kombination mit Kundendaten werden die Kontakt-Geschäftsbeziehungen ebenfalls als Endpunkt benötigt.
Hier sind die Objektname "Contact" und "ContactBusinessRelation" durch die spezifischen Prozesse
vorgeschrieben.

Abfragen sind nur bei lokalen Installationen möglich und über SQL-Zugriffe implementiert.
Wenn Datendienste oder Abfrage-Prozesse zum Einsatz kommen sollen, müssen diese Zugangsdaten angegeben werden.
Dies kann auch mittels der Syncler-SQL-Bridge abgesichert werden. (:doc:`bridgeservice`)

Es stehen spezifische Prozesse für die Synchronisation mit Sage CRM und CAS inklusive Vorlagen zur Verfügung.
Dazu zählt auch die Anlage und Verknüpfung von Debitoren oder Kreditoren zu vorhandenen Kontakten.
Weitere Systeme und Entitäten können über Universalprozesse angebunden werden.


Funktionen
----------

:Schema ermitteln:

Das Schema der Verbindung wird über die REST API ermittelt.
Hierfür wird der $metadata Aufruf ausgeführt und ausgewertet.
Alle bereitgestellten Entitäten stehen für alle Operationen zur Verfügung.
Geschachtelte Daten stehen zu "salesquote", "salesorder", "purchaseinvoice" und "salesinvoice"
zur Verfügung.
Die Änderungsinformation zur Entität wird über den Feldnamen identifiziert.


:Lesen von Schema-basierten Daten:

Das Lesen von Datensätzen erfolgt über die REST API und wird durch die angegebene Firma eingeschränkt.
Zusätzlich können über den Prozess noch weitere Filter im OData-Syntax definiert werden.
Spezifische Prozesse unterscheiden automatisch Firmen- und Personenkontakte.
In Universalprozessen muss dies per Filter realisiert werden. Type eq 'Company'


:Lesen von Abfrage-basierten Daten:

Das Lesen von Abfrage-basierten Daten wird per SQL-Verbindung realisiert.


:Schreiben von Daten:

Das Schreiben von Datensätzen erfolgt über die REST API und wird durch die angegebene Firma eingeschränkt.
Das Löschen von Datensätzen wird unterstützt.
Das Speichern von Positionen in geschachtelten Daten erfolgt mit separaten Aufrufen.


:Schreiben von Bulk-Daten:

Diese Funktion wird nicht unterstützt.


Einstellungen
-------------

Folgende Einstellungen müssen bereitgestellt werden.

:API Basis-URL:

Die Basis-URL für die REST API.
Die Version muss hier angegeben werden. 
Sollten weitere Endpunkte angelegt werden, müssen diese der selben API Version zugeordnet werden.

.. code-block:: none

    http://<Server>:<WebServicePort>/<ServerInstance>/api/v1.0

:Benutzername:

Dieser Wert gehört zu den Zugangsdaten.

:Passwort:

Dieser Wert gehört zu den Zugangsdaten.

:Firma:

Dies ist der Name des ERP-Mandanten.

:Kundennummer statt Kunden-ID als Schlüssel verwenden:

Bei Upgrades kann statt der ID-Variante noch die No-Variante für die Identifikation von Datensätzen im Einsatz sein.
Damit in diesem Fall eine Kundenverarbeitung möglich ist, muss dieser Parameter auf Ja gestellt werden.

:Artikelnummer statt Artikel-ID als Schlüssel verwenden:

Bei Upgrades kann statt der ID-Variante noch die No-Variante für die Identifikation von Datensätzen im Einsatz sein.
Damit in diesem Fall eine Artikelverarbeitung möglich ist, muss dieser Parameter auf Ja gestellt werden.

:Artikelkategorie Code statt Artikelkategorie-ID als Schlüssel verwenden:

Bei Upgrades kann statt der ID-Variante noch die No-Variante für die Identifikation von Datensätzen im Einsatz sein.
Damit in diesem Fall eine Artikelgruppenverarbeitung möglich ist, muss dieser Parameter auf Ja gestellt werden.

:Belegnummer statt Beleg-ID als Schlüssel verwenden:

Bei Upgrades kann statt der ID-Variante noch die No-Variante für die Identifikation von Datensätzen im Einsatz sein.
Damit in diesem Fall eine Belegverarbeitung möglich ist, muss dieser Parameter auf Ja gestellt werden.

