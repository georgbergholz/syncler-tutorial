Warteschlangen (Draft)
==============

Die Ausführung von Prozessen oder Datendiensten wird mit einem Aktionseintrag in einer Warteschlange gestartet.
Es gibt jeweils eine Warteschlange für Prozesse und für Datendienste. 
Deren Abarbeitung kann separat über die Einstellungen gestartet oder gestoppt werden.

Warteschlangen werden kontinuierlich auf auzuführende Aktionen geprüft.
Nach der Ausführung bilden die Einträge ein Protokoll der jeweiligen Ausführung und speichern die gesammelten Statusinformation.
Für die Fehlerbehandlung werden historische Einträge auch genutzt, um fehlgeschlagene Verarbeitungen zu wiederholen.

Folgende Typen von Aktionen werden bei Prozessen unterschieden.

:Manuell:

Startet den Prozess einmalig mit den gleichen Parametern wie für eine zeitgesteuerte Ausführung.
Nachfolgerprozesse werden gestartet, aber eine Fehlerbehandlung über einen weiteren Aktionsdatensatz ist nicht vorgesehen.

:Einzelübertragung:

Startet die gezielte Verarbeitung eines Datensatzes durch den Prozess. 
Eine Fehlerwiederholung wird abhängig von der Konfiguration mit weiteren Aktionsdatensätzen realisiert.

:Geplant:

Ist die zeitgesteuerte Ausführung eines Prozesses. 
Die Anlage des nächsten geplanten Aktionsdatensatzes wird vom Prozess durchgeführt. 
Dieser berücksichtigt dabei die Einstellung zur Fehlerbehandlung.

:Nachfolger:

Bilden eine Prozesskette, wo der 1. Prozess die Zielmenge des folgenden Prozesses einschränkt. 
Dabei wird auf den Aktionsdatensatz des Vorgängers zugegriffen.

:Wiederholung:

Stellt eine Fehlerbehandlung dar, bei der aufgetretene Fehler die Ausführung sofort wiederholen soll. 
Die zeitliche Differenz beträgt dabei immer drei Minuten.

:Wiederherstellen:

Ruft die Rollback-Funktion eines Prozesses zu einen Sicherungsdatensatz auf. 
Diese Funktion steht nicht für alle Prozesse zur Verfügung.


Folgende Typen von Aktionen werden bei Datendiensten unterschieden.

:Manuell:

Startet den Datendienst einmalig mit den gleichen Parametern wie für eine zeitgesteuert Ausführung.

:Einzelübertragung:

Startet die Verarbeitung einer Datenabbildung durch den Datendienst.

:Geplant:

Ist die zeitgesteuerte Ausführung eines Datendienstes. 
Die Anlage des nächsten geplanten Aktionsdatensatzes wird vom Datendienst durchgeführt. 
Dieser berücksichtigt dabei die Einstellung zur Fehlerbehandlung.

:Wiederholung: 

Stellt eine Fehlerbehandlung dar, bei der aufgetretene Fehler die Ausführung sofort wiederholen soll. 
Die zeitliche Differenz beträgt dabei immer drei Minuten.
