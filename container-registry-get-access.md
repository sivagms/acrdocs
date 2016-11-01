<properties
   pageTitle="Access to Container Registry preview | Microsoft Azure"
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

# Access to the Container Registry private preview

Here are one-time steps to get access to the Container Registry private preview from you your Azure subscription.

## Step 1: Register your subscription with the resource provider

Using [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/):

```
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ContainerRegistry
```

Using the [Azure CLI 2.0 Preview](https://github.com/azure/azure-cli):

```
$ az resource provider register -n "Microsoft.ContainerRegistry"

```

## Step 2: Register with the Container Registry feature

Using Azure PowerShell:

```
Register-AzureRmProviderFeature -FeatureName "PrivatePreview" -ProviderNamespace "Microsoft.ContainerRegistry"

```

Using the Azure CLI 2.0 Preview:

```
az resource feature register --namespace Microsoft.ContainerRegistry -n PrivatePreview

```

If you run this CLI command:

```
az resource feature show --name PrivatePreview --namespace Microsoft.ContainerRegistry
```

You'll see output similar to:
```
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
* [Create a container registry using the Azure portal](./container-registry-get-started-portal.md)
* [Login to a container registry](container-registry-authentication.md) 
* [Install the Azure CLI for Container Registry preview](./container-registry-get-started-azure-cli-install.md)
* [Create a container registry using the Azure CLI](./container-registry-get-started-docker-cli.md)
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)
 
