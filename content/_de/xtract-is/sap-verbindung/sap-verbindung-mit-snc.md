---
ref: xi-sap-connection-02
layout: page
title: SAP-Verbindung mit SNC
description: SAP-Verbindung mit SNC
product: xtract-is
parent: sap-verbindung
permalink: /:collection/:path
weight: 2
lang: de_DE
old_url: /Xtract-IS-DE/default.aspx?pageid=sap-verbindung-mit-snc
---

Sie können auch SNC (Secure Network Communication) für die Verbindung mit dem SAP-System verwenden.<br>
Dazu klicken Sie im SAP-Verbindungsmanager auf **Additions**. Im Abschnitt SNC setzen Sie das Häckchen bei **SNC enabled** und füllen Sie die entsprechenden Felder.

![SNC](/img/content/SNC.jpg){:class="img-responsive"}

Mit der Eigenschaft **Quality Of Protection** lässt sich die bevorzugte Sicherheitsstufe setzen. Genaueres dazu findet sich hier: [http://help.sap.com/saphelp_nw70ehp1/helpdata/en/e6/56f466e99a11d1a5b00000e835363f/content.htm](http://help.sap.com/saphelp_nw70ehp1/helpdata/en/e6/56f466e99a11d1a5b00000e835363f/content.htm)

Weitere Informationen zur SSO-Konfiguration auf SAP-Seite finden Sie unter: <br>
[http://help.sap.com/saphelp_nw73/helpdata/en/44/0e2e0cc7330d19e10000000a114a6b/frameset.htm](http://help.sap.com/saphelp_nw73/helpdata/en/44/0e2e0cc7330d19e10000000a114a6b/frameset.htm)


**Die DLLs herunterladen**

Sie müssen die relevanten DDLs von der SAP-Seite herunterladen. Diese DLLs sind für 32-Bit und 64-Bit Plattformen unterschiedlich und werden mit dem SAP-Hinweis 352295 zur Verfügung gestellt:<br> 
[https://websmp230.sap-ag.de/sap/support/notes/352295](https://websmp230.sap-ag.de/sap/support/notes/352295) 

Die DLLs heißen: 

Für 32-Bit: gsskrb5.dll<br>
Für 64-Bit x86: gx64krb5.dll<br>

Der folgende Knowledge Base Artikel beschreibt, wie Sie Ihr SAP-System mit SSO/SNC einrichten:<br>
[http://my.theobald-software.com/index.php?/Knowledgebase/Article/View/87/3/snc-connection-with-sso](http://my.theobald-software.com/index.php?/Knowledgebase/Article/View/87/3/snc-connection-with-sso) 