---
title: How to debug Azure Logic Apps
date: "2022-06-19"
template: "post"
draft: false
slug: "How-to-debug-Azure-Logic-Apps"
category: "Azure"
tags:
  - "Azure"
  - "Logic Apps"
  - "Azure Logic Apps"
description: "One of the most frequent problems we face during troubleshooting logic app is,  identifying the run associated to a logic app. It is a bit easy when we have few runs in a day. When a problem is reported, we could ask for time when it occurred and use the time stamp to find the run, through run history."
---

<iframe width="640" height="315" src="https://www.youtube.com/embed/1AxS2uUgM-Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

One of the most frequent problems we face during troubleshooting logic app is,  identifying the run associated to a logic app.

It is a bit easy when we have few runs in a day. When a problem is reported, we could ask for time when it occurred and use the time stamp to find the run, through run history. But when have 

1. some thousands of runs per day?
2. If you know the time frame, you can filter for failed runs. But all of them shows success even though there is something wrong (This because of how you coded your logic app)

In this blog, we will see 

1. how to trouble shoot a logic app errors.
2. What is the best practise we need to follow during development so we can trouble shoot the issues super quick in Production environment.

### Before you begin

You need to have a log analytic work space configured for your logic apps. Without this, debugging in production can be a nightmare. 

Long story shot - When log analytics configured properly, It will will ingest log data into workspace repository. We can then go to Log Analytics workspace, query the logs to see logic app execution details. 

### Tracked Properties Makes debugging easy

You can track input or output of an action in logic app using tracked properties. 

When Tracked Properties are configured in an logic app, while execution this data will be ingested to log analytics and it will be associated with run instance.

This is very useful for debugging purposes.

For example, if you have HTTP trigger logic app which receives numerous requests from different clients, it is hard to track back which run instance associated to which client. If we log Client ID using tracked properties, we can simply query in log analytics using Client ID, and find the run ID. We can this run ID to find out the running instances.

### Configure Log Analytic workspace for logic app

Got Azure portal and open the logic app. Go to *Diagnostic settings.* Configure log analytic workspace so it can ingest logs into it.

![Azure Portal](/media/1.png)

### Configure tracked properties

In Azure portal, open the logic app in edit mode. Open settings of an which for which you are looking to configure tracked properties. This action holds the data identifier inform of input or output which you can use to identify the logic app run. 

You can find *Traced Properties* section in the settings. Now enter *Key* and *Value*

Key: Give a name to tracked property. 

Value: Read desired input/output value of action - ex:   **"@{outputs('Execute_JavaScript_Code')?['body']['id']}”**

 

![Azure Portal](/media/2.png)

Now when this logic app runs, it will start logging tracked properties. This tracked property will be added a new column in the AzureDiagnositic table.

Go to Log Analytic Workspace logs, search with tracked property.

```sql
AzureDiagnostics
| where trackedProperties_ClientId_s contains "456"
```

![Azure Portal](/media/3.png)

When a problem is reported, get the Identifier, go to log analytic work space, search with identifier, get the run id associated with it. Go to logic app run history and search with run id.