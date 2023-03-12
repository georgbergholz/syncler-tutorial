Eingehende Webhooks
===================

In diesem Bereich können eingehende Webhooks konfiguriert werden, die dann über die API aufgerufen werden können.
Dies bietet einen einfachen Weg für die Bereitstellung von Funktionen und erleichtert die Integration von externen Systemen.

Mit Webhooks können Daten gelesen und geschrieben werden.
Außerdem kann eine Adhoc-Ausführung eines Prozesses gestartet werden.
Die Konfiguration des Webhooks ermöglicht die Definition eines Quell- und Zielschema in JSON und ist dadurch optimal
an die Bedürfnisse und Vorgaben externer Systeme anpassbar.

Webhooks können mit einem GET oder POST Aufruf angesprochen werden.
Bei einem GET Aufruf werden die URL-Parameter für die Quelldaten der Ausführung verwendet.
Der POST Aufruf erwartet entweder ein JSON Objekt im Nachrichten-Body oder Formulardaten.
Aus Formulardaten wird ein Json-Objekt für die interne Verarbeitung erzeugt. 
Aus den Feldnamen werden dabei die Namen der Eigenschaften erzeugt.

Die komplexe Webhook ID, die für die URL verwendet wird, wird automatisch generiert und kann den Eigenschaften entnommen werden.
Um die Sicherheit zu verbessern, kann zusätzlich ein Geheimschlüssel manuell angegeben werden.
Dieser Geheimschlüssel muss als Header "syncler_webhooksecret" im Aufruf übergeben werden.
Wenn das Feld leer bleibt, wird diese Prüfung übersprungen.

Außerdem kann eine Ausführungsbedingung in SQL-Notation definiert werden, die einen Wahrheitswert generiert und
ggf. die Aktion nicht ausführt. In der Bedingung können Quellfelder in Rauten eingeschlossen als Platzhalter verwendet werden.



Einstellungen
-------------

Folgende Parameter werden unter "Allgemein" konfiguriert.

:Name:

Ist eine administrative Bezeichnung.

:Ist aktiv:

Nur aktive Webhooks können aufgerufen werden.
Inaktive Webhooks liefern einen 410-Fehler beim Aufruf.

:Webhook:

Das ist die generierte Webhook ID. Das Feld ist schreibgeschützt und bei der Neuanlage noch leer.

:Webhook Url:

Mit dieser URL kann der Webhook aufgerufen werden. Die URL der API muss noch als Präfix ergänzt werden.

:Geheimnis:

Dieser Geheimschlüssel muss als Header "syncler_webhooksecret" im Aufruf übergeben werden.
Wenn das Feld leer bleibt, wird diese Prüfung übersprungen.

:Ausführungsbedingung:

Die in SQL formulierte Wahrheitsbedingung wird mit Quelldaten über Raute-Platzhalter gefüllt und geprüft.
Ein negatives Ergebnis überspringt die Ausführung.

:Aktion ausführen:

Dieser Wert definiert die Funktion, die beim Aufruf ausgeführt werden soll.
Eine Detailbeschreibung finden Sie unter "Aktionen".

:Prozess für Aktion:

Mit diesem Wert wählen Sie den vorhandenen Prozess aus, der von der Aktion verwendet wird.
Für das Starten kann jeder beliebige Prozess verwendet werden.
Lesen und Schreiben mit einem Prozess erfordern die Verwendung eines Webhook Prozesses.

:Verbindung für Aktion:

Mit diesem Wert wählen Sie die vorhandene Verbindung aus, die für Lesen oder Schreiben verwendet werden soll.
Zusätzlich muss ein Schema von dieser Verbindung festgelegt werden.

:Schema-Objekt für Verbindung:

Dieses Schema-Objekt stammt von der ausgewählten Verbindung und wird für das Lesen oder Schreiben mit einer Verbindung genutzt.

:Weiterleitungs-Url nach dem Ausführen:

