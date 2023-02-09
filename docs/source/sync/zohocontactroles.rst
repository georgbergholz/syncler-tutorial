Zoho CRM - Kontakt-Rollen
=========================

Die Zoho CRM-Verbindung stellt das Schemaobjekt "Contact_Roles" zur Verfügung.
Hierbei handelt es sich nicht um ein Modul-Objekt, sondern um ein Funktionsobjekt zur Verwaltung von Kontakt-Rollen eines Abschlusses.

Jeder Abschluss kann eine beliebige Liste von Kontakt-Rollen besitzen.
Dies sind 1:n Verknüpfungen zu Kontakten, die zusätzlich noch mit einer Rolle charakterisiert werden können.

Die Kontakt-Rolle besitzt selbst keine ID, weshalb das Schemaobjekt eine zusammengesetzte ID aus Abschluss-ID (deal_id) und Kontakt-ID (contact_id) bereitstellt.
Auch eine Änderungsinformation steht hier nicht zur Verfügung.

Bei einer Abfrage von Kontakt-Rollen antwortet die Zoho CRM-API mit dem Kontaktdatensatz und fügt die Rolle als zusätzliches Feld hinzu.
Damit diese Daten auch genutzt werden können, beinhaltet das Schemaobjekt alle Kontaktfelder schreibgeschützt und zusätzlich noch die ID-Felder für Abschluss und Kontakt, 
sowie den Rollennamen zum Speichern oder Löschen einer Kontakt-Rolle.

Die Antwort liefert die ID der Rolle und nicht den Namen, wohingegen das Anlegen oder Bearbeiten nur den Namen der Rolle akzeptiert.
Deshalb stellt das Schemaobjekt beide Felder für ID (contact_role_id) und Name (contact_role_name) bereit und reichert die Daten auch entsprechend an.

Die Zoho CRM-Verbindung unterstützt das Lesen von Kontakt-Rollen (Liste) eines Abschlusses oder das einzelne Lesen einer Kontakt-Rolle zwischen einem Abschluss und einem Kontakt.
Für den Aufruf erwartet die Verbindung die Parameter in Feldnotation.
Dies kann als Prozessfilter (z.B. auch kombiniert in Abläufen), als Adhoc-Ausführung oder in einer Übereinstimmungsregel erfolgen.

	deal_id|:|1234|;| liest alle Kontaktrollen des Abschlusses mit der ID 1234

	deal_id|:1234|;|contact_id|:|5678|;| liest die Kontaktrolle zwischen dem Abschluss mit der ID 1234 und dem Kontakt mit der ID 5678

Für das Anlegen oder Aktualisieren einer Kontaktrolle müssen die ID des Abschlusses (deal_id) und die ID des Kontaktes (contact_id) zugeordnet werden.
Im Fall einer Aktualsierung kann dies bereits durch eine Datenabbildung oder eine Übereinstimmungssuche erfolgt sein.
Wenn die Übereinstimmungssuche allerdings kein Ergebnis liefert, müssen die ID-Werte als Felder zugeordnet sein.
Die Angabe der Rolle ist optional und muss mit dem Rollennamen (contact_role_name) erfolgen.

Das Löschen von Kontakt-Rollen kann mit dem Universal-Löschprozess oder einem Abfrageprozess erfolgen.
Diese arbeiten auf der Basis einer Datenabbildung oder einer Übereinstimmungssuche und erhalten darüber die ID-Werte für das gezielte Löschen der Kontakt-Rolle.