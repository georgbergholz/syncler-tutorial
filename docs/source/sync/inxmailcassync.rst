Synchronisation zwischen Inxmail und CAS (Draft)
========================================


Übertragung von Listen mit identischem Namen nicht möglich: Ressource bereits vorhanden.

Anlage von Empfängern mit identischer Emailadresse überschreibt vorhandenen ohne Vorwarnung.
Syncler gibt Fehlermeldung und Verweis aus. Weitere Korrektur erfolgt nicht.


    Die Basis im CAS wird dafür über vier Datensatztypen realisiert:
    - Adressen, welche die Empfänger innerhalb der Empfängerlisten umfasst
    - Verteilter, welcher im Inxmail die Empfängerliste darstellt
    - Newsletter, welche Mailings darstellen und an Empfängerlisten gesendet werden
    - Response, welche das Feedback der Empfänger aus diesem Mailing darstellt
    Innerhalb verschiedener Prozesse wird dann in beide Richtungen ein Informationsaustausch eingerichtet. Gängige Beispiele:
    - Verteiler können bidirektional synchronisiert werden, d.h. Bestände können jeweils aus beiden Systemen übernommen werden
    - Adressen, vorwiegend Ansprechpartner, welche in einem Verteiler enthalten sind, können per Übertragung des Verteilers in die Synchronisation aufgenommen und dauerhaft aktuell gehalten werden
    - Newsletter werden in Abhängigkeit zu den Verteilern und Adressen regelmäßig auch in CAS synchronisiert
    - Responses, welche daraus entstehen, werden ebenfalls aus Inxmail an des jeweilige Mailing im CAS übertragen
    - Anhand der im CAS dadurch vorhandenen Daten, können wiederum neue Verteiler mit Empfängern im CAS erstellt und dann an Inxmail übergeben werden.
    Auch Auswertungen und Darstellungen sind möglich:
    - Es können Kennzahlen über Empfänger, Abmeldungen oder weitere Zahlen am Mailing dargestellt werden
    - Es kann die komplette Sendungsstatistik aus Inxmail im CAS dargestellt werden
    - Eigene Kennzahlen, Reports und Diagramme können nach Wunsch auf Basis der Daten angezeigt und angelegt werden
