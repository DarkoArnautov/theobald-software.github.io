**Achtung**: Die Schritte des DeltaQ-Customizings außer Schritt 2 sind Mandantenabhängig.  

Um die DeltaQ-Komponente nutzen zu können, sind einige Customizing-Einstellungen im SAP vorzunehmen, die im Folgenden Schritt für Schritt beschrieben sind.

**Schritt 1**

Legen Sie in der Transaktion SM59 eine neue RFC-Destination vom Typ R/3 an (z.B. mit Namen XTRACT01, Connection Type 3). Sie brauchen keinen Verbindungstest durchzuführen. Die Destination muss nur vorhanden sein.

**Schritt 2 (Optional)**

Der 2. Schritt, also die Anlage der logischen Destination, ist optional. 
Im Schritt 3 wird beim Ausführen des FuBas RSAP_BIW_CONNECT_40 automatisch die logische Destination angelegt. 

Legen Sie mit Hilfe der Transaktion SALE ein logisches System an mit demselben Namen wie die Destination aus Schritt 1.

![DeltaQ-Customizing-01](/img/content/DeltaQ-Customizing-01.png){:class="img-responsive"}

Der 2. Schritt, also die Anlage der logischen Destination, ist optional. 
Im Schritt 3 wird beim Ausführen des FuBas RSAP_BIW_CONNECT_40 automatisch die logische Destination angelegt. 

**Schritt 3**

Gehen Sie in die Transaktion SE37 und rufen Sie den Baustein RSAP_BIW_CONNECT_40 in der Testumgebung auf. Füllen Sie die Import-Parameter wie im Screenshot angegeben. <br>
Der Parameter I_SLOGSYS ist der logische Name des Quellsystems. Falls Sie diesen nicht wissen, schauen Sie in die Tabelle T000 für den jeweiligen Mandanten (Feld LOGSYS). <br>
Das Feld I_SAPRL wird automatisch vom SAP-System gesetzt.
Mit *F8* starten Sie den Baustein.


**Achtung**: Dieser Schritt setzt voraus, dass das SAP-System in bestimmten Bereichen (2 bis 3) veränderbar ist. , für weitere Infos siehe unseren folgenden Knowledge base Artikel.

**Achtung**: Die Werte für die Felder I_BASIC_IDOC und I_TSPREFIX müssen eindeutig für alle RFC-Destinationen sein. 
Wenn Sie ZXTIDOC und XT schon für XTRACT01 verwendet haben, können Sie für XTRACT02 z.B. ZX2IDOC und X2 verwenden.

![DeltaQ-Customizing-02](/img/content/DeltaQ-Customizing-02.png){:class="img-responsive"}

![DeltaQ-Customizing-03](/img/content/DeltaQ-Customizing-03.png){:class="img-responsive"}

**Schritt 4**

Gehen Sie wieder in die Transaktion SM59 und löschen Sie die Destination, die Sie im Schritt 1 angelegt haben (*Detailanzeige -> Menü Löschen*). Legen Sie dann eine neue Destination an mit exakt demselben Namen, diesmal aber vom Connection *Typ* T=TCP/IP. Der Aktivierungstyp muss *registrierbares Serverprogramm* sein; als *Program ID* tragen Sie den Namen der Destination ein.

**Gateway Host** ist der Name (oder IP-Adresse) Ihres SAP-Systems (ptmalg ist der Name des in dieser Anleitung verwendeten SAP-Systems). <br>
**Gateway Service** ist in der Regel in der Form sapgwNN, wobei NN die ID ihres SAP-Systems ist, eine zweistellige Zahl zwischen 00 und 00.

![DeltaQ-Customizing-04](/img/content/DeltaQ-Customizing-04.png){:class="img-responsive"}

Optional, aber empfohlen: Ab Xtract IS Version 2.15.0 wurde der Wiederversand von fehlgeschlagenen tRFC-Calls  (siehe DeltaQ Settings) als 'deprecated' gekennzeichnet. Auch wenn diese Funktionalität weiterhin unterstützt wird, wird die Nutzung von uns nicht mehr empfohlen. Bei Neuanlage einer DeltaQ Extraktion ist sie daher standardmäßig deaktiviert (in früheren Versionen von Xtract IS war sie standardmäßig aktiviert). Anstattdessen empfehlen wir eine Anpassung der tRFC-Optionen der gerade erstellten RFC Destination. Rufen Sie in der Transaktion SM59  *Bearbeiten - TRFC-Optionen* auf, und setzen Sie den Parameter *Verbindungsversuche bis zur Aufgabe* auf 30 und *Pause zw. 2 Versuchen [min]* auf 2. 


**Schritt 5**

Führen Sie den Baustein RSAS_RBWBCRL_STORE wie unten gezeigt aus. Er dient dazu, das neue Zielsystem zu aktivieren.

![DeltaQ-Customizing-05](/img/content/DeltaQ-Customizing-05.png){:class="img-responsive"}

**Schritt 6**

In unserer [Knowledge Base](https://my.theobald-software.com/index.php?/Knowledgebase/Article/View/100/0/registering-rfc-server-in-sap-releases-above-kernel-release-720) finden Sie die Anleitung zu der Registrierung des RFC Servers in SAP. 

**Achtung**: Dieser Schritt gilt ab der SAP Kernel-Version 720.

**Schritt 7**

Ändern Sie in der Transaktion SMQS den Parameter Max.Verb. auf den Wert 10. Erhöhen Sie diesen Wert, wenn Sie mehrere DeltaQ-Extraktionen auf derselben RFC Destination parallel ausführen.

Bei Fehlern bitte im [DeltaQ Troubleshooting Guide](https://my.theobald-software.com/index.php?/Knowledgebase/Article/View/107/4/deltaq-troubleshooting-guide) (Englisch) nachschlagen.