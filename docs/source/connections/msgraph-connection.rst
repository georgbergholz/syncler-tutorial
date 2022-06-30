Microsoft Graph API
===================

Die Microsoft Graph API ist eine REST-basierte Schnittstelle für den Zugriff auf Microsoft 365.
Diese Verbindung realisiert die Anmeldung an der API und stellt ein ausgewähltes Datenschema bereit.
Ein Fokus der Verbindung ist der Zugriff und die Synchronisation von Terminen, wofür spezielle Parameter 
vorhanden sind.

Für die Einrichtung der Anmeldung ist eine registrierte Anwendung bei Microsoft erforderlich.

Registrieren Sie die Anwendung über das Registrierungsportal https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade.
Melden Sie sich mit Ihrem Microsoft Konto an und rufen Sie die Funktion "Neue Registrierung" auf.
Vergeben Sie einen Anwendungsnamen und klicken Sie auf Registrieren.

Danach wird Ihnen die Übersicht zur Registrierung angezeigt.
Für die Verbindung benötigen Sie die Anwendungs-ID (Client-ID) und die Verzeichnis-ID (Mandant).
Übernehmen Sie die Angaben in die Felder Client-ID und Azure AD Mandanten ID.

Damit die Verbindung auf die Graph API zugreifen kann, müssen Sie unter "Zertifikate & Geheimnisse" einen 
geheimen Clientschlüssel generieren.
Wählen Sie dazu die Funktion "Neuer geheimer Clientschlüssel".
Stellen Sie die gewünschte Gültigkeit ein und klicken Sie auf Hinzufügen.
Den angezeigte Geheimschlüssel müssen Sie direkt in das Feld "Client Geheimschlüssel" übernehmen.
Der Schlüssel ist nachträglich nicht mehr einsehbar.
Sollte der Schlüssel nicht mehr zur Verfügung stehen, müssen Sie einen neuen Geheimschlüssel hinzufügen.

Konfigurieren Sie als nächstes die API-Berechtigungen.
Für die Synchronisation von Termines des Unternehmen brauchen Sie die Berechtigungen "User.Read.All" und 
"Calendars.ReadWrite".
Beide Berechtigungen müssen durch den Administrator freigegeben werden.
Klicken Sie auf "Berechtigung hinzufügen", "Microsoft Graph" und "Anwendungsberechtigung".
Mittels des Suchfeldes können Sie die Berechtigungen leicht auswählen.


Funktionen
----------

:Schema ermitteln:

