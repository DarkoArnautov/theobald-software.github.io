---
ref: ec-linq-to-sap-03
layout: page
title: Table Access Restrictions
description: Table Access Restrictions
product: erpconnect
parent: linq-to-sap
permalink: /:collection/:path
weight: 3
lang: en_GB
old_url: /ERPConnect-EN/default.aspx?pageid=linq-to-sap-table-access-restrictions
---

As shown in the previous section, tables can be called without having to do any installations in the SAP system. Unfortunately though, the same restrictions apply here as with the traditional ReadTable class (see chapter [Reading SAP Tables Directly with ReadTable](../special-classes/reading-sap-tables-directly-with-readtable)).

To deal with this problem, it is possible to install a Z-module in the SAP system, see chapter [Installing the Z-function module](../sap-customizing/install-report-custom-function-module).

As long as this module is available in the system, you can activate it by entering the name of the LINQ table dialog (if necessary, the module's name can be changed according to your naming requirements).

![LINQToERP-Tables-004](/img/content/LINQToERP-Tables-004.png){:class="img-responsive" width="800px" }

Not all LINQ expressions are technically feasible or make sense in LINQ to SAP. Apart from classical expressions like the operators <, > and =, LINQ to SAP offers all character-like functions like Equals (=), Contains (LIKE "%..%"), StartsWith (LIKE "%...") and EndsWith (LIKE "…%"). There is also an extension function called InList. But this is only active when ERPConnect.Linq has been specified in the "using" section (or, if applicable, in the imports in VB).

<details>
<summary>Click to open C# example.</summary>
{% highlight csharp %}
using ERPConnect.Linq; 
  
[…] 
  
var MyTexts = from t in sc.MAKTList 
         where t.MATNR.StartsWith("100") 
         && t.SPRAS.InList("D","E") 
         select t;
{% endhighlight %}
</details>
