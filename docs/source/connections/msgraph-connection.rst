Microsoft Graph API
===================

Die Microsoft Graph API ist eine REST-basierte Schnittstelle für den Zugriff auf Microsoft 365.
Diese Verbindung realisiert die Anmeldung an der API und stellt ein ausgewähltes Datenschema bereit.
Ein Fokus der Verbindung ist der Zugriff und die Synchronisation von Terminen, Aufgaben und Kontakten, 
wofür spezielle Parameter und Prozesse vorhanden sind.

Für die Einrichtung der Anmeldung ist eine registrierte Anwendung bei Microsoft erforderlich.

Registrieren Sie die Anwendung über das Registrierungsportal https://go.microsoft.com/fwlink/?linkid=2083908.
Melden Sie sich mit Ihrem Microsoft Konto an und rufen Sie die Funktion "Neue Registrierung" auf.
Vergeben Sie einen Anwendungsnamen und klicken Sie auf Registrieren.

Danach wird Ihnen die Übersicht zur Registrierung angezeigt.
Für die Verbindung benötigen Sie die Anwendungs-ID (Client) und die Verzeichnis-ID (Mandant).
Übernehmen Sie die Angaben in die gleichnamigen Felder.

Für die Authentifikation stehen verschiedene Mechanismen zur Verfügung.

:Client-Secret:

Dies ist eine Anwendungsanmeldung auf der Basis eines erzeugten Geheimnissen.
Unter "Zertifikate & Geheimnisse" müssen Sie einen geheimen Clientschlüssel generieren.
Wählen Sie dazu die Funktion "Neuer geheimer Clientschlüssel".
Stellen Sie die gewünschte Gültigkeit ein und klicken Sie auf Hinzufügen.
Den angezeigte Geheimschlüssel müssen Sie direkt in das Feld "Client Geheimschlüssel" übernehmen.
Der Schlüssel ist nachträglich nicht mehr einsehbar.
Sollte der Schlüssel nicht mehr zur Verfügung stehen oder abgelaufen sein, müssen Sie einen neuen 
Geheimschlüssel hinzufügen.
Bei dieser Methode werden nur Anwendungsberechtigung der API unterstützt.
Für den Scope-Wert muss folgendes eingestellt werden: https://graph.microsoft.com/.default

:Administrator Refresh-Token:

Dies ist eine benutzerbezogene Anmeldung, bei der die Freigabe direkt in der Verbindungskonfiguration erfolgt.
Wechseln Sie auf die Registerkarte "Microsoft 365 OAuth 2.0" und starten Sie den Freigabeprozess.
Als nächstes müssen Sie eine Anmeldung durchführen und den Zugriff durch die registrierte Anwendung freigeben.
Bei diesem Verfahren werden nur delegierte API Berechtigungen unterstützt.
Der Scope-Wert ist entscheidend für die angeforderten Berechtigungen. Diese müssen dennoch der Anwendung hinzugefügt werden.
Der Scope offline_access wird automatisch hinzugefügt.
Für den Zugriff auf Kalendereinträge wird der Scope Calendars.ReadWrite benötigt.
Mehrere Scope-Werte werden durch ein Leerzeichen getrennt.

:Benutzer Refresh-Token:

Auch dieses Verfahren ist eine benutzerbezogene Anmeldung, benötigt aber die Unterstützung durch ein externes Portal.
Für Sage CRM steht so ein Portal zur Verfügung und kann die Zustimmung und Refresh-Token von mehreren Benutzern
einholen.
Das externe Portal kann hierfür auf die API-Endpunkte GraphRefreshToken und DeleteGraphRefreshToken zugreifen.
Für die Anforderung des Refresh-Token wird der Autorisierungscode an die API übergeben, die dann den Refresh-Token abruft.
Dadurch wird der Refresh-Token nur intern verarbeitet und steht nie außerhalb des Synclers zur Verfügung.
Der Scope für die Anforderung des Autorisierungscodes muss identisch mit dem Scope-Wert in der Verbindung sein, damit
ein gültiger Access-Token angefordert werden kann.
Die vorhandenen Refresh-Token können in verschlüsselter Form im Bereich "Parameter" eingesehen und gelöscht werden.
Außerdem kann das externe Portal das Löschen der Freigabe auslösen.
Bei diesem Verfahren werden nur delegierte API Berechtigungen unterstützt.


