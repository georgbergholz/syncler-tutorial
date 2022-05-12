Release 4.3.8 - 12.05.2022
==========================

Änderungen
----------

Die Sage 100 API unterstützt das Objekt VkBelegeStuecklisten.

Die Sage 100 Verbindung speichert die Url des Objektes. Damit sollen Fehlern bei neuen Objekten
vorgebeugt werden.

Die Sage 100 Verbindung unterstützt die OfficeLine Version 6.2 nicht länger.

Die Transformation "Daten abfragen" unterstützt untergeordnete Strukturen im Objekt.
Diese werden mit einem Doppelpunkt notiert in das Ergebnis übernommen.

Im Syncler Administrator wurde das Neu-Menü für Transformationen strukturiert.

Es wurde eine zusätzliche Aktivitätskontrolle für die Warteschlangen-Verarbeitung eingeführt.
Diese kann ggf. die Verarbeitung reaktivieren, falls diese in Folge eines Fehlers nicht mehr
aktiv sein sollte.

Für Datendienste steht der Parameter "Format für Datums- und Uhrzeitfilter" zur Verfügung.
Damit kann ein individuelles Format für Filterabfragen definiert werden, falls dieses die
Datenquelle erfordert.

Die Serienbrief-Verbindung kann Serienbrief-Felder in Word-Vorlagen mit strukturiertem Inhalt aus Html, Rtf 
oder Word füllen. Das Feld muss dafür den Präfix Html: Rtf: oder Docx: tragen.

Der Universal Sync Prozess für Emails lässt mehrfach zugeordnete Datenabbildungen zu.
Da diese Daten nur unidirektional übertragen werden können, kann kein Konflikt entstehen.
Damit können verschiedene Emails dem identischen Ziel zugeordnet werden. 
Z.B. Emails zu einem Ticket.
Die Datenabbildungen sind in Folgeprozessen oder zur Dublettenvermeidung vorhanden.

Die Transformation "Parameter erzeugen" überschreibt keine Quelldaten, falls der Parameter
keinen Wert hat. Damit können Parameter für Feldzuordnungen definiert werden, welche auf
Felder aus Vorgängerprozessen verweisen. Siehe Abläufe.

Das Universal Ablauf Plugin steht zur Verfügung. Damit können komplexere Abläufe definiert werden.
Siehe :doc:`/processes/flowbase`

Der Platzhalter "#FlowFilter#" kann in Abfrageprozessen eingefügt werden. Damit kann die Abfrage
aus Abläufen heraus individualisiert werden.

Die Standardwerte im Wartungsprozess wurden auf 14 Tage reduziert.

Für die Abläufe stehen zwei weitere Prozesse zur Verfügung.
Mit "Daten lesen" und "Geschachtelte Daten lesen" können Daten ohne eine Zielverarbeitung initial für
einen Ablauf gelesen werden.

Die Email Verbindung bereitet den HtmlBody als HtmlBodyInlineImages auf, damit ContentId durch 
Filename ersetzt wird und dieser so z.B. direkt im Sage CRM verwendet werden kann.
Die Attachments erhalten das Feld ContentId, damit zwischen Inline-Bild und Anhang unterschieden 
werden kann.

Der neue Prozess "Email Anhänge nach Sage CRM" führt die gesammelt Ablage von Anhängen durch.
Libr_IsInlineImage, Libr_FileName und Libr_FileSize werden dabei automatisch gesetzt.
Weitere Felder können per Feldzuordnung gefüllt werden.

Der neue Feldtyp "Objekt" ermöglich die Übergabe eines Json-Strings, der dann als Objekt 
ausgewertet wird.

Die Email Verbindung enthält Felder für einen Standardabsender. 
Dieser wird bei Emailversand aus Abläufen verwendet.

Es steht eine neue Verbindung zu Maileon zur Verfügung.
Siehe :doc:`/connections/maileon-connection`

Es wurden die Voraussetzungen für abschließende Fehler ohne Wiederholung geschaffen.
Diese produzieren eine Warnung werden aber nicht weiter wiederholt.
Das wird bereits in der Maileon-Verbindung genutzt, wo bestimmte Fehler gar nicht aufgelöst werden können.

Die Suche nach Email, Phone und Word in der Zoho CRM Verbindung wurde angepasst.
Die Kriteriumsnotation wird weiterhin verwendet, intern aber in eine gezielte Abfrage umgeformt.
Die Kriteriumssuche nach diesen Feldern wird von Zoho CRM nicht mehr unterstützt.

Die Zoho CRM Verbindung unterstützt die Nachfolger-Beziehung Campaigns zu Contacts, welche per
Nachfolgerprozessen ausgewertet werden kann.

Der Universal Lösch Prozess wurde hinzugefügt. Dieser kann gezielt per Datenabbildung oder
Übereinstimmungssuche einen Datensatz im Ziel löschen.
Optional können auch die Datenabbildungen entfernt werden.

Der Universal Sync Prozess erzeugt Daten im Änderungsspeicher, falls diese keine ID-Werte haben.
Das Lesen muss durch die Verbindung unterstützt werden.

Alle Sync-Prozesse haben einen neuen Parameter für das Abschalten einer Datensatzkopie in den
Datenabbildungen. Damit kann Speicherplatz gespart werden, wenn z.B. Prozesse nur unidirektional übertragen.
Das Abschalten per Servereinstellungen kann damit nicht umgangen werden. Dies hat Priorität.

Der Onpremises-Setup konfiguriert den Dienst für Neustarten im Fehlerfall.

Zur Syncler Bridge kann in den Verbindungen ein Timeout definiert werden.

Korrekturen
-----------

Alle Abfrage-Prozess mit Ziel Sage CRM wurden korrigiert. Bei der Übertragung von Personen 
wurde die Firma nicht korrekt ermittelt, wodurch das Setzen der Primärperson fehlgeschlagen ist.

Die CSV-Verbindung wurde ergänzt, damit fehlende Spalten übersprungen werden.

In der Sage Bäurer b7 Verbindung werden die Felder aufnr und rg_nr im Schema nicht mehr als Auswahl
geführt, sondern als String gespeichert.
Damit findet das Abrufen von AWL dazu nicht statt, was i.d.R. in ein Timeout läuft.

Datensatzsperren werden für Datensätze ohne IDs nicht mehr angelegt.

Die Zoho CRM Verbindung hat für Activities ein doppeltes Tag-Objekt in das Schema eingefügt.
Dies hat in der Verarbeitung zu Fehlern geführt.

In der Sage Bäurer b7 Verbindung wurde die Verarbeitung von Request-Antworten nicht auf den Objekttyp geprüft.
Damit konnte eine Verarbeitung durch einen fremden Prozess erfolgen, falls parallel verschiedene
Requests aufgeführt wurden.

Die Graph Verbindung konnte ohne ein Schema nicht neu angelegt werden.

Die Sprache des Syncler Administrators richtet sich nach den Einstellungen und nicht nach der Umgebung.