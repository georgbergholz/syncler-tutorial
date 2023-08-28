On-Premises Version
===================

Die On-Premises Version kann lokal installiert werden.
Dies wird mit einer Windows-Installationsroutine unterstützt.
Die Anwendung kann aber auch in einer Linux-Umgebung eingesetzt werden.
Hier erfolgt die Bereitstellung der Anwendung und der Web-API manuell.

Damit die installierte Version verwendet werden kann, wird eine Lizenz benötigt.
Diese kann bei Sellmore erworben werden.

Durch die Windows-Installationsroutine werden die Hauptanwendung (Daemon), die Web-API (Service) und der Desktop-Administrator
in einem Windows-Betriebssystem installiert.
Die Anwendungen setzen .Net-Core SDK 3.1 und .Net-Framework 4.7.2 voraus.

Durch die Installationsroutine wird kein Datenbanksystem installiert.
Sie können einen SQL-Server oder eine MariaDB für den Syncler verwenden.
Beides muss eigenständig installiert und konfiguriert werden.
Bei der ersten Einrichtung des Synclers mit dem Desktop-Administrator konfigurieren Sie die Zugangsdaten und den Typ des Datenbanksystems.
Die Datenbank wird dann automatisch mit dem angegebenen Namen erzeugt, falls diese nicht bereits existsiert.
Alles weitere erfolgt automatisch.

Die Installationsroutine registriert zwei Windows-Dienste.

Der Windows-Dienst "Syncler Windows Daemon" ist die Hauptanwendung.
Diese Anwendung ist für die Ausführung von Prozessen, Datendiensten und Projekten zuständig.
Sie kommuniziert ausschließlich über die Datenbank und besitzt keine eigenen Schnittstellen.

Der Windows-Dienst "Syncler Windows Service" stellt die Web-API des Synclers mit einem Kestrel-Webserver bereit.
In der Grundeinstellung ist diese über http://localhost:3030/SisService aufrufbar.
Der Listen-Port der Web-API kann über die Syncler-Konfiguration geändert werden.
Eine Änderung des Ports erfordert den Neustart des Windows-Dienstes.

Die Web-API ist die Schnittstelle für alle Zugriffe auf den Syncler und wird auch vom Desktop-Administrator genutzt.
Sie stellt Endpunkte für die Konfiguration, Push-Nachrichten, IDoc-Nachrichten, ERP-Fokus-Zugriffe oder Webhooks bereit.
Die Schnittstellen-Dokumentation kann über http://localhost:3030/SisService/swagger/index.html aufgerufen werden.
In bestimmten Endpunkten wird eine "TenantId" benötigt. Diese lautet bei lokalen Installationen immer "Master".

Für einen Zugriff auf die Web-API kann direkt der Kestrel-Server verwendet werden.
Dazu muss der definierte Port in den beteiligten Firewalls freigegeben werden.

Es besteht aber auch die Möglichkeit, den Zugriff durch einen Reverse-Proxy bereitzustellen.
Dies ist in zentral-verwalteten Infrastrukturen von Vorteil.

Im IIS können Sie dazu eine Anwendung hinzufügen, die eine URL Rewrite InboundRule definiert.
Diese leitet den externen Zugriff dann auf die lokal definierte Adresse inklusive des Listen-Ports weiter.



.. toctree::
    :titlesonly:
    
    configuration
