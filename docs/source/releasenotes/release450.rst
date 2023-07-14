Release 4.5.0 - 13.07.2023
==========================

Änderungen
----------

Die Microsoft Dynamics 365 Customer Engagement Verbindung

* Für Syncler steht die Verbindung zu Microsoft Dynamics 365 Customer Engagement zur Verfügung.
* Für die Synchronisation können die Universal-Prozesse genutzt werden.
* Mit Abfrageprozessen können beliebige Anfragen an die API gestellt werden.
* Es werden diese Schemaobjekte unterstützt: "account", "contact", "lead", "opportunity", "opportunityproduct", "product", "businessunit", "transactioncurrency", "externalparty", "territory", "service", "systemuser", "team", "equipment", "pricelevel", "productpricelevel", "uomschedule", "uom"
* Es stehen Vorlagen für die Kombination mit der Sage 100 bereit.
* Die Anmeldung kann per OAuth 2.0 oder Client-ID erfolgen.

Der Syncler Administrator

* Transformationsschritte können mit Klick statt Doppelklick geöffnet werden.
* Es wurde eine Import-Funktion für Prozesse ergänzt.
* Tabellen der Support-Datenbank können per Menü geleert werden.
* Es können Spalten in der Support-Datenbank an Tabellen ergänzt werden.
* Ein Abfrage-Dialog kann für die Support-Datenbank geöffnet werden, um beliebige Abfragen mit Ergebnisausgabe auszuführen.
* Einzelne Spalten einer Tabelle in der Support-Datenbank können als Index definiert werden, um Abfragen zu optimieren.
* An einer Verbindung können Auswahllisten eingesehen, bearbeiten und angelegt werden. Diese können in Transformation oder dem DQM eingesetzt werden.
* Im Testlauf wird nicht ausschließlich das Objektschema für Quell- und transformierte Daten verwendet, sondern zusätzlich vorhandene Daten werden ergänzt. Dies kann z.B. in untergeordneten Listen der Fall sein.
* An Verbindungen steht die Funktion "Abfrage ausführen" zur Verfügung. Der folgende Abfrage-Dialog kann beliebige Abfragen ausführen und das Ergebnis darstellen.
* Der Neustart eines Warteschlangeneintrags leert die Liste der fehlgeschlagenen Datensätze, was sonst das neue Resultat beeinträchtigt hat.

Der IDoc-Salesforce-Beleg Prozesse

* Es kann ein Skript für die Datensatzverarbeitung hinterlegt werden. Damit kann unabhängig von der Transformation die Verarbeitung beeinflusst werden.
* Wenn sich bei der Aktualisierung einer Position die PricebookEntryId ändert, wird diese Zielposition zum Löschen markiert. Die Quelldaten werden dann als neue Position übertragen.

Schema und Prozesse für geschachtelte Datensätze

* Die Positionsdatensätze enthalten jetzt immer eine Kopie des Hauptdatensatzes und eine einzelne Position. 
Damit stehen auch Daten des Hauptdatensatzes in Transformationen oder Bedingungen zur Verfügung.

Prozess Sage CRM Kommunikation nach Microsoft Graph Ereignis

* Mit einem neuen Parameter kann das Verschieben eines Termins zwischen Postfächern / Organisatoren aktiviert werden. 
Die Basis dafür ist ein Feldmapping auf den Organisator. Quell- und Zielwert werden bei der Aktualisierung verglichen und ggf. wird Ziel und Mapping gelöscht. 
Der Termin wird dann neu angelegt.

Die SQL-Verbindung

* Das Speichern von UniqueIdentifier durch Guid-Spalten aus Prozessen wurde ergänzt.

Datenabbildungen

* Fehler beim Speichern erzeugen einen abschließenden Fehler, der nicht automatisch wiederholt wird.

Die Saleforce-Verbindung wurde auf Version 57 aktualisiert.

Bei der Verarbeitung von Ablaufdatensätzen werden zusätzliche Debug-Meldungen erzeugt.

Die Auswahllisten können um deutsche und englische Übersetzungen ergänzt werden. Diese können dann im generischen ERP-Fokus zur Übersetzung verwendet werden.

Die Transformation "Daten abfragen" verwendet einen neuen Limit-Parameter, der automatisch die Resultatsmenge begrenzt. Dies optimiert die Transformation bei umfangreichen Abfrageresultaten.

Der Universal-SDK-Prozess

* Verschiedene Ergänzungen aus dem Universalprozess wurden in diesen Prozess übernommen, damit der Funktionsumfang identisch ist.

Die Salesviewer-Verbindung

* Mit dieser neuen Verbindung können Salesviewer Leads und Besuchsdaten mit einem Universalprozess in jedes beliebige System übertragen werden.

Die Docu-Sign-Verbindung

* Mit dieser neuen Verbindung kann ein Remote-Signing-Prozess implementiert werden. 
* Der Versand von Unterschriftsanfragen und das Speichern von unterschriebenen Dokumenten kann damit realisiert werden.

Universalprozess nach Seriendruck

* Mit diesem neuen Prozess können auch schema-basierte Daten für Seriendrucke genutzt werden. Dies war bisher nur mit Abfragen möglich.

Die Evalanche-Verbindung

