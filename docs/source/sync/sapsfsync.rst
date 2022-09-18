SAP IDoc und Salesforce (Draft)
=======================






Saleforce Verkaufschance nach SAP Orders
----------------------------------------

Für dieses Szenario steht ein eigener Prozess zur Verfügung, der die Verkaufschancen-Positionen auf die Angebotspositionen abbilden kann.
Hierbei steht eine spezielle Funktion zur Verfügung, die die Positionseinteilung des SAP Angebots erzeugt.
Positionen können per Parameter über den Produkt-Code gruppiert werden.
Die erste Produktzeile füllt dabei die Belegposition und alle Produktzeilen füllen die Einteilung der Belegposition.
Dabei ist es außerdem möglich vorher Summen zu bilden, damit diese der Belegposition zugeordnet werden können.
Dazu definiert man eine Liste von Feldern kommagetrennt in einem Parameter.
Die Feldbezeichung folgt dabei der Pfadangabe mit Punkt getrennt.
Die ermittelte Summe wird wieder der ersten Zeile zugeordnet, die für das Füllen der Belegposition verwendet wird.