Release 4.3.6 - 15.02.2022
==========================

Änderungen
----------

Die Zoho Verbindung prüft das Schema Price und führt selbständig ein PUT statt POST aus.
Damit kann das Schema Price auch in Universalprozessen genutzt werden.

Sage 100 Belegübertragung:
Das Verhalten zu Ansprechpartnern und Adressfeldern wurde geändert.
Der Zusatz für A0, A1 und A2 wird nicht mehr vom Ansprechpartner überschrieben.
Im Belegrequestobjekt ist die Property "A1AdressNummer" hinzugekommen. 
Hier kann nun optional eine dem Auftraggeber zugehörige abweichende Lieferanschrift mitgegeben werden. 
Wird nichts übermittelt bleibt die A1AdressNummer auf der Adresse des Auftraggebers stehen.
Der Ansprechpartner der abweichenden Lieferanschrift muss immer in Bezug zur A1AdressNummer stehen. 

Die Universal SDK-Prozesse wurden im Verhalten den Universalprozessen angeglichen bzgl. Rückschreiben, Bedingungen und Änderungsspeicher.

Es steht eine rudimentäre Verbindung zu EmarSys zur Verfügung. Diese kann Kontakte übertragen oder aktualisieren.
Außerdem können Events getriggert werden.

Die REST Verbindung unterstützt das Anmeldeverfahren WSSE UsernameToken.

Die SDK-Verbindung hat generische Parameter für Zugangsdaten, 
damit diese den Passwortschutz nutzen können und nicht im Skript enthalten sein müssen.

Die REST Verbindung hat einen neuen Parameter "Immer alle Felder senden". 
Damit wird im Update-Fall ein vollständiges Objekt versendet, statt ausschließlich ein Delta-Objekt.

Für Sage b7 werden Datensätze mit unbestimmter Datenabbildung wiederholt und nicht übersprungen.
Unbestimmte Datenabbildungen liegen vor, wenn auf eine Insert-Nachricht noch keine Antwort zur Verfügung steht.

Für IDoc werden Datensätze mit unbestimmter Datenabbildung wiederholt und nicht übersprungen.
Unbestimmte Datenabbildungen liegen vor, wenn auf eine Insert-Nachricht noch keine Antwort zur Verfügung steht.

Mit der Übersetzung "SisDataServiceDropdown" = Y kann im ERP-Fokus für Sage CRM die Registerkartenleiste durch ein Dropdown-Menü ersetzt werden.

Es steht eine neue Transformation "HTML zu Text" zur Verfügung.

Die Sage CRM Verbindung unterstützt geschachtelte Daten für das Kommunikationsobjekt. 
Die Teilnehmer (Comm_Link) werden als geschachtelte Liste behandelt.
Zusätzlich wird der Organisator automatisch zu den Teilnehmern.

Die Zoho Verbindung unterstützt das Abfragen von gelöschten Daten.
Über das Schema und einen spezifischen Prozess können gelöschte Daten abgefragt werden.
Neben der ID beinhaltet die Antwort noch den Anzeigenamen des Datensatzes.

Die Email-Verbindung enthält das Feld FileContent in der MimeMessage. 
Dieses wird beim Lesen mit einer EML-Version in Base64 der Email gefüllt.

Die CAS Verbindung enthält das Feld FileContent im Objekt EMAILSTORE.
Zugewiesene Daten werden als Email in CAS archiviert.

Es steht ein neuer Prozess "Universal Sync Prozess für Email" zur Verfügung.
Dieser Prozess basiert auf dem Universalprozess und verarbeitet eingehende Emails.
Abweichend zum Basisprozess wird keine komplementäre Richtung oder Konflikte berücksichtigt.
Außerdem können verarbeitete Emails gelöscht oder verschoben werden.

Im Schema der REST Verbindung kann per Wert "NestedList" definiert werden, 
welche Unterliste das Alleinstellungsmerkmal bekommt. Diese Eindeutigkeit ist für Belegprozesse relevant.

Die Zoho Verbindung unterstützt das Schemaobjekt Photo.
Der Prozess "Hotfolder nach Zoho Foto" erlaubt den Upload von Fotos aus einem Verzeichnis.
Modulname und Modul-ID müssen per Transformation bestimmt werden.

Die Zählung von lesenden Transaktionen wurde von eine physischen auf eine logische Anzahl umgestellt. 
Bisher haben die Verbindungen jedes Lesen gezählt. 
Jetzt wird das Lesen über die Prozess-Zusammenfassung gezählt und hat damit einen direkten Bezug zur Ausführungshistorie.
Lesen zum Anreichern von Daten in der Verbindung werden nicht mehr extra gezählt.

Das Produkt-Schema in der Sage CRM Verbindung unterstützt einen Standardpreis für Standardpreisliste und Standardmengeneinheit. 

Der Refresh-Token der Sage 200 Verbindung wird direkt in der Verbindung ermittelt.

Der neue Feldtyp "Array" ermöglicht die Verarbeitung von Json-Arrays. 
Der String wird abhängig von der Verbindung als JArray verarbeitet.

Prozesse zu SQL Hauptobjekt legen keine parallelen Mappings mehr an und prüfen eine Änderungsinformation gegen die 
eigene Datenabbildung für die Feststellung der Synchronität.

In der SQL-Verbindung können für das Hauptobjekt optional ID-Felder angegeben werden.
Durch die Abfrage ermittelte ID-Felder haben weiterhin Priorität.

Es steht eine neue Transformation "Formel ausführen" zur Verfügung.
Mittels Platzhalter kann eine Formel in SQL-Notation definiert werden.
Das Resultat wird als Feld übernommen.
Möglich sind dadurch mathematische Operationen oder auch Zeichenkettenoperationen.


Korrekturen
-----------

Die Erfolgsrückmeldung zu Sage 100 Belegübertragung war unvollständig, 
wodurch die Statistik in der Warteschlange unvollständig war.

Das Laden aller Datensätze in der Sage 100 Verbindung ignoriert den Parameter LAST_SYNC_VERSION.
Dieser wurde standardmäßig aus den Universalprozessen übergeben, was dazu geführt hat, das statt allen Daten nur Änderungen geladen wurden.

Der API Endpunkt StartProcessDirect schreibt das Finish-Datum in den Warteschlangendatensatz.

Beim Speichern von Verbindungen hat die API keine Anreicherung mit Schemaobjekten zurückgeliefert.

Der Universalprozess für geschachtelte Daten hat den Source-Lock nicht aktualisiert. 
Dadurch konnten Datensatzsperren erhalten bleiben.

In der CRM-Verbindung wurde die Order und Quote ID bei der Aktualisierung von Positionen übergeben.
Das hat im CRM eine Fehlermeldung ausgelöst.

Für CAS werden LinkTo und LinkFrom nicht übergeben, falls die Partner ID leer ist. 
Dies beugt einer Fehlermeldung vor.

Datendienste mit Berechtigungsgruppen wurden im ERP-Fokus nicht als Registerkarten dargestellt, die die Abfrage danach den leeren Fall nicht berücksichtigt hat.

Die Übernahme der transformierten Daten wurde intern korrigiert. 
Felder mit beliebiger Schachtelungstiefe wurden nicht berücksichtigt.