Speziell für das Schreiben von Daten kann dieser Parameter genutzt werden, um einer Weiterleitungs-Url zu definieren, die dann nach der Ausführung 
als Weiterleitungsaufforderung zurückgemeldet wird.
Damit ist es möglich, den Webhook als Empfänger eines Formulars zu definieren, welches nach dem Speichern eine LandingPage anzeigen soll.

:Daten im Änderungsspeicher für den Prozess ablegen:

Hier kann ein Prozess definiert werden, für den ein Datensatz im Änderungsspeicher abgestellt werden soll.
Speziell hierfür gibt es den Prozesstyp "Universal Ablauf - Daten aus Änderungsspeicher lesen".
Dieser Prozesstyp dient zum Einlesen der Daten aus dem Änderungsspeicher für eine anschließende Verarbeitung in einem Ablauf.
Sobald hier ein Prozess ausgewählt wird, wird mit den übergebenen Daten ein Änderungsdatensatz gespeichert.
Das Objekt erhält dabei den Names des Quellobjektes aus dem ausgewählten Prozess.
Sobald dieser Parameter definiert wird, erhält der Adhoc-Prozessstart nur die Guid des Änderungsdatensatzes und nicht mehr die Daten selbst.

:Suche nach Quelldatensatz für Prozess und Verbindung:

Diese Where-Clause wird mit Raute-Platzhaltern gefüllt und für das Lesen von Daten über einen Prozess oder eine Verbindung verwendet.
Die Formulierung muss für das Zielsystem passend erfolgen (SQL oder OData usw.).

:Sortierung:

Sofern die Verbindung, die das Lesen direkt oder indirekt über den Prozess ausführt, das Sortieren des Ergebnisses ermöglicht,
wird dieser optionales Wert dafür verwendet.
Auch hier werden Raute-Platzhalter mit den Quelldaten gefüllt.

:Nur den ersten Datensatz zurückgeben:

Abhängig vom aufrufenden System kann die Antwort mit einem Array von Daten nicht gewünscht oder verwendbar sein.
Für diesen Fall kann mit diesem Parameter nur der erste Datensatz als JSON Objekt zurückgegeben werden.
Ansonsten erfolgt die Antwort immer als Array, sobald ein Resultat gefunden wurde.

:Abfrage-Filter für Lesen einer Abfrage:

Dieses Filterfragment ersetzt den Plathalter FlowFilter in der Abfrage des Prozesses.
Dabei werden Platzhalter im Fragment mit den Daten des Aufrufs ersetzt.

:Suche nach Zieldatensatz für Verbindung:

Wenn das Schreiben mit einer Verbindung einen Datensatz aktualisieren soll, muss eine Suchanfrage formuliert werden.
Diese Where-Clause wird mit Raute-Platzhaltern gefüllt und für das Suchen des Zieldatensatzes über eine Verbindung verwendet.
Die Formulierung muss für das Zielsystem passend erfolgen (SQL oder OData usw.).

:Verhalten bei keiner Übereinstimmung für Schreiben mit Verbindung:

Sollte keine Suche formuliert sein oder diese kein Ergebnis geliefert haben, steuert dieser Parameter das weitere Vorgehen.
Der aktuelle Aufruf kann übersprungen werden oder es kann ein neuer Datensatz angelegt werden.

:Verhalten bei exakter Übereinstimmung für Schreiben mit Verbindung:

Sollte eine Suche formuliert sein und diese exakte einen Zieldatensatz gefunden haben, steuert dieser Parameter das weitere Vorgehen.
Der aktuelle Aufruf kann übersprungen werden oder der gefundene Datensatz kann aktualisiert werden.



Neben den allgemeinen Einstellungen stehen auch noch weitere Registerkarten zur Verfügung, die je nach Aktion konfiguriert werden müssen.

