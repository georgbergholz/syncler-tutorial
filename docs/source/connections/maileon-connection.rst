Maileon
=======

Maileon ist eine E-Mail-Marketing Lösung für professionelle Newsletter und Marketing Automation.
Diese Verbindung realisiert die Anmeldung und Kommunikation mit der API und stellt ein Datenschema 
mit zusätzlichen Funktionen bereit.
Für die Integration mit anderen Verbindungen können die Univeral Prozesse verwendet werden.

Funktionen
----------

:Schema ermitteln:

    Das Datenschema wird fest von der Verbindung erstellt.
    Benutzerdefinierte Kontaktfelder werden dynamisch beim Erstellen des Schemas eingelesen.
    Die Funktion zum Anlegen von Kontaktfeldern erweitert das interne Datenschema automatisch.
    Das Datenschema ist eine Kombination aus lesbaren Feldern, angereicherten Feldern, 
    übergebbaren Parametern, z.B. beim Speichern von Daten und zusätzlichen Parametern, 
    die Funktionen direkt ansteuern können.
    Unter Datenobjekte steht eine Detailbeschreibung zur Verfügung.

:Laden von Quelldaten:

    Abhängig von Datentyp können Listen, einzelne Datensätze oder Änderungen abgerufen werden.
    Unter Datenobjekte steht eine Detailbeschreibung zur Verfügung.

:Schreiben von Daten:

    Mittels dem schreiben von Daten werden Datensätze angelegt, geändert oder auch Funktionen
    aufgerufen.
    Unter Datenobjekte steht eine Detailbeschreibung zur Verfügung.


Einstellungen
-------------

Folgende Einstellungen müssen bereitgestellt werden.

:API Key:

    Der API Key kann über die Benutzeroberfläche von Maileon ermittelt werden.
    Melden Sie sich dazu bei Maileon an und wechselnen Sie in den Bereich Einstellungen.
    Unter Konto / API-Keys können vorhandene API Keys ausgelesen oder neue angelegt werden.    

:Proxy Server:

    Adresse des Proxy-Servers für den Zugriff auf öffentliche Adressen.
    Dieser Wert kann in einer On premise Installation erforderlich sein.

:Proxy Benutzername:

    Zugangsdaten zum Proxy Server.

:Proxy Passwort:

    Zugangsdaten zum Proxy Server.

Datenobjekte
------------

Folgende Datenobjekte stehen zur Verfügung.

:Kontakt / contact:

Mit diesem Objekt können Kontakt in Maileon ausgelesen, angelegt, aktualisiert oder gelöscht werden.
Das Löschen eines Kontaktes erfordert die Einrichtung eines speziellen Löschprozesses.
Der Bereich custom_fields enthält die benutzerdefinierten Felder, welche auch mit der Verbindung und dem Objekt 
customfield angelegt werden können.

Die folgenden Felder werden als Parameter für das Anlegen oder Aktualisieren verwendet.

- **src** (Insert/Update: Eine Zeichenfolge, die die Quelle des Kontakts beschreiben soll.)
- **doimailing** (Insert/Update: Dieser Parameter wird ignoriert, wenn triggerdoi nicht angegeben oder falsch ist. Referenziert das zu verwendende doi-Mailing.)
- **subscription_page** (Insert: Falls diese Methode von einer Abonnementseite aufgerufen wurde, bietet diese Zeichenfolge die Möglichkeit, sie für die Verwendung in Berichten zu verfolgen.)
- **doi** (Insert: Gibt an, ob für den erstellten Kontakt ein Double-Opt-In-Prozess gestartet werden soll. Beachten Sie, dass der für diese Anfrage zurückgegebene Statuscode nicht bedeutet, dass der doi-Prozess erfolgreich war. Unterstützte Werte sind true und false.)
- **doiplus** (Insert: Dieser Parameter wird ignoriert, wenn doi nicht angegeben oder falsch ist. Falls der Doi-Prozess erfolgreich ist, darf Maileon Öffnungen und Klicks des Kontakts nachverfolgen.)
- **triggerdoi** (Update: Wenn bereitgestellt und wahr (unterstützte Werte sind wahr und falsch) und wenn die Berechtigung entweder 1, 2, 3 oder 6 ist, wird die Berechtigung direkt gesetzt und es wird KEINE DOI-Mail gesendet, da sie für diese Berechtigungen nicht erforderlich ist. Wenn die Berechtigung auf 4 (doi) oder 5 (doi+) gesetzt ist, wird ein doi-Prozess für den Kontakt ausgelöst, anstatt die Berechtigung sofort auf 4 oder 5 zu setzen (nochmals: die Berechtigung wird nicht geändert).)

