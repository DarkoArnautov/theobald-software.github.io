---
ref: xu-datasource-deltaq-08
layout: page
title: Extraktionseinstellungen
description: Extraktionseinstellungen
product: xtract-universal
parent: datasource-deltaq
permalink: /:collection/:path
weight: 8
lang: de_DE
old_url: /Xtract-Universal-DE/default.aspx?pageid=deltaq-extraktionseinstellungen
---

Über den *Extraction Settings*-Link im Editor öffnet sich das Einstellungsfenster.

![XU_DeltaQ_Settings](/img/content/XU_DeltaQ_Settings.jpg){:class="img-responsive"}

**Transfer Mode**<br>
Die Rohdatenpakete können aus SAP über tRFC-Calls oder Daten-IDocs versendet werden. <br>
In der Regel ist tRFC als Default-Wert optimal. <br>Sollte es aber nötig sein, um z.B. die Rohdatenpakete zu Debugging-Zwecken anschauen zu können, kann der Datentransfer auf Idoc umgestellt werden. Dann lassen sich die Datenpakete in der Transaktion WE02 (Idoc-Monitoring) einsehen.

**Check IDoc Request State**<br>
Definiert, ob der Request-Status der versendeten IDocs geprüft wird. Die IDoc-Nummer wird ins Log geschrieben und der IDoc-Status wird auf Erfolg geprüft.<br>
Diese Einstellung kann bei der Analyse eines Fehlverhaltens hilfreich sein. Insbesondere wenn Extraktionen wiederholt fehlschlagen oder ohne weitere Informationen keine Jobs in der SAP-Transaktion SM37 generieren.<br>
Standardmäßig ist diese Option nicht gesetzt. Damit findet die Überprüfung nicht statt, was die Performance erhöht. 

**Resend errors (deprecated)**<br>
In früheren Versionen der DeltaQ hieß diese Option Don't resend tRFC errors automatically und war in der Default-Einstellung aktiviert. Mittlerweile ist die Einstellung im Default deaktiviert, da diese Einstellung nicht mehr notwendig sein sollte. Die Einstellung triggert in einem kurzen zeitlichen Intervall auf dem SAP-System einen Wiederversand von tRFC-Paketen und IDocs, wenn diese aufgrund eines tRFC-Verbindungsfehlers nicht an die Xtract RFC-Destination übermittelt werden konnten (Einträge in der Transaktion SM58). Anstelle dieser Option empfehlen wir, den Wiederversand über die tRFC-Optionen der RFC-Destination in der Transaktion SM59 auf SAP-Seite zu setzen, siehe Kapitel [Customizing für DeltaQ, Schritt 4](../sap-customizing/customizing-fuer-deltaq).

