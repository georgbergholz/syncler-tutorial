Microsoft Business Central
==========================

Die Anbindung von Business Central erfolgt �ber die REST API.
Die Integrationen verwenden in der Regel die Kontakte als Basis f�r die Synchronisation.
Diese geh�ren nicht in allen Installationen zu den Standard-Endpunkten und m�ssen �ber eine API Page bereitgestellt werden.
F�r eine Kombination mit Kundendaten werden die Kontakt-Gesch�ftsbeziehungen ebenfalls als Endpunkt ben�tigt.

Abfragen sind per SQL-Zugriff implementiert.
Wenn Datendienste oder Abfrage-Prozesse zum Einsatz kommen sollen, m�ssen diese Zugangsdaten angegeben werden.
Dies kann auch mittels der Syncler-SQL-Bridge abgesichert werden. (:doc:`bridgeservice`)


:API Basis-URL:

Die Basis-URL f�r die REST API.
Die Version muss hier angegeben werden. 
Sollten weitere Endpunkte angelegt werden, m�ssen diese der selben Version zugeordnet werden.

.. code-block:: none

    http://<Server>:<WebServicePort>/<ServerInstance>/api/v1.0

:Benutzername:

Dieser Wert geh�rt zu den Zugangsdaten.

:Passwort:

Dieser Wert geh�rt zu den Zugangsdaten.

:Firma:

Dies ist der Name des ERP-Mandanten.

:Kundennummer statt Kunden-ID als Schl�ssel verwenden:

Bei Upgrades kann statt der ID-Variante noch die No-Variante f�r die Identifikation von Datens�tzen im Einsatz sein.
Damit in diesem Fall eine Kundenverarbeitung m�glich ist, muss dieser Parameter auf Ja gestellt werden.

:Artikelnummer statt Artikel-ID als Schl�ssel verwenden:

Bei Upgrades kann statt der ID-Variante noch die No-Variante f�r die Identifikation von Datens�tzen im Einsatz sein.
Damit in diesem Fall eine Artikelverarbeitung m�glich ist, muss dieser Parameter auf Ja gestellt werden.

:Artikelkategorie Code statt Artikelkategorie-ID als Schl�ssel verwenden:

Bei Upgrades kann statt der ID-Variante noch die No-Variante f�r die Identifikation von Datens�tzen im Einsatz sein.
Damit in diesem Fall eine Artikelgruppenverarbeitung m�glich ist, muss dieser Parameter auf Ja gestellt werden.

:Belegnummer statt Beleg-ID als Schl�ssel verwenden:

Bei Upgrades kann statt der ID-Variante noch die No-Variante f�r die Identifikation von Datens�tzen im Einsatz sein.
Damit in diesem Fall eine Belegverarbeitung m�glich ist, muss dieser Parameter auf Ja gestellt werden.

