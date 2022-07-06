---
title: What is Azure Log Analytics Workspace | How to create and configure Azure Log Analytics Workspace
date: "2022-07-06"
template: "post"
draft: false
slug: "What-is-Azure-Log-Analytics-Workspace"
category: "Azure"
tags:
  - "Azure"
  - "Logic Apps"
  - "Azure Logic Apps"
description: "Understanding how the logs and logging works in Azure cloud environment is very critical for Troubleshooting any issues. We need to configure Azure resources properly so they can emit the logs during execution. "
---

<iframe width="640" height="315" src="https://www.youtube.com/embed/1qNgFLTdOVc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Understanding how the logs and logging works in Azure cloud environment is very critical for Troubleshooting any issues. We need to configure Azure resources properly so they can emit the logs during execution. 

This Blog will help you understand the basics of Azure Log Analytics Workspace and how to configure a logic app to use Azure Log Analytics workspace, so it can emits the logs during execution.

### What is Azure Log Analytics Workspace?

Log Analytic workspace is an environment for Azure Monitor to log data. It is like a repository, a repository for all your logs. 

Based on your requirement, you can use a single workspace for all your data collection, or you may create multiple workspaces. Each workspace has its own data repository and configurations. Each workspace contains multiple tables and each table is defined by a unique set of columns

![Azure Log Analytics Workspace](/media/1.png)

On the left hand side you can see the data sources. These are nothing but Azure services which will be ingesting the data during execution. For example, a logic app. While execution, it can ingest the logs into log analytic workspace. We will see this in demo

On the right hand side, we have log query - These are queries we write to retrieve the log data.

The log data can be retrieved using log queries and fed to other services for example dash board an log alerts. We can identify the service behaviour using log data and trigger alerts.

Different Azure resources emit the log data into different tables of  log analytics workspace. Below diagram gives you a glimpse of it.

![Azure Log Analytics Workspace](/media/2.png)

For a step by step demo of how to create and configure Azure Log Analytic Workspace, watch the <a href="https://www.youtube.com/embed/1qNgFLTdOVc" target="_blank">Video</a>  
