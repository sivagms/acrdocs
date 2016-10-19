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

>[AZURE.NOTE]Container Registry is currently in preview.

# What is Azure Container Registry?

The Azure Container Registry provides local, network-close storage of your container images. By instancing a Container registry within your subscription, you have full control over the access and image names. By instancing a registry in the same data center as your deployments, your network latency will be reduced, as well removing ingress/egress charges.

## Deployment Targets
Docker is becoming the new [binary format for deployments](https://blogs.msdn.microsoft.com/stevelasker/2016/05/26/docker-containers-as-the-new-binaries-of-deployment/). Development and Operations teams can manage the configuration of their app, isolated from the configuration the hosting environment. Containers aren't just deployed to highly scalable orchestration systems like DC/OS, Docker Swarm and Kubernetes, but all types of deployments. 

App Services, Azure Batch and other services are coming online that support Containers as their deployment model.
Regardless of where you deploy containers, you'll need a place to store and manage the images. Using the Azure Container Registry, teams can store their images for all their container deployments. 

## Private Preview
Please note, the **Azure Container Registry is NOT yet public**. On November 16, 2016, we will announce public preview availability at Connect(). 

## Login URLs
For the initial private preview, you'll notice login urls created with `-exp` in the domain name. `contoso-exp.azurecr.io`. This is an indication that you are using an experimental version of the container registry. We will be changing the login urls to support multiple teams in what appears as a single registry, providing the ability for groups to manage their segmentation/sandbox of images. We aim to support multi-data center geo replication at a future date, and want to provide a stable image url developers can embed in their dockerfiles and deployment files (docker-compose.yml). 

We hope to stabilize the login urls in the coming weeks. We will provide a grace period to move your images from the `-exp` registry instances to the preview instances.  


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

See [Authenticating against the Azure Container Registry](./container-registry-authentication.md) for more info. 

#Support
For support, please email: [Azure Container Registry Discussions](mailto:acr-disc@microsoft.com)

## Next steps
* [Request Access to the ACR Private Preview](./container-registry-get-access.md)
* [Create a new Azure Container Registry using the Azure Portal ](./container-registry-get-started-portal.md)
* [Logging into the Azure Container Registry](container-registry-authentication.md) 
* [Install Azure Container Registry CLI ](./container-registry-get-started-azure-cli-install.md)
* [Create a new Azure Container Registry using the az CLI](./container-registry-get-started-docker-cli.md)
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)

 