Konfigurieren Sie als nächstes die API-Berechtigungen.
Für die Synchronisation von Termines des Unternehmen brauchen Sie die Anwendungsberechtigungen "Calendars.ReadWrite".
Für eine benutzerbezogene Authentifikation werden delegierte Berechtigungen benötigt.
Für die Verwendung des Benutzerfilter wird die Berechtigung "User.Read.All" benötigt. Sie können die
Benutzer mit deren Emailadresse aber auch im Feld Benutzerliste auflisten. Die Filterfunktion verhält sich
dynamisch, wohingegen die Benutzerliste statisch ist und ggf. für neue Benutzer angepasst werden muss.

Wenn die Benutzerauswahl durch eine Gruppe gesteuert werden soll, wird die Berechtigung GroupMember.Read.All benötigt.

Für die Synchronisation von Kontakten wird die Anwendungsberechtigung "Contacts.ReadWrite" benötigt.

Die Anwendungsberechtigungen müssen durch den Administrator freigegeben werden.
Klicken Sie auf "Berechtigung hinzufügen", "Microsoft Graph" und "Anwendungsberechtigung".
Mittels des Suchfeldes können Sie die Berechtigungen leicht auswählen.

Die Graph API unterstützt für den Zugriff auf Outlook-Aufgaben keine Anwendungsberechtigung.
Damit mit der Verbindung auch Aufgaben synchronisiert werden können, müssen Sie die delegierte Berechtigung 
"Tasks.ReadWrite" hinzufügen.
Im Anschluss müssen die Benutzer den Zugriff bestätigen, wofür je nach Ziel-System eine eigene Oberfläche 
oder API-Endpunkte (GraphRefreshToken, DeleteGraphRefreshToken) in der Syncler API zur Verfügung stehen.


Funktionen
----------

:Schema ermitteln:

