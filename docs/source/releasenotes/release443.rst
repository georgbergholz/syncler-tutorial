Release 4.4.3 - 24.01.2023
==========================

Änderungen
----------

Der Prozess "Sage CRM ABC-Analyse"

* Dieser neue Prozess setzt auf dem Addon ABC-Analyse für Sage CRM auf und aktualisiert Firmen gemäß der definierten Kriterien und dem erreichten Scoring.

Die Zoho-Verbindung

* Eine Feldnotation für gefilterte Abfragen, z.B. aus der Transformation, kann direkt für die Einzelabfrage von Datensätzen genutzt werden.
* Die Beschreibung zu Terminen enthält den Betreff und das Datum, damit auch Serienvorkommen einfach unterschieden werden können.

Die CAS-Verbindung

* Für das Lesen und Löschen von Links wird der Parameter "Attribute" ausgewertet, um die korrekte Verknüpfung auszuwählen.

Die SAP-IDOC-Verbindung

* Für die Generierung der DOCNUM werden auch die Millisekunden verwendet, damit bei einer schnellen Folge von Dokumenten keine Dopplungen entstehen.

Die Email-Verbindung

* Beim Versand einer Email mit einem Datenobjekt wird der geparste Inhalt der Email zurückgeliefert und kann so für Archivierungen genutzt werden.

Der Zweitfilter wurde bei diesen Prozessen aktiviert.

* Sage CRM Marketing-Center Eintrag für Personen nach CleverReach Empfänger
* Sage CRM Marketing-Center Eintrag für Personen nach InxMail Empfänger
* InxMail Bounce nach Sage CRM Marketing-Center Gruppe
* InxMail WebBeaconHit nach Sage CRM Marketing-Center Gruppe
* InxMail Klick nach Sage CRM Marketing-Center Gruppe
* InxMail Abmeldung nach Sage CRM Marketing-Center Gruppe

Bei diesen InxMail-Prozessen wird ein Skip ausgelöst, wenn keine Listen-ID vorhanden ist.
Dies kann passieren, wenn die Liste in InxMail gelöscht wird und Resultate dazu abgerufen werden.

* InxMail Bounce nach Sage CRM Marketing-Center Gruppe
* InxMail WebBeaconHit nach Sage CRM Marketing-Center Gruppe
* InxMail Klick nach Sage CRM Marketing-Center Gruppe
* InxMail Abmeldung nach Sage CRM Marketing-Center Gruppe

Die ActiveCampaign-Verbindung

* Diese neue Verbindung ermöglicht die Anbindung des E-Marketing-Anbieters ActiveCampaign.
* Synchronisationen können mit dem Universalprozess eingerichtet werden.
* Für die Kombination mit CAS stehen bereits Vorlagen zur Verfügung.
* Siehe :doc:`/connections/ac-connection`

Für die Erzeugung eines unbedenklichen Feldnamens für Abfrageergebnisse wird eine neue Methode eingesetzt, die folgende Sonderzeichen ersetzt: . : ? % - + * | ( ) [ ] / \ "
Diese Methode wird in der REST API-, der Zoho- und der ActiveCampaign-Verbindung eingesetzt.

Die Graph-Verbindung

* Die Konfiguration der Verbindung wurde überarbeitet und kann jetzt durch verschiedene Auswahlen besser gesteuert werden.
* Das Anmeldeverfahren wird per Auswahl gesteuert und kann einen Admin- oder Benutzer-Refresh-Token verwenden.
* Der Benutzerkreis für Synchronisationen wird per Auswahl gesteuert und unterstützt die Benutzer-Refresh-Token.
* Der Scope kann konfiguriert werden, was durch die Unterstützung von Refresh-Token erforderlich wurde.
* Die Beschreibung zu Terminen enthält den Betreff und das Datum, damit auch Serienvorkommen einfach unterschieden werden können.
* Es steht eine schreibgeschützte Liste der vorhandenen Benutzer-Zustimmungen zur Verfügung. Dies soll eine Übersicht zu den synchronisierten Benutzern liefern.
* Das Objekt Event enthält das schreibgeschützte Feld "user", damit der Benutzerbezug in Transformationen ausgewertet werden kann. Dies ist z.B. bei externen Organisatoren und Zoho Terminen relevant, da der Host immer ein Benutzer sein muss.

Die Synchronisation zwischen Microsoft Graph und Zoho CRM, sowie Sage CRM wurde überarbeitet. Das bisherige Verfahren konnte zu Fehlern bei Serienterminen führen.

* Der Änderungsspeicher wird nicht länger verwendet.
* Eine neue oder geänderte Serie löscht ggf. die vorhandene Serie im Ziel komplett und legt diese neu an. Danach werden alle Instanzen der Serien abgeglichen, um Ausnahmen und Lücken zu übertragen. Der Abgleich erzeugt auch die Datenabbildungen zwischen den Vorkommen.
* Eine Neuanlage von Vorkommen außerhalb der Serienverarbeitung findet nicht statt.

Der Syncler-Administrator

* Es steht eine neue Liste für die internen Parameter zur Verfügung, die z.B. Delta- oder Refresh-Token verwendet werden.
* Die Protokoll-Listen wurden in Allgemein, Prozesse, Datendienste und Webhooks aufgetrennt.

Die Synchronisation zwischen Sage CRM Marketing-Center und CleverReach oder InxMail

