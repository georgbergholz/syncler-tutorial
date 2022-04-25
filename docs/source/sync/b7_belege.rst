Sage Bäurer b7 Belege
=====================

Für die Objekte Angebot, Auftrag und Rechnung können zusätzliche Selektionskriterien definiert werden, um die Daten zu filtern.
Die Angabe wird im Filterfeld des jeweiligen Prozesses in Feld-Notation eingegeben.

Beispiel: datvon|:|2022-04-01T00:00:00+0100|;|


Angebote
--------

Folgende Kriterien sind für Angebote verfügbar.

:kontoid:

	eindeutige ID eines Kunden / Interessenten

:konto:

	Kontonummer eines Kunden / Interessenten, die in der Regel nur mit Angabe einer Satzart eindeutig ist

:satzart:

	Kontoart („1“ = Kunde, „4“ = Interessent)

:offer_id:

	eindeutige ID eines Angebots; entspricht dem DB-Feld „aufnr“ unter Berücksichtigung der für diesen UseCase fixen Vorgangsart für Angebot

:datvon:

	Die Angabe eines Zeitpunktes ermöglicht die Einschränkung auf „neuere“ Datenobjekte, d.h. Angebotsdatum ist gleich oder größer.Beispiel: "2019-01-01T00:00:00+0100"

:nur_offen:

	Mögliche Werte sind true oder false. Bei true werden nur offene Angebote abgestellt.


Aufträge
--------

Folgende Kriterien sind für Aufträge verfügbar.

:kontoid:

	eindeutige ID eines Kunden

:konto:

	Kontonummer eines Kunden, die in der Regel nur mit Angabe einer Satzart eindeutig ist

:satzart:

	Kontoart („1“ = Kunde, „4“ = Interessent nicht möglich)

:order_id:

	eindeutige ID eines Auftrags; entspricht dem DB-Feld aufnr unter Berücksichtigung der für diesen UseCase fixen Vorgangsart für Auftrag

:datvon:

	Die Angabe eines Zeitpunktes ermöglicht die Einschränkung auf „neuere“ Datenobjekte, d.h. Auftragsdatum ist gleich oder größer.Beispiel: "2019-01-01T00:00:00+0100"

:nur_offen:

	Mögliche Werte sind true oder false. Bei true werden nur offene Aufträge abgestellt.


Rechnungen
----------

Folgende Kriterien sind für Rechnungen verfügbar.

:kontoid:

	eindeutige ID eines Kunden

:konto:

	Kontonummer eines Kunden, die in der Regel nur mit Angabe einer Satzart eindeutig ist

:satzart:

	Kontoart („1“ = Kunde [„4“ = Interessent nicht möglich]

:order_id:

	eindeutige ID eines Auftrags; entspricht dem DB-Feld aufnr unter Berücksichtigung der für diesen UseCase fixen Vorgangsart für Auftrag

:rg_nr:

	Rechnungsnummer

:rg_dat_von:

	Die Angabe eines Zeitpunktes ermöglicht die Einschränkung auf „neuere“ Datenobjekte, d.h. Rechnungsdatum ist gleich oder größer.Beispiel: "2019-01-01T00:00:00+0100" 