**Automatic Synchronisation**<br>
Je nach Systemlandschaft kann es vorkommen, dass Entwicklungen ausschließlich in einem Testsystem vorgenommen werden. Wenn Extraktionen dann in der produktiven Umgebung eingesetzt werden, muss die DataSource dort aktiviert werden. Um manuelles Eingreifen im Produktivsystem zu vermeiden, kann diese Option gesetzt werden. Dann wird die Aktivierung automatisch erledigt und der Timestamp der DataSource so angepasst, dass er konsistent mit dem SAP-System übereinstimmt.<br>
Wenn was in der DataSource im SAP-System geändert wird, z.B. ein Feldname, Datentyp, Datentyplänge oder die Datentransferstruktur, müssen Sie in der DeltaQ-Komponente die DataSource manuell aktivieren, auch wenn diese Option gesetzt ist, sonst wird die Extraktion fehlschlagen. Dieses Verhalten ist von SAP vorgegeben und wird in der [SAP help](https://help.sap.com/viewer/ccc9cdbdc6cd4eceaf1e5485b1bf8f4b/7.4.19/de-DE/4a12eaff76df1b42e10000000a42189c.html) dokumentiert.

**Add Serialization Info to Output**<br>
Fügt der Ausgabe zwei zusätzliche Spalten hinzu: DataPackageID für die Paketnummer und RowCounter für den Datensatz innerhalb des Paketes.<br>
Gemeinsam mit der Spalte RequestID haben die Daten einen zusammengesetzten Schlüssel der von SAP gelieferten Datensätze.<br>
Neuere Datensätze haben eine höhere PackageID.
Im selben Paket haben neuere Daten einen höheren RowCounter-Wert. 


**Accept Gaps in DataPackage Id**<br>
Die DeltaQ-Komponente macht am Ende jede Extraktion einen Konsistenzcheck. Nur wenn alle Pakete korrekt angekommen sind, gilt die Extraktion als konsistent. Für den Fall, dass der Kunde im User-Exit einer OLTP-Source nun aber eine Filterfunktion eingebaut hat, die dafür sorgt, dass bestimmte Datenpakete nicht versendet werden, muss der Konsistenz-Check etwas entschärft werden. Sonst würde der Kundenfilter als Inkonsistenz gewertet. Wenn diese Option also aktiviert ist, werden von der DeltaQ Lücken in der Paketnummerierung nicht als Inkonsistenz gewertet sondern als bewusst zurückgehaltene Daten. Die Option sollte man nur dann verwenden, wenn wirklich eine entsprechende Filterfunktion im User-Exit vorliegt. Das Verhalten lässt sich häufig bei 0FI- oder 0CO-DataSources beobachten.

**Timeout (sec)**<br>
Der Timeout definiert die Zeitspanne, wie lange die Komponente maximal auf fehlende IDocs oder Datenpakete vom SAP System warten soll (in Sekunden), nachdem der Extraktionsjob auf SAP-Seite beendet wurde. Der Default-Wert sind 300 Sekunden.

**Request Maintenance**<br>
Zum Anzeigen bzw. Löschen von vorigen Init-Anfragen (Einträge in RSA7).

- **Delete Request**
    Löscht die Init-Abfragen (Einträge in RSA7).

- **Allow BW requests deletion**
    Erlaubt die Löschung der Init-Abfragen für die Export DataSources in BW.



**Hierarchy Settings**

Falls Sie eine Hierachie-Datasource extrahieren, finden Sie im Reiter Hierarchy die entsprechenden Einstellungen.

![Deltaq-Preferences-Hierarchy](/img/content/Deltaq-Preferences-Hierarchy.jpg){:class="img-responsive"}

**Language**<br>
Legt die Sprache fest, falls eine Hierarchie extrahiert wird.

**Hierarchy Name**<br>
Legt den Hierarchienamen fest.

**Hierarchy Class**<br>
Legt die Hierarchieklasse fest.


**Representation**

- ParentChild: Die Hierarchie hat das SAP Parent-Child Format.

![Deltaq-Hierarchies-Parent-Child](/img/content/Deltaq-Hierarchies-Parent-Child.png){:class="img-responsive"}

- Natural: Die Parent-Child Beziehung wird in eine reguläre Hierarchie umgewandelt.

**Level Count**<br>
Legt die maximale Anzahl der Ebenen fest, falls die Representation Natural gewählt ist. Im nächsten Screenshot sehen Sie die obige Hierarchie in der Repräsentation Natural mit 5 Ebenen.

![Deltaq-Hierarchies-Parent-Child-Natural](/img/content/Deltaq-Hierarchies-Parent-Child-Natural.png){:class="img-responsive"}

**Fill empty levels**<br>
Falls die Representation Natural gewählt ist, wird das unterste Element in der Hierarchie bis in die letzte Ebene kopiert. Im nächsten Screenshot sehen Sie die obige Hierarchie in der Repräsentation Natural mit 5 Ebenen und der Option Repeat Leaves.

![Deltaq-Hierarchies-Parent-Child-Repeat](/img/content/Deltaq-Hierarchies-Parent-Child-Repeat.png){:class="img-responsive"}

**Description texts for levels** <br>
bedeutet, dass für jedes Level-Feld LevelN das Feld LevelTextN ausgegeben wird, welches den Stammdatentext in der jeweiligen Anmeldesprache enthält.

**Leaves only**<br>
liefert nur für die Blätter jeweils einen eigenen Datensatz. 