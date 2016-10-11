<properties
   pageTitle="Azure Container Registry introduction | Microsoft Azure"
   description="Azure Container Registry provides a cloud-based Docker private registry..."
   services="container-registry"
   documentationCenter=""
   authors="stvelas"
   manager="balans"
   editor="dlepow"
   tags=""
   keywords=""/>

<tags
   ms.service="container-registry"
   ms.devlang="na"
   ms.topic="get-started-article"
   ms.tgt_pltfrm="na"
   ms.workload="na"
   ms.date="10/10/2016"
   ms.author="stevelas"/>

# What is Azure Container Registry?

The Azure Container Registry provides local, network-close storage of your container images. By instancing a Container registry within your subscription, you have full control over the access and image names. By instancing a registry in the same data center as your deployments, your network latency will be reduced, as well removing ingress/egress charges.


>[AZURE.NOTE]Container Registry is currently in preview.


## Namespace Support
The Azure Container Registry supports multi-level namespaces. This enables grouping collections of images related to a specific app, or a collection of apps to specific groups.

* `contoso.azurecr.io/aspnetcore:1.0.1` represents a corporate wide image
* `contoso.azurecr.io/warrantydept/dotnet-build` represents an image used to build dotnet apps, shared across the warranty department
* `contoso.azrecr.io/warrantydept/customersubmissions/web` represents a web image, grouped in the constomersubmissions app, owned by the warranty department
* `contoso.azrecr.io/warrantydept/customersubmissions/api` represents an api image, used in the same customersubmissions application. 
* `contoso.azrecr.io/marketing/products/web` represents a similar structure, for the marketing department 
* `contoso.azrecr.io/marketing/products/api` 
* `contoso.azrecr.io/marketing/products/test/functionaltest` represents a collection of images for testing the marketing site. 

## Securing Registry Access
For the initial private preview, securing a registry is limited basic auth flows using username and passwords  managed with service principals. 
At a future date, integration with individual AAD identity will be provided, allowing you to manage access to a registry with AAD groups. 

See [Authenticating against the Azure Container Registry](/container-registry-authenticating.md) for more info. 


## Next steps

* [Create a new Azure Container Registry using the Azure Portal ](./container-registry-get-started-portal.md)
* [Install Azure Container Registry CLI ](./container-registry-get-started-azure-cli-install.md)
* [Create a new Azure Container Registry using the az CLI](./container-registry-get-started-docker-cli.md)
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)
