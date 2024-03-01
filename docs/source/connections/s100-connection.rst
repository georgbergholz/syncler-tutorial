Sage 100 (Draft)
========


Bezüglich der Zubehörartikelunterstützung:

Besitzt ein Artikel automatische Zubehörartikel werden diese entsprechend hinzugefügt. 
Gehören zu einem Artikel optionale Zubehörartikel, muss dessen Hinzufügen mittels des Positionrequestproperties 'ForceOptionalZubehoerartikel' erzwungen werden. 
Diese erzwungenen optionalen Zubehörartikelpositionen werden mit Menge = 0 dem Beleg hinzugefügt und müssen im weiteren Verlauf manuell im UI geändert werden.  


Im Request Objekt steht jetzt das neue Property „VkAngebotsstatus“ vom Typ int zur Verfügung.

Folgende Werte könnt ihr dort setzen:

None = 0,
Neuanlage = 1,
Abgelehnt = 3,
Angenommen = 4,
Erfuellt = 5

Sendet ihr keinen Wert für VkAngebotsstatus, also NULL, wird automatisch wie bisher 1 gesetzt. Im UI steht dann nicht Neuanlage , sondern Neu.

