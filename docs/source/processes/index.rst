Die Prozesse
====



Prozesstypen
----
Es gibt verschiedene Typen von Prozessen, die sich in Konfiguration und Verwendung unterscheiden.

:Schema-basierter Synchronisationsprozess:

:Abfrage-basierter Synchronisationsprozess:

:Synchronisationsprozesse f�r geschachtelte Daten:

:Ablauf-basierter Prozess:

:Sonstige Prozesse:

Das Prozesskonzept in der Synchronisation
----


Universalprozess oder spezifischer Prozess
----

Es gibt spezifische Prozesse unter den Plugins, die die System- und Objekttypen genau festlegen.
Diese Konstellation kann i.d.R. auch �ber den Universalprozess konfiguriert werden.
Die spezifischen Prozesse f�hren aber auch zus�tzliche Pr�fungen aus oder speichern weitere Daten, damit die Konsistenz im Zielsystem sichergestellt ist.
Sie sollten immer den spezifischen Prozess bevorzugt einrichten, damit es nicht zu inkonsistenten Zust�nden kommen kann.
Eine genaue Beschreibung, was der spezifische Prozess automatisch vorsieht, kann der jeweiligen Dokumentation entnommen werden.

Prozesse im Detail
----

.. toctree::

    sync/inxmail
    sync/cas_bc

