---
title: What is Azure API Management | Publishing your first API with APIM
date: "2022-07-04"
template: "post"
draft: false
slug: "What-Is-Azure-API-Management"
category: "Azure"
tags:
  - "Azure"
  - "API Management"
description: "Azure API Management is a reliable, secure and scalable way to publish, consume and manage all your API’s. It provides a central interface and essential tools to create, provision and manage all you APIs."
---


<iframe width="640" height="315" src="https://www.youtube.com/embed/xZsk3rAqjrg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


Azure API Management is a reliable, secure and scalable way to publish, consume and manage all your API’s. It provides a central interface and essential tools to create, provision and manage all you APIs. 

### **API Management components**

Azure API Management is made up of an API *gateway*, a *management plane*, and a *developer portal*. These components are Azure-hosted and fully managed by default as part of APIM Management.

![Azure Portal](/media/1.png)

## API Gateway

API Gateway acts as a front gate  to the backend services. The client requests first reach API Gateway which then routes them to backend services. 

The API gateway:

- Verifies API keys, JWT tokens, certificates, and other credentials
- Enforces usage quotas and rate limits.
- Emits logs, metrics, and traces for monitoring, reporting, and troubleshooting

## Management Plane

Management Plane provides full access to the API Management service capabilities. This is nothing but, APIM resource interface in Azure portal. You can also use, Azure PowerShell, Azure CLI to interact with it. 

Use the management plane to:

- Provision and configure API Management service settings
- Define or import API schemas
- Package APIs into products
- Set up [policies](https://docs.microsoft.com/en-us/azure/api-management/api-management-key-concepts#policies) like quotas or transformations on the APIs
- Get insights from analytics
- Manage users

### Developer Portal

This an automatically generated, fully customizable web portal for the documentation of your APIs.

Look and feel of the developer portal can be customized by adding custom content, customizing styles, and adding branding. 

Consumers use the open-source developer portal to discover the APIs, and learn how to consume them in applications. 

Using the developer portal, developers can:

- Read API documentation
- Call an API via the interactive console
- Create an account and subscribe to get API keys
- Access analytics on their own usage
- Download API definitions
- Manage API keys


For the demo, please check the <a href="https://www.youtube.com/embed/xZsk3rAqjrg" target="_blank">Video</a>  