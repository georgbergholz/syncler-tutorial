Microsoft Graph API
===================

Die Microsoft Graph API ist eine REST-basierte Schnittstelle f�r den Zugriff auf Microsoft 365.
Diese Verbindung realisiert die Anmeldung an der API und stellt ein ausgew�hltes Datenschema bereit.
Ein Fokus der Verbindung ist der Zugriff und die Synchronisation von Terminen, wof�r spezielle Parameter vorhanden sind.

F�r die Einrichtung der Anmeldung ist eine registrierte Anwendung bei Microsoft erforderlich.

Registrieren Sie die Anwendung �ber das Registrierungsportal https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade.
Melden Sie sich mit Ihrem Microsoft Konto an und rufen Sie die Funktion "Neue Registrierung" auf.
Vergeben Sie einen Anwendungsnamen und klicken Sie auf Registrieren.

Danach wird Ihnen die �bersicht zur Registrierung angezeigt.
F�r die Verbindung ben�tigen Sie die Anwendungs-ID (Client-ID) und die Verzeichnis-ID (Mandant).
�bernehmen Sie die Angaben in die Felder Client-ID und Azure AD Mandanten ID.

Damit die Verbindung auf die Graph API zugreifen kann, m�ssen Sie unter "Zertifikate & Geheimnisse" einen geheimen Clientschl�ssel generieren.
W�hlen Sie dazu die Funktion "Neuer geheimer Clientschl�ssel".
Stellen Sie die gew�nschte G�ltigkeit ein und klicken Sie auf Hinzuf�gen.
Den angezeigte Geheimschl�ssel m�ssen Sie direkt in das Feld "Client Geheimschl�ssel" �bernehmen.
Der Schl�ssel ist nachtr�glich nicht mehr einsehbar.
Sollte der Schl�ssel nicht mehr zur Verf�gung stehen, m�ssen Sie einen neuen Geheimschl�ssel hinzuf�gen.

Konfigurieren Sie als n�chstes die API-Berechtigungen.
F�r die Synchronisation von Termines des Unternehmen brauchen Sie die Berechtigungen "User.Read.All" und "Calendars.ReadWrite".
Beide Berechtigungen m�ssen durch den Administrator freigegeben werden.
Klicken Sie auf "Berechtigung hinzuf�gen", "Microsoft Graph" und "Anwendungsberechtigung".
Mittels des Suchfeldes k�nnen Sie die Berechtigungen leicht ausw�hlen.

Funktionen
----------

