<properties
   pageTitle="Azure Container Registry introduction | Microsoft Azure"
   description="Azure Container Registry provides a cloud-based Docker private registry."
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
   ms.date="10/31/2016"
   ms.author="stevelas"/>



# What is Azure Container Registry?

Azure Container Registry is a managed Docker registry service to store and manage your private [Docker container](https://www.docker.com/what-docker) images. Container Registry gives you the ability to create and manage private registry instances similar to the public [Docker Hub](http://hub.docker.com). 

By creating a container registry within your subscription, you have full control over access and image names for all of your container deployments. Ceate a registry in the same Azure location as your deployments to take advantage of local, network-close storage of your container images. This can help reduce network latency in your deployments as well as reduce charges for storage ingress and egress.

For background about Docker and containers, see:

* [Docker user guide](https://docs.docker.com/engine/userguide/)
* [Docker containers as the new binaries of deployment](https://blogs.msdn.microsoft.com/stevelasker/2016/05/26/docker-containers-as-the-new-binaries-of-deployment/) 


## Key concepts

* **Registry** - Create one or more container registries in your Azure subscription. Each registry is backed by an Azure storage account in the same region. Configure your deployment targets to access container images in your registries. 

* **Repository** - Each registry consists of one or more repositories, which are collections of related images. Azure Container Registry supports multilevel namespaces. This enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational groups. For example:

    * `contoso.azurecr.io/aspnetcore:1.0.1` represents a corporate wide image
    * `contoso.azurecr.io/warrantydept/dotnet-build` represents an image used to build dotnet apps, shared across the warranty department
    * `contoso.azrecr.io/warrantydept/customersubmissions/web` represents a web image, grouped in the constomersubmissions app, owned by the warranty department

* **Image** - Images are read-only snapshots of Docker containers. Use standard [Docker commands](https://docs.docker.com/engine/reference/commandline/) to push images into a Container Registry repository, or pull an image from a repository.

* **Container** - A container defines a software application and its dependencies wrapped in a complete filesystem including code, runtime, system tools, and libraries. Containers running on a single machines share the same operating system kernel. Docker containers are fully portable to all major Linux distros, Mac, and Windows.




## Deployment targets
Development and Operations teams can manage the configuration of their app, isolated from the configuration of the hosting environment. Deploy containers from an Azure container registry to a variety of deployment targets:

* **Scalable orchestration systems** including DC/OS, Docker Swarm, and Kubernetes

* **Azure services** including Container Service, App Service, and Batch  

## Login URLs
For the initial private preview, you'll notice login urls created with **-exp** in the domain name - for example, `contoso-exp.azurecr.io`. This is an indication that you are using an experimental version of the Container Registry service. We will be changing the login urls to support multiple teams in what appears as a single registry, providing the ability for groups to manage their segmentation/sandbox of images. We aim to support multi-data center geo replication at a future date, and want to provide a stable image url developers can embed in their dockerfiles and deployment files (docker-compose.yml). 

We hope to stabilize the login urls in the coming weeks. We will provide a grace period to move your images from the `-exp` registry instances to the preview instances.  




## Securing registry access
For the initial private preview, securing a registry is limited to basic authentication flows using usernames and passwords, managed with Azure Active Directory service principals. 

At a future date, integration with individual Azure Active Directory identities will be provided, allowing you to manage access to a registry with Active Directory groups. 

See [Authenticating with a container registry](./container-registry-authentication.md) for more info. 

>[AZURE.IMPORTANT]The **Azure Container Registry service is NOT yet public**. On November 16, 2016, we will announce public preview availability at Connect().

## Support
For support, please email: [Azure Container Registry Discussions](mailto:acr-disc@microsoft.com)

## Next steps
* [Request Access to the ACR Private Preview](./container-registry-get-access.md)
* [Create a container registry using the Azure portal ](./container-registry-get-started-portal.md)
* [Authenticate with a container registry](container-registry-authentication.md) 
* [Install the Azure CLI for Container Registry CLI preview](./container-registry-get-started-azure-cli-install.md)
* [Create a new Azure Container Registry using the az CLI](./container-registry-get-started-docker-cli.md)
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)

 