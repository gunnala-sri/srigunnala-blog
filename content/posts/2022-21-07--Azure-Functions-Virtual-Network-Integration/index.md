---
title: Azure Functions VNET integration | Private Endpoints for Azure Functions
date: "2022-07-21"
template: "post"
draft: false
slug: "Azure-Functions-Virtual-Network-Integration"
category: "Azure"
tags:
  - "Azure"
  - "Azure Function Apps"
  - "Azure Virtual Network"
description: "Azure Function VNET integration is supported by Premium Azure functions, App Service Plan minimum Basic tier and of course App Service Environment. When we create an azure function without any VNET integration, it will have a public IP address and it will be exposed to the internet. This Blog will explain how we can secure the Azure function with VNET integration? How we can create a private endpoint to secure incoming traffic? How can we restrict outbound traffic from the Azure function to VNET?"
---

<iframe width="640" height="315" src="https://youtu.be/hvHloEGqI-A" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

We can host the function app mainly in two ways

1. In Multitenant infrastructure
    1. Consumption Plan — scales dynamically in response to load and offers minimal network isolation options.
    2. Premium Plan — scales dynamically and offers more comprehensive network isolation.
    3. App Service Plan — operates at a fixed scale and offers network isolation similar to the Premium plan
2. In App Service Environment — This method deploys your function into your virtual network and offers full network control and isolation.

### VNET Integration options

![Azure Functions Networking Options](/media/networking-options.png)

Azure Function VNET integration is supported by Premium Azure functions, App Service Plan minimum Basic tier and of course App Service Environment. When we create an azure function without any VNET integration, it will have a public IP address and it will be exposed to the internet. 

### This Blog will explain

1. How we can secure the Azure function with VNET integration?
2. How we can create a private endpoint to secure incoming traffic?
3. How can we restrict outbound traffic from the Azure function to VNET?

I will demonstrate this using App Service Plan Basic tier azure function with step by step process through the Azure portal.

# Why do we need Azure function VNET Integration?

1. Access to VNET-based resources
2. Lock down your function app behind a VNET (no public IP Address at the source or destination)
3. Access to Azure PaaS services(for example, Azure Storage and SQL Database) over a private endpoint.
4. Access services running on-premises over ExpressRoute private peering, VPN tunnels and peered virtual networks.

# Inbound Traffic

Inbound traffic is controlled using Accessing Restrictions and Private endpoints.

### Access Restrictions

You can use access restrictions to define a priority-ordered list of IP addresses that are allowed or denied access to your app. When there are one or more entries, an implicit "deny all" exists at the end of the list. IP restrictions work with all function-hosting options. 

### What is a Private Link?

Azure PaaS services are shared services and they are available over public IP addresses. Private Link enables us to connect to Azure PaaS services(storage, SQL, logic apps, service bus, event grids etc..) without opening to the Internet. A private link will give a private IP address to the Azure PaaS service and traffic will go through the Microsoft backbone network. So, No internet exposure.

# Outbound Traffic

Outbound IP restrictions are available in a Premium plan, App Service Plan, or App Service Environment. You can configure outbound restrictions for the virtual network where your App Service Environment is deployed.

When you integrate a function app in a Premium plan or an App Service plan with a virtual network, the app can still make outbound calls to the internet by default. By integrating your function app with a virtual network with Route All enabled, you force all outbound traffic to be sent into your virtual network, where network security group rules can be used to restrict traffic.

# Demo

![Azure Function VNET Integration](/media/Architecture.png)

The <a href="https://youtu.be/hvHloEGqI-A" target="_blank">video</a> demonstrates the step-by-step process of Azure function VNET integration.  We will do it with a simple azure function that retrieves the data from the Azure storage table. Here is what we will do

1. Inbound Traffic
    1. The azure function is with App Service Plan Free tier. It is accessible over the internet.
    2. We will create a private endpoint for the Azure function and place this in the **sg-vnet** virtual network. 
    3. As soon as we create a private endpoint, the Azure function is access is blocked over the internet. The azure function is accessible only from the vent where the private endpoint is placed.
    4. To demonstrate Azure function access from **sg-vent**, we will create a virtual machine without a public IP address inside the same virtual network **sg-vnet.**
    5. As the virtual machine is a private one, we will also create a Bastion resource to access the VM.
    6. Now we will access the azure function from VM.
2. Outbound Traffic
    1. We will integrate the function app to sg-vnet, so traffic from the function app is restricted only to **sg-vnet**
    2. We will restrict the azure storage account access to **sg-vent**
    3. Now we again access the azure function from VM.
    
    <a href="https://youtu.be/hvHloEGqI-A" target="_blank">Watch it here</a>.
    