Das Datenschema wird aus den Metadaten der Graph API (https://graph.microsoft.com/v1.0/$metadata) ermittelt.
Dabei werden nicht alle Objekte zur Verfügung gestellt, sondern nur eine aktuell geprüfte Teilmenge.
ID-Felder und Felder mit Änderungsinformationen werden gekennzechnet, damit diese in Prozessen genutzt werden können.


:Lesen von Schema-basierten Daten:

Mit dem Universalplugin können Daten gelesen werden. 
Dabei ist auch eine Abfrage per Änderungsdatum möglich.
Daneben stehen spezielle Prozesse zur Verfügung, die eine umfassende Synchronisation ermöglichen, 
und neben Vorkommen einer Serie auch das Löschen von Ereignissen verarbeiten.

Speziell bei Ereignissen / Events wird die Abfrage über alle Benutzer einzeln ausgeführt.
Die betreffenden Benutzer werden über eine Verbindungseinstellung festgelegt.
Das genaue Verfahren wird in den Besonderheiten beschrieben.


:Lesen von Abfrage-basierten Daten:

Diese Funktion wird nicht unterstützt.


:Schreiben von Daten:

Das Schreiben eines Ereignisses erfolgt über den Benutzer, der für das Lesen genutzt wurde.
Bei der Neuanlage wird dieser Benutzer aus dem Feld Organisator entnommen.
Ungültige Werte führen dabei zu einer Fehlermeldung.
Die Anlage einer Serie ruft im Anschluss die Vorkommen des aktuellen Zeitfensters ab und speichert
Informationen dazu im Änderungsspeicher.
Dies ermöglich speziellen Prozessen die Vorkommen mit den Quelldaten abzugleichen.


:Schreiben von Bulk-Daten:

Diese Funktion wird nicht unterstützt.


Einstellungen
-------------

Folgende Einstellungen müssen bereitgestellt werden.

:API Url:

Definiert die Basis-Url aller Abfragen. Der Wert ist aktuell immer https://graph.microsoft.com

:Azure AD Mandanten ID:

Diese ID definiert das Unternehmen und kann bei der Registrierung der Anwendung ausgelesen werden,

:Filter für Benutzer:

Dieser Wert in OData-Notation definiert die Menge an Benutzer, für die Termine abgefragt und ggf. synchronisiert werden.
Das genaue Vorgehen ist in den Bensonderheiten beschrieben.
Folgender Wert wählt alle Mitglieder des Unternehmens aus: userType eq 'Member'

:Anzahl vergangener Monate:

Diese Ganzzahl definiert den Anfang des Zeitfensters für Synchronisationsprozesse.
Die Anzahl an Monaten wird bei kompletten Abfragen dem aktuellem Datum abgezogen.
Je größer der Wert ist, umso größer kann das Datenvolumen sein.

:Anzahl zukünftiger Monate:

Diese Ganzzahl definiert das Ende des Zeitfensters für Synchronisationsprozesse.
Die Anzahl an Monaten wird bei kompletten Abfragen dem aktuellem Datum hinzugefügt.
Je größer der Wert ist, umso größer kann das Datenvolumen sein.

:Client-ID:
    
Die Anwendungs-ID der registrierten Anwendung.

:Client-Geheimschlüssel:

Ein geheimer Schlüssel der registrierten Anwendung.


Besonderheiten
--------------

Beim Lesen von Ereignissen gibt es folgendes zu beachten.
Ereignisse werden über eine Liste von Benutzern ermittelt.
Da die ID eines Ereignisses abhängig vom Benutzer ist, über den die Abfrage ausgeführt wurde, 
wird die Antwort wie folgt verarbeitet.
Wenn der aktuelle Benutzer gleich dem Organisator des Ereignisses ist, wird der Datensatz übernommen und 
die ID z.B. in Datenabbildungen verwendet.
Wenn der aktuelle Benutzer nicht gleich dem Organisator ist und der Organisator aber über den Benutzerfilter 
erfasst wird, wird der Datensatz verworfen, damit keine Dubletten angelegt werden.
Wenn der Organisator nicht durch den Benutzerfilter erfasst wird, wird der Termin übernommen und alle 
Teilnehmer entfernt, die im Benutzerfilter enthalten sind und nicht dem aktuellen Benutzer entsprechen.
Dieses Verfahren stellt sicher, dass auch geteilte Ereignisse identifiziert werden können und keine Datensätze 
doppelt verarbeitet werden.

Die Abfragen von Ereignissen mit Universalplugins ermöglicht nicht das Abfragen von Vorkommen einer Serie oder 
gelöschten Datensätzen.

Für die Synchronisation von Ereignissen können Prozesse die Delta-Funktion der CalendarView verwenden.
Diese Funktion benötigt ein definiertes Zeitfenster (siehe Einstellungen) und einen gespeicherten Änderungstoken.
Prozesse, die dies nutzen, speichern das letzte Abfragedatum der kompletten Abfrage.
Ab da wird über den Änderungstoken abgefragt, der intern gespeichert und bei erfolgreicher Verarbeitung auch 
aktualisiert wird.
Da das definierte Zeitfenster keine kontinuierliche Synchronisation ermöglicht, wird mit jedem neuen Tag eine 
komplette Abfrage ausgelöst und das Zeitfenster um einen Tag vorgeschoben.
Termine außerhalb des Zeitfensters werden dann nicht von der Synchronisation erfasst.

Wenn die Delta-Funktion einen Termin als gelöscht ausgibt, wird dieser gezielt abgefragt.
Sollte er noch existieren, wurde er aus dem aktuellen Zeitfenster verschoben und wird mit verarbeitet.
Ohne Resultat wird der Termin als "gelöscht" verarbeitet.


Synchronisationsprozesse
------------------------

:doc:`/sync/graphzohosync`