<properties
   pageTitle="Container Registry in the Portal | Microsoft Azure"
   description="Get started with the Azure Container Registry in the Azure portal..."
   services="container-registry"
   documentationCenter=""
   authors="stevelas"
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
   ms.date="10/07/2016"
   ms.author="stevelas"/>

# Get started using the Container Registry in the Azure portal


>[AZURE.NOTE]Container Registry is currently in preview.


## Crate a New Container Registry
While the Container Registry is in preview, you'll need to add a query parameter to your portal URL. Use the following URL [https://aka.ms/acr/portal](https://aka.ms/acr/portal) to launch the portal, with the ACR preview enabled.

* Navigate to [https://aka.ms/acr/portal](https://aka.ms/acr/portal) 
* Click [+ Add] button 
* Enter a globally unique dns name that represents your specific instance. eg: warrantycontoso
	* **note: for the first round of preview, all registries will have -exp concatenated to the login url. In the next few weeks, prior to the public preview, the login urls will change.**  
* Enter a resource group, or select an existing resource group
* Choose a location. **Note:** New locations will be supported at a later date
* Use the default for creating a new storage account, or select an existing storage account

## Next steps

* [Request Access to the ACR Private Preview](./container-registry-get-access.md)
* [Create a new Azure Container Registry using the Azure Portal ](./container-registry-get-started-portal.md)
* [Logging into the Azure Container Registry](container-registry-authentication.md) 
* [Install Azure Container Registry CLI ](./container-registry-get-started-azure-cli-install.md)
* [Create a new Azure Container Registry using the az CLI](./container-registry-get-started-azure-cli.md)
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)
 
