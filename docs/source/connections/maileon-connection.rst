Maileon
=======

Maileon ist eine E-Mail-Marketing Lösung für professionelle Newsletter und Marketing Automation.
Diese Verbindung realisiert die Anmeldung und Kommunikation mit der API und stellt ein Datenschema 
mit zusätzlichen Funktionen bereit.
Für die Integration mit anderen Verbindungen können die Universal Prozesse verwendet werden.


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


:Lesen von Schema-basierten Daten:

Abhängig vom Datentyp können Listen, einzelne Datensätze oder Änderungen abgerufen werden.
Unter Datenobjekte steht eine Detailbeschreibung zur Verfügung.


:Lesen von Abfrage-basierten Daten:

Diese Funktion wird nicht unterstützt.


:Schreiben von Daten:

Mittels dem Schreiben von Daten werden Datensätze angelegt, geändert oder auch Funktionen
aufgerufen. Unter Datenobjekte steht eine Detailbeschreibung zur Verfügung.


:Schreiben von Bulk-Daten:

Diese Funktion wird nicht unterstützt.


Einstellungen
-------------

Folgende Einstellungen müssen bereitgestellt werden.

:API Key:

Der API Key kann über die Benutzeroberfläche von Maileon ermittelt werden.
Melden Sie sich dazu bei Maileon an und wechseln Sie in den Bereich Einstellungen.
Unter Konto / API-Keys können vorhandene API Keys ausgelesen oder neue angelegt werden.


Datenobjekte
------------

Folgende Datenobjekte stehen zur Verfügung.

Das einzelne Abrufen von Datensätzen kann, falls unterstützt, mit den Standard-Prozessfeldern und folgender Notation
erfolgen.

.. code-block:: none

    id|:|1234|;|


:Kontakt / contact:

Mit diesem Objekt können Kontakte in Maileon ausgelesen, angelegt, aktualisiert oder gelöscht werden.
Das Löschen eines Kontaktes erfordert die Einrichtung eines speziellen Löschprozesses.
Der Bereich custom_fields enthält die benutzerdefinierten Felder, welche auch mit der Verbindung und dem Objekt 
customfield angelegt werden können.

Die folgenden Felder werden als Parameter für das Anlegen oder Aktualisieren verwendet.

- **src** Insert/Update: Eine Zeichenfolge, die die Quelle des Kontakts beschreiben soll.
- **doimailing** Insert/Update: Dieser Parameter wird ignoriert, wenn triggerdoi nicht angegeben oder falsch ist. Referenziert das zu verwendende doi-Mailing.
- **subscription_page** Insert: Falls diese Methode von einer Abonnementseite aufgerufen wurde, bietet diese Zeichenfolge die Möglichkeit, sie für die Verwendung in Berichten zu verfolgen.
- **doi** Insert: Gibt an, ob für den erstellten Kontakt ein Double-Opt-In-Prozess gestartet werden soll. Beachten Sie, dass der für diese Anfrage zurückgegebene Statuscode nicht bedeutet, dass der doi-Prozess erfolgreich war. Unterstützte Werte sind true und false.
- **doiplus** Insert: Dieser Parameter wird ignoriert, wenn doi nicht angegeben oder falsch ist. Falls der DOI-Prozess erfolgreich ist, darf Maileon Öffnungen und Klicks des Kontakts nachverfolgen.
- **triggerdoi** Update: Wenn bereitgestellt und wahr (unterstützte Werte sind wahr und falsch) und wenn die Berechtigung entweder 1, 2, 3 oder 6 ist, wird die Berechtigung direkt gesetzt und es wird keine DOI-Mail gesendet, da sie für diese Berechtigungen nicht erforderlich ist. Wenn die Berechtigung auf 4 (doi) oder 5 (doi+) gesetzt ist, wird ein doi-Prozess für den Kontakt ausgelöst, anstatt die Berechtigung sofort auf 4 oder 5 zu setzen (nochmals: die Berechtigung wird nicht geändert).

Kontakte können als einzelne Datensätze oder Liste abgerufen werden.
Das Abrufen von geänderten Kontakten per Prozess wird ebenfalls unterstützt.
Checksummen werden beim Lesen nicht verwendet.

Das Filtern oder Suchen von Kontakten kann in den Standard-Prozessfeldern mit folgender Notation erfolgen.
Damit können gezielt Inhalte von Kontaktfiltern abgerufen oder einzelne Kontakte per E-Mail oder externer ID gesucht werden.

.. code-block:: none
    
    Suche nach Kontakten:
        emails|:|gesuchte@email.de|;|
        externalid|:|gesuchte_externe_id|;|

.. code-block:: none

    Abrufen eines Kontaktfilters:
        contactfilterid|:|kontaktfilter_id|;|


:Benutzerdefiniertes Feld / customfield:

Dieses Objekt kann nur für die Anlage oder das Umbenennen eines benutzerdefinierten Feldes genutzt werden.
Eine Abfrage über die Lesen-Funktion der Verbindung ist nicht vorgesehen und wird immer ein leeres Ergebnis liefern.

Folgende Felder stehen zur Verfügung.

- **name** Der Name des Feldes.
- **oldname** Für den Fall, dass ein vorhandenes Feld umbenannt werden soll, wird hier der aktuelle Name erwartet.
- **type** Definiert den Datentyp des Feldes. (string / integer / float / date / boolean)

Beim Schreiben dieses Objektes über die Verbindung wird automatisch auch das Schema des Kontakt-Objektes aktualisiert.
Eine manuelle Aktualisierung ist nicht erforderlich.


:Kontaktfilter / contactfilter:

Dieses Objekt kann ausgelesen und aktualisiert werden. Die direkte Anlage wird nicht unterstützt.
Allerdings kann ein Kontaktfilter über die Verteilerliste automatisiert angelegt werden. Details dazu finden Sie beim Objekt
Verteilerliste.
Das Löschen eines Kontaktfilters erfordert die Einrichtung eines speziellen Löschprozesses.

Bei der Aktualisierung kann ausschließlich der Name des Kontaktfilters verändert und ein Refresh der Kontakte ausgelöst werden.

-**refresh_contacts** Wird diesem Feld der Wert true beim Schreiben übergeben, wird die Aktualisierung der Kontakte des Kontaktfilters ausgelöst. Die Verwendung ist nur aller 10 Minuten möglich.

Kontaktfilter können einzeln abgerufen werden. 
Wird das Filtern oder Suchen mit den Standard-Prozessfeldern ausgelöst, wird der Wert direkt mit dem Names des
Kontaktfilters verglichen und alle Übereinstimmungen werden zurückgegeben.


:Verteilerlisten / targetgroup:

Dieses Objekt kann ausgelesen und aktualisiert werden.
Das Löschen einer Verteilerliste erfordert die Einrichtung eines speziellen Löschprozesses.
Für die Anlage einer Verteilerliste stehen zwei Verfahren zur Verfügung.

- **contact_filter_name** Kann bei Anlage zur Suche eines Kontaktfilters verwendet werden.
- **contact_filter_id** Kann bei Anlage zur Auswahl eines Kontaktfilters verwendet werden.
- **create_contact_filter** Erzeugt ggf. benutzerdefiniertes Feld und gleichnamigen Kontaktfilter, der der neu angelegten Verteilerliste zugeordnet wird.
- **contact_filter_fieldname** Definiert den Feldnamen des Kontaktfilters. Das Feld wird ggf. als Wahrheitsfeld für Kontakte angelegt. Sollte das Feld bereits vorhanden sein und einen anderen Typ haben, resultiert daraus eine Fehlermeldung.

Verteilerlisten können einzeln abgerufen werden.
Wird das Filtern oder Suchen mit den Standard-Prozessfeldern ausgelöst, wird der Wert direkt mit dem Names der
Verteilerlisten verglichen und alle Übereinstimmungen werden zurückgegeben.

Beim Erzeugen einer Verteilerliste mit dem Setzen der Felder contact_filter_name oder contact_filter_id muss
der Kontaktfilter bereits vorhanden sein, da es sonst zu einer Fehlermeldung kommt.
Werden für die Anlage die Felder create_contact_filter und contact_filter_fieldname verwendet, wird der gleichnamige Kontaktfilter
automatisch angelegt.

Der Name einer Verteilerliste muss eindeutig sein. Identische Namen führen bei Anlage oder Aktualisierung zu einer
Fehlermeldung.


:Berichte / reports:

Dies ist ein Oberbegriff für folgende Typen, die identisch verwendet werden können.

- open
- unique_open
- bounce
- unique_bounce
- click
- unique_click
- block
- unsubscription
- subscriber
- recipient

Abhängig vom Typ des Berichts steht der betreffende Kontakt als untergeordnetes Objekt im Schema zur Verfügung.
Außerdem werden die Einträge zu den Berichten mit dem Namen des Mailings **mailing_name** angereichert.

Bei Berichten können keine einzelnen Datensätze, sondern nur Listen abgerufen werden.
Das Schreiben und Löschen wird nicht unterstützt.
Sollte es bei der Verarbeitung im Prozess zu Fehlern oder Wiederholungen kommen, werden diese über den Änderungsspeicher
realisiert.

Für die Änderungsabfrage wird automatisch der Parameter **from_date** verwendet.
Alle Eingaben in Filter- und Suchfeldern eines Prozesses werden der verwendeten Url angehängt.
Damit können weitere Filter, wie z.B. mailing_id, to_date oder standard_field, realisiert werden.