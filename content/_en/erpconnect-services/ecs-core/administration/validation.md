---
layout: page
title: Validation
description: Validation
product: erpconnect-services
parent: administration
permalink: /:collection/:path
weight: 5
lang: en_GB
old_url: /ERPConnect-Services-EN/default.aspx?pageid=validation1
---

To test and insure that the configured components work correctly you can use the [tEcs-Library]() (recommended), alternatively use the instructions and snippets prepared for you in the section ERPConnect Services Runtime>Webservices>REST without tEcs  "Table with REST" or another example.

Use this [JSBin snippet]() to easily test your ECSCore and SAP Connection.

```
tEcs.testSapConnection({
    connection: {
        ecs: {
            core: true,
            coreApiKey: "E380FB721AFA4EB2A86CC624E4B6890C",
            //instance: "ec4",
            url: "https://ecscore.mydomain.com"
        }
    }
});
```

Another option is to build a query with browser extensions: [POSTMAN]() (Chrome) or [RESTClient]() (Firefox).

Here you must notice how the Authorization Header is set:

**Authorization** 		APIKEY 

Base64 encoded key can be copied directly from the Management Site, you need to click on the generated API Key and select copy base64 value.