Fragen und Antworten (Draft)
====================


Was ist beim Kopieren von Verbindungen zu beachten?

    Das Kopieren schließt gesicherte Daten, wie Passwörter, nicht mit ein.
    Diese müssen erneut eingegeben werden.

Was ist bei der Gesamtanzahl von zu verarbeitenden Datensätzen zu beachten?

    Die Anzahl wird bei bekannten ID-Werten über eindeutige ID-Werte ermittelt.
    Falls die Quelle aber Dubletten liefert, die durch den Prozess nicht eliminiert werden können, 
    stimmt die Gesamtanzahl und die Anzahl der verarbeiteten Datensätze nicht mehr überein.

Die Ausführung eines C#-Skripts liefert mir trotz Umwandlung keine UTC-Zeit zurück.

    Der Resultat der Skript-Ausführung durchläuft einen Umwandlungsprozess.
    Dabei geht die Zeitzonen-Information aus reinen DateTime-Werten verloren und das Resultat wird
    in die lokale Zeit konvertiert.
    Um den UTC-Wert zu erhalten können Sie folgendes verwenden.

.. code-block:: C#

    InputValues["Datum"] = new DateTime(Datum.ToUniversalTime().Ticks, DateTimeKind.Local);

Die Ausführung eines C#-Skriptes liefert mir die Fehlermeldung "Connection refused".

    Für die Ausführung von C#-Skripten sind die Ressourcen für Speichernutzung und Ausführungsdauer beschränkt.
    Sollten die Grenzwerte durch Ihr Skript überschritten werden, führt das zum Abbruch der Ausführung.
    In diesem Fall sollte das Skript bzgl. Speichernutzung und Laufzeit kontrolliert und ggf. angepasst werden.
    Einfache Berechnungen können z.B. auch durch Transformationen wie "Formel ausführen" umgesetzt werden.
    Sollte dies keine Abhilfe schaffen, wenden Sie sich an unseren Support.


