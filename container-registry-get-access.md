<properties
   pageTitle="Azure Container Registry introduction | Microsoft Azure"
   description="Azure Container Registry getting access..."
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

# Request Access through Subscription Registration

```
Register-AzureRmProviderFeature -FeatureName "PrivatePreview" -ProviderNamespace "Microsoft.ContainerRegistry"

```

or using `az` cross-platform CLI:

```
az resource feature register --namespace Microsoft.ContainerRegistry -n PrivatePreview

az resource feature show --name PrivatePreview --namespace Microsoft.ContainerRegistry
{
  "id": "/subscriptions/27b750cd-ed43-42fd-9044-8d75e124ae55/providers/Microsoft.Features/providers/Microsoft.ContainerRegistry/features/PrivatePreview",
  "name": "Microsoft.ContainerRegistry/PrivatePreview",
  "properties": {
    "state": "Pending"
  },
  "type": "Microsoft.Features/providers/features"
}
```

**Important**

Once you see your request pending email `sajaya` or `sivag` to approve the feature registration request.
 


## Next steps
* [Request Access to the ACR Private Preview](./container-registry-get-access.md)
* [Create a new Azure Container Registry using the Azure Portal](./container-registry-get-started-portal.md)
* [Logging into the Azure Container Registry](container-registry-authentication.md) 
* [Install Azure Container Registry CLI](./container-registry-get-started-azure-cli-install.md)
* [Create a new Azure Container Registry using the az CLI](./container-registry-get-started-docker-cli.md)
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)
 