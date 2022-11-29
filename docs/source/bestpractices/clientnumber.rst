Die laufende Nummer des Mandanten (Draft)
=================================

Diese Nummer an Prozessen struktuiert die synchronisierten Daten in Mandanten.
In Systemen wie Sage CRM, CAS oder Salesforce können die Sync-Statusfelder zu den Stammdaten nummeriert angegeben werden und beziehen sich auf diese Nummer.
Dies steuert, welche Prozesse auf den Datensatz zugreifen dürfen und damit auch, welches Ziel der Datensatz hat.
Diese Nummer wird aber auch für Datenabbildungen verwendet.
Ein Prozess sucht nur nach vorhandenen Datenabbildung für seine laufende Nummer und auch nur diese Datenabbildungen
werden ggf. erzeugt oder aktualisiert.
Durch die Verwendung von unterschiedlichen Nummern können Datensätze dadurch auch gezielt doppelt angelegt werden.

Folgende Beispiele sollen die Verwendung der Nummer veranschaulichen.

