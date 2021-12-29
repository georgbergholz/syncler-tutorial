Microsoft Business Central
==========================

Die Anbindung von Business Central erfolgt über die REST API.
Die Integrationen verwenden in der Regel die Kontakte als Basis für die Synchronisation.
Diese gehören nicht in allen Installationen zu den Standard-Endpunkten und müssen über eine API Page bereitgestellt werden.
Für eine Kombination mit Kundendaten werden die Kontakt-Geschäftsbeziehungen ebenfalls als Endpunkt benötigt.

Abfragen sind per SQL-Zugriff implementiert.
Wenn Datendienste oder Abfrage-Prozesse zum Einsatz kommen sollen, müssen diese Zugangsdaten angegeben werden.
Dies kann auch mittels der Syncler-SQL-Bridge abgesichert werden. (:doc:`bridgeservice`)


:API Basis-URL:

Die Basis-URL für die REST API.
Die Version muss hier angegeben werden. 
Sollten weitere Endpunkte angelegt werden, müssen diese der selben Version zugeordnet werden.

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

