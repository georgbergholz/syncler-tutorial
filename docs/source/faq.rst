Fragen und Antworten
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

