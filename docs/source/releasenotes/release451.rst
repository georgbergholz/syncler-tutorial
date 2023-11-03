Release 4.5.1 - 03.11.2023
==========================

Änderungen
----------

WinCarat Verbindung

* Die Änderungsinformation wurde auf die Spalte "ROWDATUM" umgestellt. Die Versionsnummern werden nicht mehr verwendet.

Microsoft Graph nach Sage CRM und Zoho CRM Prozesse

* Der Reminder für vergangene Termine wird anhand des Startdatums abgeschaltet.

Data Quality Management

* Für die Dublettensuche kann je Spalte eine Ersetzungsliste angegeben werden. Mit dieser Pickliste wird der Vergleichswert beidseitig für den Vergleich angepasst. Damit können Bindeworte oder Unternehmensformen normalisiert werden.
* Transformationen können in der Aufbereitung angewendet werden.

SDK Helper

* Die InvokeUrl-Methode hat einen zusätzlichen optionalen Parameter für den ContentType bekommen. Der Standard ist application/json.

Syncler Administrator

* Neuer PageType OAuthGrantFlow für eine generische OAuth Authorization eingefügt. Wird aktuell in der SDK Verbindung und Vorlage SDK Verbindung angeboten.
* OAuth-Flow und OAuth-Flow 365 mit WebView2 umgesetzt, damit aktuelles Javascript unterstützt wird. Ggf. muß WebView2 auf dem Rechner nachinstalliert werden.

Syncler API

* Nach dem Schema-Refresh einer Verbindung wird diese nochmal gespeichert. Damit ist es möglich, Verbindungseigenschaften in z.B. Schema-Skripten zu beeinflussen.
* Für den Endpunkt RunConnectionSetData wurde ein RequestSizeLimit von 100MB festgelegt. Der Standard sind 30MB.

Syncler Datenbank

* Bei 95% der DB Nutzung wird für den Tenant eine Warnung täglich versendet.

Transformation

* In der Transformation "Daten abfragen" kann eine beliebige Verbindung ausgewählt werden.
* Neue Transformation "Geschlecht ermitteln". Mittels Vornamen und Land kann das Geschlecht einer Person ermittelt werden. Zu den Resultaten Männlich, Weiblich und Unisex können Ausgabewerte definiert werden.

Graph Verbindung

* Neues Schema UserRefreshToken ermöglicht die Überwachung von gesammelten Refresh-Token. Per Prozess kann damit auf abgelaufene Refresh-Token reagiert werden.
* Die Notation Related|:|group|;|RelatedId|:|1234|;| als Filter wird für Abfrageparameter ausgewertet. Damit können z.B. Mitglieder einer Gruppe abgerufen werden.

Universal Schreibprozess

* Damit können Json-Daten ohne Quelle direkt geschrieben werden.

Databyte Verbindung

* Die neue Verbindung zu Databyte steht zur Verfügung.

Sage 100 - Salesforce Belegübertragungsprozess

* Parameter für Positionssortierung wurde hinzugefügt.

Neuer Prozess

* Universal Prozess für geschachtelte Daten nach Seriendruck.


Korrekturen
-----------

Prozessausführung durch Ablauf

* Bei der Variante "Prozess für jeden Datensatz und angepassten Filter ausführen" wurde bei den einzelnen Ausführung nicht auf deren Abschluss gewartet.
* Dadurch konnten einzelne Ausführungen parallel laufen.

CAS Verbindung

* Der Upload von Dokumenten wurde korrigiert. Ein Aufruf per PUT liefert keinen Location-Header, der für die Ergebnisverarbeitung erforderlich ist.

Abfrageprozesse

* Die exakte Übereinstimmungssuche hat mit der Einstellungen "Nur Datenabbildung" den Datensatz übersprungen, wodurch dieser nicht für Nachfolgeprozesse bereitgestellt wurde. Der Datensatz wird jetzt als Erfolgreich markiert.

Speicheroptimierung

* Erzeugte Nachrichten wurden nach der Datensatzverarbeitung bis zum Abschluss des Prozesses im Speicher gehalten. Dieser werden jetzt nach Weiterleitung aus dem Speicher entfernt.

Webhooks

* Webhooks haben aus Prozessen keine typisierten Daten geliefert, falls diese transformiert wurden. Die Json-Antwort wird jetzt nach dem Datentyp geparst.

Support-Datenbank

* Bei der manuellen Bearbeitung wurde das Leeren eines Feldes nicht als Änderung erkannt.


Die Universal- und Universal-SDK-Prozesse entfernen Änderungsspeicherdatensätze nur noch anhand der Guid und nicht der Prozess-Zuordnung.

