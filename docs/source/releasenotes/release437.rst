Release 4.3.7 - 31.03.2022
==========================

Änderungen
----------

Die Datenabbildung beinhaltet bei geschachtelten Datensätzen den reinen Quelldatensatz und nicht mehr ausschließlich den Hauptdatensatz.

Der Universalprozess für geschachtelte Daten markiert alle vorhandenen Zielposition zum Löschen, 
wenn keine Übereinstimmungsregel für Positionen angegeben wurde.

Die Zoho CRM Verbindung wurde auf die API Version 2.1 umgestellt. Diese Umstellung erfordert eine Aktualisierung des Schemas und ggf. von Belegprozessen.
Die Beleg-Positionen wurden mit einem anpassbaren Modul ersetzt, wodurch vorhandene Feldzuordnungen ungültig werden.
Die Behandlung von Nachschlag-Feldern und Subforms hat sich auch geändert.

Die Fehlerbehandlung bei Business-Central-Kundenprozessen wurde angepasst. Fehler bei Business-Relations werden separat behandelt,
damit eine gültige Datenabbildung erzeugt werden kann.

Die Zoho CRM Verbindung unterstützt ein neues Schema-Objekt users, womit Abfragen nach Benutzern möglich werden. Ggf. muss das Scope des Self-Clients ergänzt werden.

Die Zoho CRM Verbindung legt interne Auswahllisten für Auswahlfelder an. 
Diese können in der Transformation "Auswahlliste abbilden" verwendet werden, um Text-Wert oder Text-ID Umwandlungen vorzunehmen.

Die Sage 100 Verbindung unterstützt Zubehörartikel bei der Belegerzeugung.
Besitzt ein Artikel automatische Zubehörartikel werden diese entsprechend hinzugefügt. 
Gehören zu einem Artikel optionale Zubehörartikel, muss dessen Hinzufügen mittels des Positionrequestproperties 
"ForceOptionalZubehoerartikel" erzwungen werden. 
Diese erzwungenen optionalen Zubehörartikelpositionen werden mit Menge = 0 dem Beleg hinzugefügt und müssen im weiteren 
Verlauf manuell im UI geändert werden. 

Die Projektnummer kann EK-Positionen in der Sage 100 Verbindung zugeordnet werden.

In Prozessen mit geschachtelten Daten steht ein sekundärer Filter für Positionen zur Verfügung. 
Damit können Positionen für die weitere Verarbeitung ausgeschlossen werden.

Die neue Verbindung zur Microsoft Graph-API steht zur Verfügung.
Dies beinhaltet auch Prozesse und Vorlagen für die Synchronisation mit Zoho CRM Meetings.

Die Zoho CRM Verbindung wurde für die Behandlung von Serienterminen erweitert.

In der Sage CRM Verbindung kann per Einstellung kann festgelegt werden, 
ob die per Typ ausgewählten Adressen an Firma und Person auch mehrfach verwendet werden können. 
Dies kann beim Schreiben allerdings zu einem Konflikt führen und muss genau geprüft werden.

Für die SAP IDoc Verbindung brauchen Multitexte im Schema nur noch ein MaxOccurs von 1 und das Feld TDLINE.
Damit stehen Multitexte auch am Produkt zur Verfügung.

Die neue Transformation "Datenabbildung abfragen" steht zur Verfügung.
Es wird ein Prozess ausgewählt und festgelegt, ob die Suche per Source oder Target erfolgt.
Der geparste Suchstring wird dann direkt verglichen und als Resultat werden SourceId, TargetId und TargetIsDeleted bereitgestellt.
Häufige Abfragen an das Zielsystem nach Datensätzen, die verknüpft werden sollen, können damit reduziert werden.

Die On-premises Version beinhaltet eine aktive Benachrichtigung per Email zu neuen Versionen.

Die CAS Verbindung unterscheidet nach Datum und Datum-Uhrzeit Feldern anhand der percision-Angabe.
Datumsfelder werden nicht in nach lokal beim Lesen oder nach UTC beim Schreiben konvertiert.
Die Übergabe beim Schreiben erfolgt ohne Uhrzeit.


Korrekturen
-----------

Bei der direkten Verwendung der Syncler-API per Client-ID konnte bei bestimmten Funktionen ein Unauthorized access ausgelöst werden, 
wenn Protokolle geschrieben werden sollten.

Der Standard-Preis für Sage CRM Produkte konnte einen Fehler auslösen, wenn das entsprechende Schema nicht vorhanden war.
Dies wurde mit einer zusätzlichen Prüfung korrigiert.

Beim Schreiben von Daten mit der Business-Central-Verbindung wird der eingestellte Mandant per Url übergeben.
Die Definition einer Standard-Firma entfällt.

Die API-Aufrufe bei Business-Central können case-sensitiv sein, wodurch die Prozesse zur Kundenanlage den neuen Kontakt nicht behandeln konnten.

In einigen Prozessen wurde vor dem Rückschreiben nicht geprüft, ob die Sync-Felder auch im Schema enthalten sind.
Dies konnte zu einem kontinuierlichen "leeren" Rückschreiben führen, da das neue Änderungsdatum größer als 
der neue Grenzwert ist.

Das Abfrufen von Daten mit der SQL-Verbindung und der SQL-Bridge wurde korrigiert. 
Die abgefragten Daten wurden nicht der Verarbeitung in Prozessen übergeben. 
Das betrifft ausschließlich das Hauptobjekt.