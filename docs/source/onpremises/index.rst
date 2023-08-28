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
Bei der ersten Einrichtung des Synclers konfigurieren Sie die Zugangsdaten und den Typ des Datenbanksystems.
Die Datenbank wird dann automatisch mit dem angegebenen Namen erzeugt, falls diese nicht bereits existsiert.
Alles weitere erfolgt automatisch.





.. toctree::
    :titlesonly:
    
    configuration
