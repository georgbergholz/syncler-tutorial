Konfiguration
=============

Über den Menüpunkt Einstellungen / Konfiguration erreichen Sie die Konfiguration Ihres Syncler-Accounts.
Im Syncler Administrator ist das im Kontextmenü des obersten Navigationseintrages als "Eigenschaften" enthalten.

Dort können Sie auf Einstellungen und Parameter zugreifen, die im Folgenden erläutert werden.

:Administrator E-Mailadressen: 
Es können mehrere Emailadressen mit Semikolon getrennt hinterlegt werden. 
Sollten keine abweichenden Adressen hier oder am Prozess definiert sein, werden alle Email an diese Adressen versendet.
Automatische Emails umfassen:

- Emails zu Fehlern bei Prozess- oder Datendienstausführung
- Tägliche Statusemail bei aktiver Prozessausführung
- Täglicher Warnungsbericht bei aktiver Prozessausführung. Diese wird nur versendet, wenn Fehler oder Warnungen in den vergangenen 24 Stunden protokolliert wurden.

:Mandant ID:
Die Mandant ID wird für den Zugriff auf die API für die Authentifizierung benötigt.
Dort wird sie als Client ID bei der Anforderung eines Tokens angegeben.

Siehe :doc:`/api/index`

:Mandant Schlüssel:

Der Mandanten-Schlüssel wird für den Zugriff auf die API für die Authentifizierung benötigt.
Dort wird sie als Client Secret bei der Anforderung eines Tokens angegeben.

Siehe :doc:`/api/index`

:Abweichende E-Mailadressen für Fehlermeldungen:

Alle Emails zu Fehlermeldung werden an diese Emailadressen versendet.
Diese Emails werden beim Auftreten des Fehlers versendet.

:Abweichende E-Mailadressen für Warnungen:

Alle Emails zu Warnung werden an diese Emailadressen versendet.
Es wird eine tägliche Zusammenfassung zu Warnungen versendet.

:Abweichende E-Mailadressen für Statusberichte:

Die tägliche Status-Email wird an diese Emailadressen versendet.

:Absendername:

Sie können einen individuellen Absendernamen für Emails von Syncler definieren.

:Protokollierungsstufe für Prozessereignisse:

Sie können eine Protokollstufe für die Prozessausführung angeben.
Abhängig davon werden weniger oder mehr Protokolle zur Ausführung generiert und gespeichert.
Davon ist auch die Nachrichtenausgabe am Prozess betroffen.
Debug-Meldungen werden generell nur in der Nachrichtenausgabe dargestellt und nicht in den Protokollen gespeichert.
Details zu den Protokollstufen finden Sie im Bereich "Protokolle".

:Protokollierungsstufe für Datendienstereignisse:

Sie können eine Protokollstufe für die Datendienstausführung angeben.
Abhängig davon werden weniger oder mehr Protokolle zur Ausführung generiert und gespeichert.
Davon ist auch die Nachrichtenausgabe am Datendienst betroffen.
Debug-Meldungen werden generell nur in der Nachrichtenausgabe dargestellt und nicht in den Protokollen gespeichert.
Details zu den Protokollstufen finden Sie im Bereich "Protokolle".

:Sicherungsspeicher verwenden:

Syncler kann vor jeder Änderung eines Zieldatensatzes den Zustand im Zielsystem sichern und auch wiederherstellen.
Diese Backups werden in Ihrer Datenbank gespeichert und durch die Wartung werden auch ältere Einträge entfernt.
Die Backup sind auch einsehbar, um ggf. Änderungen nachzuvollziehen.
Diese Daten erhöhen den Speicherverbrauch der Datenbank.

:Datensatzkopie in Protokollen speichern:

Syncler kann zu jedem Protokolleintrag eine Kopie des Quelldatensatzes inkl. Transformationen speichern, sofern die Ausgabe einen Datensatz-Bezug hat.
Diese Kopie kann über die Protoklle eingesehen werden, um ggf. Änderungen nachzuvollziehen.
Diese Daten erhöhen den Speicherverbrauch der Datenbank.

:Datensatzkopie in Datenabbildung speichern:

Syncler kann zu jeder Datenabbildung eine Kopie des Quelldatensatzes inkl. Transformationen speichern.
Diese Kopie wird automatisch bei jeder Synchronisation aktualisiert und stellt den letzten bekannten Quell-Zustand dar.
Diese Daten können im Falle eines Konfliktes genutzt werden, um ausschließlich Änderungen in der Quelle und nicht Differenzen zwischen Quelle und Ziel zu übertragen.
Dies ist eine Option der Konfliktbehandlung.

:Datenbankgröße:

Das ist Ihre aktuelle Datenbankgröße.
Die Synchronisations- und eine ggf. vorhandene Hilfsdatenbanken werden summiert.

Siehe :doc:`/processes/maintenance`

:Kontingent:

Das ist Ihr aktuelles Transaktionskontingent.
Als Transaktion wird das Lesen eine Datensatzes und das Schreiben eines Datensatzes gewertet.
Sollten technologisch bedingt mehrere Lesevorgänge zu einem Datensatz erforderlich sein, wird dennoch nur eine Transaktion gezählt.
Sollte das Schreiben nicht ausgeführt werden müssen, da keine Änderungen festgestellt wurden, wird keine Transaktion gezählt.

:Seriendruck Kontingent:

Das ist Ihr aktuelles Kontingent für die Erstellung von Serienbriefen.
Hier ist auch die direkte Erstellung per API-Aufruf eingeschlossen.
Es wird jede Ausführung gezählt, unabhängig von der Anzahl der Datensätze.

:Maximale Datenbankgröße in MB:

Sobald die maximale Datenbankgröße erreicht wird, kann kein Prozess ausgeführt werden. 
Es wird beim Versuch einen Prozess zu starten eine Fehlermeldung generiert und ggf. versendet.

Siehe :doc:`/processes/maintenance`

:Sprache:

Diese Sprache wird für die Darstellung der Oberfläche und für die Ausgabe von Nachrichten und Protokollen genutzt.