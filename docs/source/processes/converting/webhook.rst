Webhook aufrufen
================

Diese Transformation ermöglich den Aufruf eines Webhooks.
Der Einsatz kann für lesende oder schreibende Aktionen genutzt werden.

Basis ist eine Url, die für jeden Datensatz aufgerufen wird.
Zusätzlich kann der Aufruf mit einem Header "Geheimschlüssel" erweitert werden.
Die Methode legt die HTTP-Methode des Aufrufes fest.
Unter "Daten senden" wird ein Json definiert, welches als Nachricht versendet wird.
Diese Vorlage kann mit Platzhaltern aus dem aktuellen Datensatz gefüllt werden.
Das Json sollte mit einfachen Hochkommas definiert werden, da diese automatisch in den Platzhaltern escaped werden.
Bei der Verwendung von doppelten Anführungszeichen und doppelten Anführungszeichen im Datensatz kann es zu einem fehlerhaften Json kommen.
Wird die Methode "GET" verwendet, werden die Json-Felder der obersten Ebene als GET-Parameter übergeben.

Die Ausführung kann Datensatz-spezifisch mit der Ausführungsbedingung übersprungen werden.
Die logische Bedingung in SQL-Notation kann Platzhalter enthalten und wird für jedenDatensatz ausgewertet.
Damit kann z.B. gesteuert werden, ob ein neuer Datensatz erzeugt werden muss.

Die Antwort des Webhooks wird in ein neues Feld gespeichert, dessen Name unter "Daten empfangen" festgelegt wird.
Sollte die Antwort ein Json-Objekt sein, kann der Inhalt mit der Transformation "Json in Spalten" (:doc:`/processes/converting/jsontocolumn`)
ausgewertet werden.

Mit der Checkbox für das Zwischenspeichern kann festgelegt werden, ob Aufrufe mit identischem Inhalt wiederverwendet werden können.
Das kann bei lesenden Webhooks mit identischem Resulat die Ausführungszeit verkürzen.

Einstellungen
-------------

Folgende Parameter werden konfiguriert.

:Name:

Ist eine administrative Bezeichnung.

:Url:

Url des Webhooks.

:Geheimnisname:

Name des zusätzlichen Headers.

:Geheimnis:

Wert des zusätzlichen Headers.

:Methode:

HTTP-Methode des Aufrufs.

:Daten senden:

Vorlage für den Versand der Json-Nachricht.
Inhalte des Datensatzes werden mit Platzhaltern übernommen.

:Ausführungsbedingung:

Logische Bedingung in SQL-Notation.
Inhalte des Datensatzes werden mit Platzhaltern übernommen.
Ein negatives Resultat überspringt den aktuellen Datensatz.

:Daten empfangen:

Feldname für die Ablage der Antwort des Aufrufs.
Das Feld wird ggf. neu hinzugefügt.

:Zwischenspeichern gleicher Anfragen:

Bei identischem Nachrichteninhalt werden Aufrufe nicht erneut ausgeführt, sondern die zwischengespeicherte Antwort verwendet.
