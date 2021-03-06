---
ref: xu-microsoft-sql-server-05
layout: page
title: Daten mergen
description: Daten mergen
product: xtract-universal
parent: microsoft-sql-server
permalink: /:collection/:path
weight: 5
lang: de_DE
old_url: /Xtract-Universal-DE/default.aspx?pageid=sql-server-daten-mergen
---

In diesem Beispiel wollen wir bestehende Datensätze aktualisieren.<br>
Es ist wichtig, dass ein entsprechender Index anlegt ist, um den Merge-Befehl schnell auszuführen. Ohne einen Index würde die Ausführung des Merge-Befehls abhängig von der Datenmenge sehr lange dauern. 

Schauen wir uns den Datensatz für das Werk 1000 an, das Feld NAME2 hat den Wert NULL.

![MSSql-Select-Before-Merge](/img/content/MSSql-Select-Before-Merge.jpg){:class="img-responsive"}

Überschreiben wir nun das Feld NAME2 mit dem Wert 'Hamburg'.

![MSSql-Update-Merge-Example-Data](/img/content/MSSql-Update-Merge-Example-Data.jpg){:class="img-responsive"}

Nun ändern wir die extraktionsspezifischen Einstellungen und setzen Preparation auf *Create if Not Exists* und Row Processing auf *Merge*, um die vorhandene Tabelle zu verwenden. Alternativ können Sie Preparation auf *None* setzen, wenn die Tabelle schon vorhanden ist.

![MSSql-Extraction-Specific-Settings-Merge-T001w](/img/content/MSSql-Extraction-Specific-Settings-Merge-T001w.jpg){:class="img-responsive"}

Der Merge-Befehl sorgt dafür, dass neue Datensätze eingefügt bzw. bestehende aktualisiert werden.<br> 
Bei bestehenden Datensätzen wird ein Update ausgeführt, sonst ein Insert.

![MSSql-Custom-SQL-Merge](/img/content/MSSql-Custom-SQL-Merge.jpg){:class="img-responsive"}

Welche Felder aktualisiert werden, kann man dem SQL-Statement entnehmen. <br>
Hier kann man das SQL-Statement bei Bedarf ändern, um z.B. bestimmte Spalten von der Aktualisierung auszuschließen.<br>
Felder, welche nicht im SQL-Statement auftauchen, sind von Änderungen nicht betroffen.

Bei der Ausführung wurde das Feld *NAME2* mit dem Wert aus SAP aktualisiert.

![MSSql-Select-After-Merge](/img/content/MSSql-Select-After-Merge.jpg){:class="img-responsive"}
