<properties
   pageTitle="Access to Container Registry [revoew | Microsoft Azure"
   description="Request access to the Azure Container Registry private preview."
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
   ms.date="10/25/2016"
   ms.author="stevelas"/>

# Request Access to the Azure Container Registry private preview

To get started, request access to the Container Registry private preview by running this [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) command:

```
Register-AzureRmProviderFeature -FeatureName "PrivatePreview" -ProviderNamespace "Microsoft.ContainerRegistry"

```

or using the [Azure CLI 2.0 Preview](https://github.com/azure/azure-cli):

```
az resource feature register --namespace Microsoft.ContainerRegistry -n PrivatePreview

```

You will see output similar to:

```
az resource feature show --name PrivatePreview --namespace Microsoft.ContainerRegistry
{
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxxx-xxxxxxxxxxxx/providers/Microsoft.Features/providers/Microsoft.ContainerRegistry/features/PrivatePreview",
  "name": "Microsoft.ContainerRegistry/PrivatePreview",
  "properties": {
    "state": "Pending"
  },
  "type": "Microsoft.Features/providers/features"
}
```

**Important**

Once you see that the state of your request is Pending, please send an email to `SteveLas@Microsoft.com` to approve the feature registration request. After your request if approved, you are ready to use the Container Registry private preview!

 


## Next steps
* [Create a container registry using the Azure Portal](./container-registry-get-started-portal.md)
* [Login to the container registry](container-registry-authentication.md) 
* [Install the Azure Container Registry CLI](./container-registry-get-started-azure-cli-install.md)
* [Create a container registry using the az CLI](./container-registry-get-started-docker-cli.md)
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)
 
