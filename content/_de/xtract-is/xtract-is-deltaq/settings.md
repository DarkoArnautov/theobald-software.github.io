---
ref: xi-q-delta-09
layout: page
title: Settings
description: Settings
product: xtract-is
parent: xtract-is-deltaq
permalink: /:collection/:path
weight: 9
lang: de_DE
old_url: /Xtract-IS-DE/default.aspx?pageid=deltaq-settings
---

Über den Settings-Link im Editor öffnet sich das Einstellungsfenster.

![XIS_DeltaQ_Settings](/img/content/XIS_DeltaQ_Settings.jpg){:class="img-responsive"}


**Automatic String Conversion**<br>
bedeutet, dass die Datenquelle alle Strings nach NVarChar konvertiert, wenn SAP ein Unicode-System ist, und nach VarChar, wenn SAP kein Unicode-System ist.

**Convert Strings to VarChar**<br>
bedeutet, dass die Datenquelle alle Strings nach VarChar konvertiert.

**Convert Strings to NVarChar**<br>
bedeutet, dass die Datenquelle alle Strings nach NVarChar konvertiert.

**Transfer Mode**<br>
Die Rohdatenpakete können aus SAP mittels *tRFC*-Calls oder Daten-*IDocs* versendet werden. <br>
In der Regel ist *tRFC* als Default-Wert optimal. Sollte es aber nötig sein, um z.B. die Rohdatenpakete zu Debugging-Zwecken anschauen zu können, kann der Datentransfer auf Idoc umgestellt werden. Dann lassen sich die Datenpakete in der Transaktion WE02 (Idoc-Monitoring) einsehen. 

**Language**<br>
Legt die Sprache fest, falls eine Hierarchie extrahiert wird.

**Hierarchy Name**<br>
Legt den Hierarchienamen fest.

**Hierarchy Class**<br>
Legt die Hierarchieklasse fest.

**Update Mode Variable**<br>
Setzen Sie den Wert für **Update Mode** auf **V - SSIS Variable** und definieren Sie hier den Namen der SSIS-Variable für den Update-Mode. Die Variable kann dann folgende Werte verarbeiten: A, F, C, D, S, I und R, wie es in der Werteliste des Update Mode steht.

**Request ID**<br>
Diese Angabe ist optional. 
Wenn hier ein Wert (z.B. XtractDatasource) eingetragen wird, wird dieser im Namen des SAP-Jobs (Transaktion SM37) als Suffix verwendet (z.B. BIXtractDatasource). <br>
Andernfalls wird eine Kombination aus Prozess ID und Zeitstempel verwendet ( z.B. REQU_pppppppp_yyyyMMddHHmmss). Dabei ist die Prozess ID die ID des Windows Prozesses, unter dem der XtractKernel.DeltaQServerPool.exe läuft.

**Debug Details**<br>
Schreibt detailliertere Informationen in das SSIS Log.

**Check IDoc Request State**<br>
Definiert, ob der Request-Status der versendeten IDocs geprüft wird. Die IDoc-Nummer wird ins Log geschrieben und der IDoc-Status wird auf Erfolg geprüft.<br>
Diese Einstellung kann bei der Analyse eines Fehlverhaltens hilfreich sein. Insbesondere wenn Extraktionen wiederholt fehlschlagen oder ohne weitere Informationen keine Jobs in der SAP-Transaktion SM37 generieren.<br>
Standardmäßig ist diese Option nicht gesetzt. Damit findet die Überprüfung nicht statt, was die Performance erhöht. 

**Resend errors (deprecated)**<br>
In früheren Versionen der DeltaQ hieß diese Option *Don't resend tRFC errors* automatically und war in der Default-Einstellung aktiviert. Mittlerweile ist die Einstellung im Default deaktiviert, da diese Einstellung nicht mehr notwendig sein sollte. Die Einstellung triggert in einem kurzen zeitlichen Intervall auf dem SAP-System einen Wiederversand von tRFC-Paketen und IDocs, wenn diese aufgrund eines tRFC-Verbindungsfehlers nicht an die Xtract RFC-Destination übermittelt werden konnten (Einträge in der Transaktion SM58). Anstelle dieser Option empfehlen wir, den Wiederversand über die tRFC-Optionen der RFC-Destination in der Transaktion SM59 auf SAP-Seite zu setzen, siehe Kapitel [Customizing für DeltaQ, Schritt 4](../sap-customizing/customizing-fuer-deltaq).

**Automatic Synchronisation**<br>
Je nach Systemlandschaft kann es vorkommen, dass Entwicklungen ausschließlich in einem Testsystem vorgenommen werden. Wenn SSIS-Pakete dann in der produktiven Umgebung eingesetzt werden, muss die DataSource dort aktiviert werden. Um manuelles Eingreifen im Produktivsystem zu vermeiden, kann diese Option gesetzt werden. Dann wird die Aktivierung automatisch erledigt und der Timestamp der DataSource so angepasst, dass er konsistent mit dem SAP-System übereinstimmt.<br>
Wenn was in der DataSource im SAP-System geändert wird, z.B. ein Feldname, Datentyp, Datentyplänge oder die Datentransferstruktur, müssen Sie in der DeltaQ-Komponente die DataSource manuell aktivieren, auch wenn diese Option gesetzt ist, sonst wird die Extraktion fehlschlagen. Dieses Verhalten ist von SAP vorgegeben und wird in der [SAP help](https://help.sap.com/viewer/ccc9cdbdc6cd4eceaf1e5485b1bf8f4b/7.4.19/de-DE/4a12eaff76df1b42e10000000a42189c.html) dokumentiert.

**Add Serialization Info to Output**<br>
Fügt der Ausgabe zwei zusätzliche Spalten hinzu: *DataPackageID* für die Paketnummer und *RowCounter* für den Datensatz innerhalb des Paketes.<br>
Gemeinsam mit der Spalte *RequestID* haben die Daten einen zusammengesetzten Schlüssel der von SAP gelieferten Datensätze.<br>
Neuere Datensätze haben eine höhere PackageID.
Im selben Paket haben neuere Daten einen höheren RowCounter-Wert. 

**Automatic Data Type conversion**<br>
Konvertiert SAP-Datentypen (z.B. Datum) zu einem passenden SQL-Datentyp.

**Value for invalid date [YYYYMMDD]**<br>
Für den Fall, dass ein SAP-Datum nicht in ein gültiges SQL-Datum konvertiert werden kann, muss ein Standard-Datumswert in die Textbox eingetragen werden. Jeder ungültige Wert wird dann in das eingegebene Datum konvertiert.<br>
Das SAP-Datum '00000000' wird abweichend von dem eingegebenen Datum immer nach NULL konvertiert.

**Request Maintenance**<br>
Zum Anzeigen bzw. Löschen von vorigen Init-Anfragen (Einträge in RSA7).

- **Delete Request**<br>
    Löscht die Init-Abfragen (Einträge in RSA7).

- **Allow BW requests deletion**<br>
    Erlaubt die Löschung der Init-Abfragen für die Export DataSources in BW. 

**Generate Documentation**<br>
Generiert eine Dokumentation über die Datasource und deren Felder im Excel-Format.