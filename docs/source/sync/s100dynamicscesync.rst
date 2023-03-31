Microsoft Dynamics 365 CE - Sage 100
====================================

Für dieses Integrationsszenario stehen verschiedene Vorlage zur Verfügung, die den Universalprozess verwenden.
Für die Synchronisation der Verkaufspreise für Artikel wird ein spezieller Prozess verwendet, der die Besonderheit der Preislistenhierarchie auswertet und verarbeitet.


Sage 100 Adresse nach Dynamics Firma
------------------------------------

Diese Vorlage basiert auf dem Universalprozess und überträgt Adressen als Firmen.
Es sind bestimmte Standardfelder in der Transformation und Zuordnung enthalten.
Der Prozess filtert auf die Kategorie 0, was den Standard-Adressen entspricht.
Auch Kontokorrent-Felder werden teilweise zugeordnet, sofern vorhanden.
Zum Beispiel wird das Währungskennzeichen mit einer Abfrage auf die ID der Währung abgebildet.


Sage 100 Ansprechpartner nach Dynamics Kontakt
----------------------------------------------

Diese Vorlage basiert auf dem Universalprozess und überträgt Ansprechpartner als Kontakte.
Es sind bestimmte Standardfelder in der Transformation und Zuordnung enthalten.

Die Firmenzuordnung wird den Datenabbildungen des Adresse-Firmen-Prozesses entnommen.
Deshalb muss bei der ersten Einrichtung diese Transformation bearbeitet und der korrekte Prozess eingestellt werden.

Für die Kundenzuordnung wird die Firma als Ziel verwendet.
Außerdem werden Ansprechpartner wiederholt, sollte die Firma noch nicht übertragen worden sein.


Sage 100 Preisliste nach Dynamics Preisliste
--------------------------------------------

Diese Vorlage basiert auf dem Universalprozess und überträgt Preislisten als Preisebene.
Es sind bestimmte Standardfelder in der Transformation und Zuordnung enthalten.
Der Prozess filtert auf den Typ 0, was Standardpreislisten entspricht.
Diese Prozess wird für die Preisübertragung vorausgesetzt.


Sage 100 Artikel nach Dynamics Produkt
--------------------------------------

Diese Vorlage basiert auf dem Universalprozess und überträgt Artikel als Produkte.
Es sind bestimmte Standardfelder in der Transformation und Zuordnung enthalten.
Die Einheitengruppe und die Einheit werden ohne konkrete Einschränkung abgefragt, womit die Standarddatensätze zugeordnet werden.
Diese Transformationen müssen im Filter angepasst werden, wenn andere Zuordnungen gewünscht sind.
Diese Prozess wird für die Preisübertragung vorausgesetzt.


Sage 100 VK-Preis nach Dynamics Preis
-------------------------------------

Diese Vorlage basiert auf einem speziellen Prozess und überträgt Verkaufspreise als Preise.
Es sind bestimmte Standardfelder in der Transformation und Zuordnung enthalten.
Die Einheitengruppe und die Einheit werden ohne konkrete Einschränkung abgefragt, womit die Standarddatensätze zugeordnet werden.
Diese Transformationen müssen im Filter angepasst werden, wenn andere Zuordnungen gewünscht sind.
Der spezielle Prozess bildet die Hierarchie der Preislisten auf einzelne Preise ab.
Dazu können die Preislisten noch mit einem eigenen Filter "Preislisten Filter" eingeschränkt werden.
Die Prozesse für Preislisten und Artikel sind die Voraussetzung für die Ausführung.
Der Prozess sucht selbständig passende Datenabbildungen, um Ziel-IDs zu ermitteln.


Dynamics Firma nach Sage 100 Adresse
------------------------------------

Diese Vorlage basiert auf dem Universalprozess und überträgt Firmen als Adressen.
Es sind bestimmte Standardfelder in der Transformation und Zuordnung enthalten.
Die Vorlage beinhalten noch keinen Quellfilter.
Sollen nicht alle Firmen übertragen werden, muss ein Filter angegeben werden.

Siehe dazu auch :doc:`/bestpractices/syncwhere`

Der Matchcode wird aus Name und Stadt gebildet. Wenn dieses Format nicht gewünscht ist, kann die entsprechende Transformation angepasst werden.


Dynamics Kontakt nach Sage 100 Ansprechpartner
----------------------------------------------

Diese Vorlage basiert auf dem Universalprozess und überträgt Kontakte als Ansprechpartner.
Es sind bestimmte Standardfelder in der Transformation und Zuordnung enthalten.

Die Adresszuordnung wird den Datenabbildungen des Firmen-Adresse-Prozesses entnommen.
Deshalb muss bei der ersten Einrichtung diese Transformation bearbeitet und der korrekte Prozess eingestellt werden.

Das Feld "Ansprechpartner" wird per Transformation aus Anrede Vorname Nachname gebildet.
Wenn dieses Format nicht gewünscht ist, kann die entsprechende Transformation angepasst werden.

Kontakte werden wiederholt, sollte die Adresse noch nicht übertragen worden sein.