Das Datenschema wird aus den Metadaten der Graph API (https://graph.microsoft.com/v1.0/$metadata) ermittelt.
Dabei werden nicht alle Objekte zur Verfügung gestellt, sondern nur eine aktuell geprüfte Teilmenge.
ID-Felder und Felder mit Änderungsinformationen werden gekennzechnet, damit diese in Prozessen genutzt werden können.
Teilweise wird das Schema auch erweitert, damit z.B. die Information "isDeleted" im Prozess ausgewertet 
oder bei Aufgaben und Kontakten über "user" der zugeordnete Benutzer festgelegt werden kann.

:Lesen von Schema-basierten Daten:

Mit dem Universalplugin können Daten gelesen werden. 
Dabei ist auch eine Abfrage per Änderungsdatum möglich.
Daneben stehen spezielle Prozesse zur Verfügung, die eine umfassende Synchronisation ermöglichen, 
und neben Vorkommen einer Serie auch das Löschen von Ereignissen, Aufgaben oder Kontakten verarbeiten.

Die Abfrage von Ereignissen, Aufgaben und Kontakten wird über alle Benutzer einzeln ausgeführt.
Die betreffenden Benutzer werden über eine Verbindungseinstellung festgelegt.
Das genaue Verfahren wird in den Besonderheiten beschrieben.
Für das Lesen von Aufgaben wird nur die Standardliste des jeweiligen Benutzers verwendet.

:Lesen von Abfrage-basierten Daten:

Diese Funktion wird nicht unterstützt.


:Schreiben von Daten:

Das Schreiben eines Ereignisses erfolgt über den Benutzer, der für das Lesen genutzt wurde.
Bei der Neuanlage wird dieser Benutzer aus dem Feld "Organisator" oder dem Feld "user" entnommen.
Ungültige Werte führen dabei zu einer Fehlermeldung.
Die Anlage einer Ereignis-Serie ruft im Anschluss die Vorkommen mit dem Startzeitpunkt und ggf.
dem Ende der Serie ab und speichert Informationen dazu im Änderungsspeicher.
Sollte die Serie kein Endzeitpunkt haben, wird das aktuelle Zeitfenster verwendet.
Dies ermöglich spezialisierten Prozessen die Vorkommen mit den Quelldaten abzugleichen.


:Schreiben von Bulk-Daten:

Diese Funktion wird nicht unterstützt.


Einstellungen
-------------

Folgende Einstellungen können bereitgestellt werden.

Für die Synchronisation von Kalendereinträgen wird die Delta-Funktion verwendet.
Diese setzt ein definiertes Zeitfenster voraus.
Ausgenommen von diesem Zeitfenster sind die Vorkommen einer Serie.
Diese werden immer vollständig synchronisiert.

:Anzahl vergangener Monate:

Diese Ganzzahl definiert den Anfang des Zeitfensters für Synchronisationsprozesse von Ereignissen.
Die Anzahl an Monaten wird bei kompletten Abfragen dem aktuellem Datum abgezogen.
Je größer der Wert ist, umso größer kann das Datenvolumen sein.

:Anzahl zukünftiger Monate:

Diese Ganzzahl definiert das Ende des Zeitfensters für Synchronisationsprozesse von Ereignissen.
Die Anzahl an Monaten wird bei kompletten Abfragen dem aktuellem Datum hinzugefügt.
Je größer der Wert ist, umso größer kann das Datenvolumen sein.

:Bevorzugte Outlook Zeitzone:

Datumswerte werden durch die Graph API mit einem Wert und einer separat angegebenen Zeitzone geliefert und erwartet.
Ohne die Angabe einer bevorzugten Zeitzone werden Datumswerte im Format "yyyy-MM-ddTHH:mm:ss" als UTC zurückgeliefert und 
müssen z.B. per Transformation in die notwendige Zielzeitzone umgerechnet werden.
Wenn Sie Daten speichern, sollten Sie die Zeitzone des Benutzers verwenden, wenn die Zeitzonen-Funktion
für Ereignisse nicht aktiviert werden soll.


:Authentifizierungsmethode:

Diese Auswahl definiert das Anmeldeverfahren, welches oben erläutert wurde.
Eine Ausnahme stellen Aufgaben dar. Diese werden immer über eine Benutzerzustimmung synchronisiert.

:Verzeichnis-ID (Mandant):

Diese ID definiert das Unternehmen und kann bei der Registrierung der Anwendung ausgelesen werden,

:Anwendungs-ID (Client):
    
Die Anwendungs-ID der registrierten Anwendung.

:Client-Geheimschlüssel:

Ein geheimer Schlüssel der registrierten Anwendung.

:Redirect URI:

Für das Authentifizierungsverfahren mittels Administrator Refresh-Token muss eine Weiterleitungs-URI konfiguriert werden.
Bei der Freigabe über den Syncler Administrator kann eine beliebige URI angegeben werden.
Für die Freigabe über das Web-Frontend ist folgender Wert notwendig.
Die Weiterleitungs-URI muss bei der registrierten Anwendung festgelegt werden.

:Ist Public Client:

Diese Einstellung ist für die Benutzerzustimmung relevant, da der Autorisierungsprozess sich unterscheidet.
Sollten Sie die Anwendung als public client konfiguriert haben, darf kein Geheimschlüssel für die
Benutzerzustimmung verwendet werden.

:Scopes:

Diese Berechtigungen werden bei einer Benutzerzustimmung angefordert.
Sollten diese geändert werden, muss die Benutzerzustimmung wiederholt werden.
Für das Client-Secret-Verfahren ist der Wert https://graph.microsoft.com/.default anzugeben.


Damit Kalender, Aufgaben und Kontakte synchronisiert werden können, müssen die betroffenen Benutzer definiert werden.
Hierfür stehen verschiedene Varianten zur Verfügung, die ggf. zusätzliche API-Berechtigungen erfordern.

:Methode für Auswahl von Benutzern:

Diese Auswahl legt das Verfahren fest, worüber der Benutzerkreis definiert wird.
Es stehen folgende Optionen zur Verfügung.

* Benutzerfilter nutzt einen definierten Filter für die Abfrage von Benutzern. Das Verfahren ist dynamisch und benötigt die Berechtigung User.ReadBasic.All
* Benutzerliste ist ein statisches Verfahren, wobei die Emailadressen mit Semikolon getrennt aufgelistet werden.
* Gruppenmitglieder ruft die Mitglieder einer Gruppe ab. Das Verfahren ist dynamisch und benötigt die Berechtigung User.ReadBasic.All und GroupMember.Read.All
* Benutzerzustimmung arbeitet auf der Basis der erteilten Zustimmungen, die über die Syncler API gesammelt wurden. Dieses Verfahren ist ebenfalls dynamisch.

:Filter für Benutzer:

Dieser Wert in OData-Notation definiert die Menge an Benutzer, für die Ereigniss, Aufgaben und Kontakte abgefragt 
und ggf. synchronisiert werden.
Das genaue Vorgehen ist in den Bensonderheiten beschrieben.
Folgender Wert wählt alle Mitglieder des Unternehmens aus: userType eq 'Member'
Falls Benutzer aus dieser Menge keine Mailbox-Rechte haben, kann es zu Fehlermeldungen kommen.

:Benutzerliste:

Wenn eine Abfrage von Benutzer nicht möglich oder gewünscht ist, können hier auch gezielt Benutzer mit Semikolon 
getrennt aufgelistet werden. Dabei wird die Emailadresse der Benutzer erwartet.

:Gruppenname für Benutzerauswahl:

Durch die Angabe eines Gruppennamens können die Benutzer aus den Mitgliedern der Gruppe entnommen werden.
Für diese Funktion wird eine Berechtigung für GroupMember und mindestens User.ReadBasic.All benötigt.
Mit jeder Prozessausführung werden die Benutzer aus der Gruppe gelesen und deren Kalender synchronisiert.

:Vorhandene Benutzerzustimmungen (schreibgeschützt):

Diese Liste wird bei der Anzeige der Verbindungseinstellungen generiert und zeigt die vorhandenen Benutzerzustimmungen.
Das Feld ist schreibgeschützt und kann nicht für die Pflege der Zustimmungen verwendet werden.


Besonderheiten
--------------

Für den delegierten Zugriff auf Aufgaben müssen noch weitere Einstellungen vorgenommen werden,
damit die Benutzer dem Zugriff zustimmen können, für den Fall, dass ein Geheimschlüssel verwendet wird.
Dazu zählt die Definition einer Umleitungs-URI, welche den erzeugten Autorisierungscode
verarbeiten kann.

Für Sage CRM ist diese URI möglich: http(s)://.../crm/CustomPages/MicrosoftConsent.asp
Damit die Benutzer die Autorisierung vornehmen können, müssen die öffentlichen Clientflows aktiviert werden.

Beim Lesen von Ereignissen gibt es Folgendes zu beachten.
Ereignisse, Aufgaben und Kontakte werden über eine Liste von Benutzern ermittelt.
Da die ID eines Ereignisses abhängig vom Benutzer ist, über den die Abfrage ausgeführt wurde, 
wird die Antwort wie folgt verarbeitet.
Wenn der aktuelle Benutzer gleich dem Organisator des Ereignisses ist, wird der Datensatz übernommen und 
die ID z.B. in Datenabbildungen verwendet.
Wenn der aktuelle Benutzer nicht gleich dem Organisator ist und der Organisator aber durch die Benutzerauswahl erfasst wird, 
wird der Datensatz verworfen, damit keine Dubletten angelegt werden.
Wenn der Organisator nicht durch die Benutzerauswahl erfasst wird, 
wird der Termin übernommen und alle Teilnehmer entfernt, die in der Benutzerauswahl enthalten sind und nicht 
dem aktuellen Benutzer entsprechen.
Dieses Verfahren stellt sicher, dass auch geteilte Ereignisse identifiziert werden können und keine Datensätze 
doppelt verarbeitet werden.

Die Abfragen von Ereignissen mit Universalplugins ermöglicht nicht das Abfragen von Vorkommen einer Serie oder 
gelöschten Datensätzen.

Für die Synchronisation von Ereignissen können Prozesse die Delta-Funktion der CalendarView verwenden.
Diese Funktion benötigt für Ereignisse ein definiertes Zeitfenster (siehe Einstellungen) und einen gespeicherten 
Änderungstoken.
Prozesse, die dies nutzen, speichern das letzte Abfragedatum der kompletten Abfrage.
Ab da wird über den Änderungstoken abgefragt, der intern in den Parametern gespeichert und bei erfolgreicher Verarbeitung auch 
aktualisiert wird.
Da ein definierte Zeitfenster keine kontinuierliche Synchronisation ermöglichen würde, wird mit jedem neuen Tag eine 
komplette Abfrage ausgelöst und das Zeitfenster um einen Tag vorgeschoben.
Termine außerhalb des Zeitfensters werden dann nicht mehr von der Synchronisation erfasst.

Für Aufgaben und Kontakte wird ebenfalls eine Delta-Funktion durch spezialisierte Prozesse unterstützt,
jedoch ist hier keine Angabe von Zeitfenstern erforderlich.

Wenn die Delta-Funktion einen Termin/Ereignis als gelöscht ausgibt, wird dieser gezielt abgefragt.
Sollte er noch existieren, wurde er aus dem aktuellen Zeitfenster verschoben und wird mit verarbeitet.
Ohne Resultat wird der Termin als "gelöscht" verarbeitet.
Dabei wird das Feld "isDeleted" mit "true" zurückgeliefert.

Eine Datenabfrage aus der Transformation "Daten abfragen" kann in Feldnotation einen einzelnen Datensatz abfragen.
Dies kann auch mit einer Benutzereinschränkung ergänzt werden, da sonst alle Benutzer geprüft werden müssen.

Beispiel:
    .. code-block:: none

        id|:|ABC|;|
        oder
        id|:|ABC|;|user|:|benutzer@domain.de|;|


Synchronisationsprozesse
------------------------

Für eine vollständige Synchronisation sind spezialisierte Prozesse erforderlich.
Hier finden Sie eine detaillierte Beschreibung. 

:doc:`/sync/graphzohosync`

:doc:`/sync/graphcrmsync`