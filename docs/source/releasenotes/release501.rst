Release 5.0.1 - 
==========================

Mit dieser Version wird eine neue Generation des Synclers veröffentlicht.
Die Anwendung wurde für die .Net-Version 8.0 überarbeitet und verabschiedet sich damit komplett von .Net-Core.
Außerdem wurden einige strukturelle Veränderungen vorgenommen, die die Entwicklung betreffen und den Weg 
für ein neues Frontend vorbereiten.
Eine on-premises Version sollte nicht aktualisiert, sondern ausgetauscht werden.

Änderungen
----------




CAS-Verbindung

* Die Verbindung wurde für die Webservice-Version 7.0 angepasst.
* Das Schemaobjekt Tag wurde ergänzt.
* Abhängig von der Version wird zwischen dossier und link unterschieden.
* Mit dem neuen Schema "recyclebin" können Datensätze aus dem Papierkorb abgerufen werden. Der Filter mit in Feldnotation im Wert "deleted" den Objekttyp enthalten.
* Mit dem neuen Prozess "CAS gelöschte Daten" können gezielt gelöschte Datensätze verarbeitet werden.