:Schema ermitteln:

    Das Datenschema wird aus den Metadaten der Graph API (https://graph.microsoft.com/v1.0/$metadata) ermittelt.
    Dabei werden nicht alle Objekte zur Verf�gung gestellt, sondern nur eine aktuell gepr�fte Teilmenge.
    ID-Felder und Felder mit �nderungsinformationen werden gekennzechnet, damit diese in Prozessen genutzt werden k�nnen.

:Laden von Quelldaten:

    Mit dem Universalplugin k�nnen Daten gelesen werden. 
    Dabei ist auch eine Abfrage per �nderungsdatum m�glich.
    Daneben stehen spezielle Prozesse zur Verf�gung, die eine umfassende Synchronisation erm�glichen, 
    und neben Vorkommen einer Serie auch das L�schen von Ereignissen verarbeiten.

:Laden von Schema-basierten Daten:

    Speziell bei Ereignissen / Events wird die Abfrage �ber alle Benutzer einzeln ausgef�hrt.
    Die betreffenden Benutzer werden �ber eine Verbindungseinstellung festgelegt.
    Das genaue Verfahren wird in den Besonderheiten beschrieben.

:Laden von Abfrage-basierten Daten:

    Diese Funktion wird nicht unterst�tzt.

:Schreiben von Daten:

    Das Schreiben eines Ereignisses erfolgt �ber den Benutzer, der f�r das Lesen genutzt wurde.
    Bei der Neuanlage wird dieser Benutzer aus dem Feld Organisator entnommen.
    Ung�ltige Werte f�hren dabei zu einer Fehlermeldung.
    Die Anlage einer Serie ruft im Anschluss die Vorkommen des aktuellen Zeitfensters ab und speichert
    Informationen dazu im �nderungsspeicher.
    Dies erm�glich speziellen Prozessen die Vorkommen mit den Quelldaten abzugleichen.

:Schreiben von Bulk-Daten:

    Diese Funktion wird nicht unterst�tzt.


Einstellungen
-------------

Folgende Einstellungen m�ssen bereitgestellt werden.

:API Url:

    Definiert die Basis-Url aller Abfragen. Der Wert ist aktuell immer https://graph.microsoft.com

:Azure AD Mandanten ID:

    Diese ID definiert das Unternehmen und kann bei der Registrierung der Anwendung ausgelesen werden,

:Filter f�r Benutzer:

    Dieser Wert in OData-Notation definiert die Menge an Benutzer, f�r die Termine abgefragt und ggf. synchronisiert werden.
    Das genaue Vorgehen ist in den Bensonderheiten beschrieben.
    Folgender Wert w�hlt alle Mitglieder des Unternehmens aus: userType eq 'Member'

:Anzahl vergangener Monate:

    Diese Ganzzahl definiert den Anfang des Zeitfensters f�r Synchronisationsprozesse.
    Die Anzahl an Monaten wird bei kompletten Abfragen dem aktuellem Datum abgezogen.
    Je gr��er der Wert ist, umso gr��er kann das Datenvolumen sein.

:Anzahl zuk�nftiger Monate:

    Diese Ganzzahl definiert das Ende des Zeitfensters f�r Synchronisationsprozesse.
    Die Anzahl an Monaten wird bei kompletten Abfragen dem aktuellem Datum hinzugef�gt.
    Je gr��er der Wert ist, umso gr��er kann das Datenvolumen sein.

:Client-ID:
    
    Die Anwendungs-ID der registrierten Anwendung.

:Client-Geheimschl�ssel:

    Ein geheimer Schl�ssel der registrierten Anwendung.

:Proxy Server:

    Adresse des Proxy-Servers f�r den Zugriff auf �ffentliche Adressen.
    Dieser Wert kann in einer On premise Installation erforderlich sein.

:Proxy Benutzername:

    Zugangsdaten zum Proxy Server.

:Proxy Passwort:

    Zugangsdaten zum Proxy Server.

Besonderheiten
--------------

Beim Lesen von Ereignissen gibt es folgendes zu beachten.
Ereignisse werden �ber eine Liste von Benutzern ermittelt.
Da ID eines Ereignisses abh�ngig vom Benutzer ist, �ber den die Abfrage ausgef�hrt wurde, wird die Antwort wie folgt verarbeitet.
Wenn der aktuelle Benutzer gleich dem Organisator des Ereignisses ist, wird der Datensatz �bernommen und die ID z.B. in 
Datenabbildungen verwendet.
Wenn der aktuelle Benutzer nicht gleich dem Organisator ist und der Organisator aber �ber den Benutzerfilter erfasst wird, 
wird der Datensatz verworfen.
Wenn der Organisator nicht durch den Benutzerfilter erfasst wird, wird der Termin �bernommen und alle Teilnehmer entfernt, 
die im Benutzerfilter enthalten sind und nicht dem aktuellen Benutzer entsprechen.
Dieses Verfahren stellt sich, dass auch geteilte Ereignisse sicher identifiziert werden k�nnen und keine Datens�tze 
doppelt verarbeitet werden.
Der Abfragen von Ereignissen mit Universalplugins erm�glicht nicht das Abfragen von Vorkommen einer Serie oder gel�schten Datens�tzen.

F�r die Synchronisation von Ereignissen k�nnen Prozesse die Delta-Funktion der CalendarView verwenden.
Diese Funktion ben�tigt ein definiertes Zeitfenster (siehe Einstellungen) und einen gespeicherten �nderungstoken.
Prozesse, die dies nutzen, speichern das letzte Abfragedatum der kompletten Abfrage.
Ab da wird �ber den �nderungstoken abgefragt, der intern gespeichert und bei erfolgreicher Verarbeitung auch aktualisiert wird.
Da das definierte Zeitfenster keine kontinuierliche Synchronisation erm�glicht, wird mit jedem neuen Tag eine komplette Abfrage ausgel�st 
und das Zeitfenster um einen Tag vorgeschoben.
Termine au�erhalb des Zeitfensters werden dann nicht von der Synchronisation erfasst.

Wenn die Delta-Funktion einen Termin als gel�scht ausgibt, wird dieser gezielt abgefragt.
Sollte er noch existieren, wurde er aus dem aktuellen Zeitfenster verschoben und wird mit verarbeitet.
Ohne Resultat wird der Termin als "gel�scht" verarbeitet.

Synchronisationsprozesse
------------------------

:doc:`/sync/graphzohosync`