* Die betroffenen Prozesse prüfen das Änderungsdatum der Quelle gegen die Datenabbildung und überspringen ggf. den Datensatz.
* Das Zurückschreiben der Referenz-ID erfolgt nur bei unterschiedlichen Werten.
* Das Abfragen von geänderten Gruppeneinträgen wählt Einträge ohne Referenz-ID unabhängig vom Datum aus. Damit soll eine zeitliche Differenz zwischen der Synchronisation der Gruppe und der Gruppeneinträge kompensiert werden.

Die eingehenden Webhooks

* Diese neue Funktion bietet die Möglichkeit eingehende Webhooks zu definieren, um eine einfache Integration in externe Systeme zu ermöglich.
* Webhooks können dabei lesend oder schreibend verwendet werden.
* Die ein- oder ausgehenden Daten können dabei flexibel als JSON-Objekt definiert werden.
* Es stehen auch zwei spezielle Prozesse für die Webhook-Funktion zur Verfügung, damit die Verarbeitung mit einer Transformation kombiniert werden kann.
* Siehe :doc:`/webhooks`

Der Prozess "Sage 100 VK-Preis nach Sage CRM Preis" wurde komplett überarbeitet und mit einem Initial-Prozess ergänzt. Dies dient vorallem der Leistungssteigerung.

* Die neue Version verzichtet vollständig auf Datenabbildungen, um die Leistung zu steigern. Ein Preis wird eindeutig durch die Mengeneinheit, das Produkt und die Preisliste definiert. Eine Verdichtung wird nicht mehr unterstützt (Übereinstimmungsregeln).
* Die betrachteten Preislisten können direkt im Prozess mit einem neuen Parameter gefiltert werden.
* Der Initial-Prozess fragt immer alle Preise und Datenabbildungen von Artikeln und Preislisten ab. Damit werden Negativabfragen für untergeordnete Preislisten und mehrfache Datenbankabfragen vermieden.

Die CSV-Prozesse

* Neue Felder aus der Transformation werden dem Export hinzugefügt.
* Der Parameter "Export-Feldliste" kann neben der Feldauswahl auch die Feldreihenfolge steuern.

Die Sage b7-Prozesse

* Durch einen neuen Parameter kann das Auslesen des Änderungsspeichers ohne Berücksichtigung des Datums erfolgen. Dadurch gehen keine Daten verloren.

Die Sage b7-Verbindung

* Durch einen internen Parameter wird verhindert, dass unterschiedliche Prozesse zeitgleich aus dem Service Bus Nachrichten abrufen.

Korrekturen
-----------

Die JSON-Konvertierung im SDK-Helper

* Die automatische JSON-Konvertierung für den SDK-Helper und der SDK-Funktionalität hat für das Resultat nur das bekannte Datenschema verwendet. Neue Felder aus der SDK-Verarbeitung wurden nicht berücksichtigt.

Die JSON-Konvertierung

* Die Datentypen Array und Objekt, die als Feld definiert wurden, wurden nicht übernommen.

Der Prozess "Microsoft 365 Aufgaben nach Sage CRM Aufgaben"

* Die Uhrzeit für die Aufgabenbenachrichtigung wurde nicht übernommen.

Der SDK-Helper

* Die Methoden InvokeGetData und InvokeSetData haben eine fehlerhafte URL verwendet.

Die Salesforce-Verbindung

* Bei Aktualisierungen wird die Spalte "id" generell nicht in die Feldliste übernommen.

Der Prozess "Salesforce Opportunity nach SAP Beleg"

* Das Element "E1EDP05" in den Positionen wird nicht übernommen, wenn das Feld "KSCHL" den Wert "ZPR0" hat. Dies ist Teil der Preisberechnung und verhindert eine Fehlermeldung in der IDOC-Verarbeitung.

Der Prozess "Zoho CRM Meeting nach Microsoft Graph Ereignis"

* Vermeindlich endlose Serien in Zoho liefern als Enddatum eine -1. Das wurde nicht in einen gültigen Wert überführt. Da eine endlose Serie dennoch eine beschränkte Anzahl an Vorkommen hat, wird diese Serie mit dem maximalen Enddatum aller Vorkommen angelegt.

Die CSV-Verbindung

* Zeilenumbrüche werden bei der Schema-Generierung aus den Feldnamen entfernt.

Die Funktion "Zurücksetzen der Sync-Infos" überspringt Einträge mit Graph-Sync-spezifischen Parametern, da dies ansonsten zu einer Störung der Synchronisation führen würde.

Die ID-Werte in den Datenabbildungen zu Microsoft 365 Objekten werden case-sensitive behandelt.

Der Bulk-Abfrage-Prozess

* Für die Fehlerbehandlung "Fehler ignorieren" werden keine Änderungsdatensätze mehr angelegt.

Behandlung von Nachfolgeprozessen durch Abfrageprozesse

* In der Release 4.4.2 ist ein Fehler entstanden, wodurch der Änderungsdatensatz nicht dem Nachfolgeprozess zugeordnet wurde. Der erste Prozess hat den Datensatz ein zweites Mal verarbeitet und erst dann an den Nachfolger übergeben. Sollten ID-Felder definiert sein, hat der Nachfolger bereits bei der ersten Ausführung den Datensatz verarbeitet.