Für das Lesen von Daten mit einer Verbindung wird bereits im Webhook das Antwortschema definiert und die Felder aus dem Schemaobjekt den
Feldern des Zielschema zugeordnet.
Unter "Json-Schema Zieldaten" definieren Sie ein JSON Objekt, dessen Eigenschaften als Zielfelder für die Zuordnung verwendet werden.
Es können auch geschachtelte Strukturen definiert werden. Die Verwendung von Arrays ist durch die Feldzuordnung nicht möglich.
Unter "Zuordnung Lesen" verbinden Sie die Quellfelder der Verbindung mit den definierten Zielfeldern für die Antwort.
Wenn das Lesen mit einem Prozess erfolgt, müssen die Registerkarten nicht konfiguriert werden.

Für das Schreiben von Daten mit einer Verbindung wird bereits im Webhook das Quellschema definiert und die Felder aus dem Schemaobjekt den
Feldern des Quellschema zugeordnet.
Unter "Json-Schema Quelldaten" definieren Sie ein JSON Objekt, dessen Eigenschaften als Quellfelder für die Zuordnung verwendet werden.
Es können auch geschachtelte Strukturen definiert werden. Die Verwendung von Arrays ist durch die Feldzuordnung nicht möglich.
Unter "Zuordnung Schreiben" verbinden Sie die definierten Quellfelder mit den Zielfeldern der Verbindung.
Wenn das Schreiben mit einem Prozess erfolgt, müssen die Registerkarten nicht konfiguriert werden.


Aktionen
--------

Diese Aktionen können mit einem Webhook ausgelöst werden.

:Starte Prozess:

Hier wird ein Adhoc-Warteschlangendatensatz für den ausgewählten Prozess angelegt.
Die Quelldaten werden dabei direkt als Ausführungsparameter dem Warteschlangendatensatz hinzugefügt.
Die Ausführung erfolgt mit dem Daemon, dessen Prozessverarbeitung dafür aktiv sein muss.

:Lese Daten mit Prozess:

Hierfür muss ein Webhook Prozess zum Lesen von Daten konfiguriert werden.
Die definierte Suche und Sortierung wird mit den Quelldaten gefüllt und über den Prozess direkt
ausgeführt.
Das Ergebnis wird durch den Prozess transformiert und zugeordnet.
Die Antwort erfolgt mit einem JSON Array und dem am Prozess definierten Zielschema.
Per Parameter kann die Antwort auf das erste Objekt des Ergebnisses beschränkt werden.
In diesem Fall erfolgt die Antwort als JSON Objekt.

:Lese Abfrage mit Prozess

Hierfür muss ein Webhook Prozess zum Lesen einer Abfrage konfiguriert werden.
Der Abfrage-Filter wir mit den Quelldaten erzeugt und der Platzhalter in der Abfrage damit ersetzt.
Dann wird die resultierende Abfrage direkt ausgegeben.
Das Ergebnis wird durch den Prozess transformiert und zugeordnet.
Die Antwort erfolgt mit einem JSON Array und dem am Prozess definierten Zielschema.
Per Parameter kann die Antwort auf das erste Objekt des Ergebnisses beschränkt werden.
In diesem Fall erfolgt die Antwort als JSON Objekt.

:Speichere Daten mit Prozess:

Hierfür muss ein Webhook Prozess zum Schreiben von Daten konfiguriert werden.
Im Prozess kann eine Transformation und Feldzuordnung konfiguriert werden.
Das Quellschema und eine Suche im Zielsystem wird ebenfalls im Prozess konfigiriert.

:Lese Daten mit Verbindung:

Hier werden direkt Daten aus einer Verbindung angefordert.
Dafür muss hier die Suche, das Zielschema und die Feldzuordnung definiert werden.
Eine Transformation des Ergebnisses ist nicht möglich.

:Speichere Daten mit Verbindung:

Hier werden direkt Daten mit einer Verbindung geschrieben.
Das Zielschema wird aus den Schemaobjekten der Verbindung ausgewählt.
Mit dem in JSON definierten Quellschema können die Felder direkt zugeordnet werden.
Für die Suche eines vorhandenen Datensatzes stehen Parameter zur Verfügung.
Eine Transformation der Quelldaten ist nicht möglich.