* Mit dieser neuen Verbindung kann der dei Evalanche Marketing Software angebunden werden.
* Die Verbindung unterstützt Mandanten und Pools.
* Es stehen Mailing, MailingDetails, MailingStatistics, Article, Profile, Recipient, Bounce, Unsubscription, GrantedPermission, RevokePermission, Impression (Openings) und Clicks zur Verfügung.
* Profile können beliebig angelegt, aktualisiert oder gelöscht werden. Auch können Berechtigungen gesetzt oder entfernt werden.
* Die Reultate werden für einen einfachen Einsatz in Prozessen aufbereitet und erweitert.

Ablauf-Prozesse

* Die Übernahme der Zieldaten erfolgt automatisch, sobald der aktuelle Prozess als Vorgänge ausgewählt wurde und dessen Zieldaten verarbeitet werden sollen.
* Bisher war das an die Übernahme der Quelldaten gekoppelt, was missverständlich war und unnötig Ressourcen beansprucht hat.

Data Quality Management

* Dieses neue Feature kann in zwei unterschiedlichen Editionen gebucht werden.
* Mit dem Data Quality Manager haben sie die Möglichkeit einen Zielzustand für ihre Daten zu definieren und die Erreichung zu analysieren.
* Daten die dem Zielzustand nicht entsprechen können manuell oder automatisch korrigiert werden.
* Eine Übertragung in ein beliebiges Zielsystem schließt den Prozess ab.
* Neben Feldeigenschaften können auch Beziehung zwischen Datenobjekten behandelt werden.
* Die Suche und Verarbeitung nach Dubletten rundet den Funktionsumfang ab.
* Die Nutzung kann manuell oder auch vollautomatisch konfiguriert werden.

Korrekturen
-----------

Abfrage nach Seriendruck Prozesse

* Das Zielobjekt wurde nicht für Abläufe bereitgestellt, wodurch keine Kombination möglich war.

Die Sage b7 Verbindung

* Die Responseverarbeitung wurde korrigiert. Dies betrifft u.a. die Antwort auf neu angelegt Datensätze. Fehler wurden als Kommunikationsfehler statt Systemfehler behandelt.
* Die Übergabe von leeren Integer- und Auswahlfeldern erfolgt als 0 und nicht als Null.

Die Json zu Datenobjekt Konvertierung

* Bei der Behandlung von primitiven Arrays werden Objektgruppen mit Value-Feldern gebildet. Bei der Konvertierung zu Json wurde daraus keine primitiven Arrays erzeugt. Dadurch gelangt eine Json-Notation in das Datenobjekt. Dies passiert in SDK-Prozessen, da dort die Objekte in den Helper als JObject gegeben werden und nach Skriptausführung wieder in ein Datenobjekt konvertiert werden.
* Die Konvertierung hat keinen Verknüpfungstyp für Unterobjekte definiert, wenn der Wertvorrat des Schemas erschöpft war. Dadurch wurden diese Daten in der Transformation verworfen. Jetzt wird ein fortlaufender Index verwendet.

Abfrage-Prozesse

* Wenn in Abfrage-Prozessen mit Datenabbildungen gearbeitet wird, hat die Übereinstimmungssuche keine bereits zugeordneten Suchergebisse ausgeschlossen. 
Dadurch konnten mehrere Quelldatensätze auf einen Zieldatensatz abgebildet werden.

Die Microsoft-Graph-Verbindung

* Der Filter für Abfragen wird nicht mehr auf Sonderzeichen geparst. Dadurch war keine Abfrage mit Sonderzeichen möglich.

Der Sage CRM ERP-Fokus

* Das Filtern von Datumswerten wurde korrigiert. Durch einen erneuten Seitenaufruf ist der vorangegangene Wert ungültig geworden.
* Der Excel-Export wurde angepasst und HTML aus den Aggregatszeilen entfernt.

Die REST-API-Verbindung

* Datumswerte werden explizit als lokal geparst.
* Das Parsen von Datumswerten kann mittels Parameter abgeschaltet werden.

Die Datensatzverarbeitung prüft auf vorhandene Primärschlüssel, bevor doppelte Datensätze ausgeschlossen werden. Dadurch werden alle Daten ohne Primärschlüssel auch verarbeitet.

CAS und Zoho Prozesse

* Die SIS_MESSAGE-Felder wurden beim Leeren mit einem Leerzeichen beschrieben. Dies ist nur bei Sage CRM eine notwendige Vorgehensweise.

CAS Adresse nach Cleverreach oder InxMai

* Die CAS-Aktualisierungsinformation wurde beim Zurückschreiben nicht korrigiert, wodruch eine erneute Verarbeitung ausgelöst wurde.

Die SQL-Bridge

* Beim Schreiben wurde versucht die Transaktion im entfernten System zu zählen, was einen Verbindungsfehler auslöst.
* Einzeln gelesene Datensätze hatten durch die Json-Serialisierung bereits als geändert markeirte Felder.

Die Sage 100 Belegübertragung

* Die bisherige Fehlerbehandlung hat keine Wiederholung nach der Übergabe an die Sage 100 zugelassen.
* Nach dieser Anpassung ist eine Fehlerwiederholung abhängig von der Antwort zur Anfrage möglich.

Prozesse mit Unterprozessen

* Bei verschiedenen Prozessen, die Unterprozesse nutzen, wurde die Nachrichtenübermittlung nicht angebunden.
* Betroffen sind CAS-Inxmail, CAS-Cleverreach, CRM-Cleverreach, CRM-Inxmail, CRM-Mailchimp

Die Inxmail-Verbindung

* Die Suche nach Emailadressen wurde korrigiert.
* Die Übertragung von geschachtelten Daten wurde korrigiert. Doppelte Listenanmeldungen werden automatisch übersprungen.