Der Webhook Prozess für das Lesen von Daten
-------------------------------------------

Für das Lesen von Daten mit einem Prozess muss dieser spezielle Prozesstyp verwendet werden.
Im Prozess wird die Quellverbindung und das Quellobjekt definiert.
Außerdem stehen Registerkarten für die Definition des Zielschemas in JSON und die Feldzuordnungen zur Verfügung.
Das gelesene Ergebnis aus der Quellverbindung durchläuft die Transformation und den zweiten Filter, bevor es an den Webhook übergeben wird.


Der Webhook Prozess für das Schreiben von Daten
-----------------------------------------------

Für das Schreiben von Daten mit einem Prozess muss dieser spezielle Prozesstyp verwendet werden.
Im Prozess wird die Zielverbindung und das Zielobjekt definiert.
Außerdem stehen Registerkarten für die Definition des Quellschemas in JSON und die Feldzuordnungen zur Verfügung.
Eine Vorbedingung für die Neuanlage und die Übereinstimmungssuche für eine Aktualisierung wird im Prozess definiert.
Die übergebenen Quelldaten durchlaufen die Transformation und den zweiten Filter, bevor das Zielobjekt geschrieben wird.


Webhook Prozess zum Lesen einer Abfrage
---------------------------------------

Für das Lesen einer Abfrage mit einem Prozess muss dieser spezielle Prozesstyp verwendet werden.
Im Prozess wird die Quellverbindung und die Abfrage definiert.
Dabei kann der Platzhalter FlowFilter mit einem durch den Webhook erzeugten Filter ersetzt werden.
Außerdem stehen Registerkarten für die Definition des Zielschemas in JSON und die Feldzuordnungen zur Verfügung.
Das gelesene Ergebnis aus der Quellverbindung durchläuft die Transformation und den zweiten Filter, bevor es an den Webhook übergeben wird.

Starten eines Ablaufs
---------------------

Ein Universal-Ablauf kann auch für die Aktion "Starte Prozess" genutzt werden, allerdings muss dabei eine bestimmte Konfiguration eingehalten werden.
Abläufe führen keine direkte Datensatzverarbeitung aus, weshalb eine Übergabe an den Ablauf keine Ausführung erzeugt.
Hierfür muss ein Lese-Prozess für das Lesen aus dem Änderungsspeicher eingerichtet werden.
Für diesen Prozesstyp kann eine Quellverbindung und ein Quellobjekt definiert werden.
Dies soll ermöglichen, dass die Daten innerhalb des Ablaufs auch an andere Prozesse übergeben werden können.
Das Json-Schema für die Quelldaten am Prozess kann definiert werden, damit eine Transformation und ein zweiter Filter eingerichtet werden können.
Die Übernahme in den Änderungsspeicher durch den Webhook erfordert aber auch ein Json-Schema für die Quelldaten.
Dieser Lese-Prozess wird nun in den Ablauf eingefügt und liefert die Daten für die weitere Verarbeitung.
Nach der erfolgreichen Verarbeitung wird der Datensatz im Änderungsspeicher gelöscht.

Formulare
---------

Ein Webhook kann auch als Empfänger für ein Web-Formular genutzt werden.
Dabei erkennt die API selbstständig am Content-Type, ob ein Json-Objekt in der Nachricht übergeben wurde, oder ob es sich um Formulardaten handelt.
Aus dem Formulardaten wird ein Json-Objekt erzeugt, wobei die Feldnamen für die Eigenschaften verwendet werden.
Da Formular vorrangig durch Benutzer verwendet werden, ist eine LandingPage nach dem Empfang der Daten notwendig.
Die Url für diese Weiterleitung wird am Webhook definiert.
Nachdem die Verarbeitung abgeschlossen wurde, wird an diese Url weitergeleitet.
So kann der Webhook Daten eines Formlars annehmen, damit diverse Prozesse starten oder Daten direkt schreiben und im Anschluss eine Folgeseite aufrufen.