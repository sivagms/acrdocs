<properties
   pageTitle="Container registries with the CLI | Microsoft Azure"
   description="Get started Installing the Azure Container Registry with the az CLI"
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

Once you see that your request is pending please send an email to `sajaya` or `sivag` to approve the feature registration request.


# Getting the az CLI


>[AZURE.NOTE]Container Registry and Azure CLI 2.0 are currently in preview.



## Downloading the Azure Container Registry Preview CLI
At this time the Azure Container Registry CLI can only be acquired using a docker image.  
To download the az CLI preview image, use the preview username and password below. 

```
docker login tryacr.azurecr.io -u 9489be1b-1dfb-4a71-9f03-bc7f8a09384e -p Microsoft
docker run -it tryacr.azurecr.io/cli
```

To avoid having to login each time, it's recommended to stop and restart the container. Killing, removing the container and issuing a new docker run will require re-authenticating.

## Configuring the az CLI
To get started, there are a few configurations you'll likely want to make.

```
az configure
```
   
Follow the prompts to configure the output format, data collection and choose the azure environment (public azure, us-gov, china-cloud, azure-stack)

## Logging into Azure
To access resources in Azure, you'll need to complete the device login

```
az login
```

Once you complete the device login flow, you'll have access to your azure resources


## Set the default subscription
If you have multiple subscriptions, you'll likely want to verify, or possibly change the default

```
az account list
```

If the default is not the subscription you wish to work with, change the default using:


```
az account set --name "[subscription name]"
```

You may see duplicate subscription names, making it difficult to set the default subscription.

   
```
  IsDefault  EnvironmentName    TenantId                              State    Name
-----------  -----------------  ------------------------------------  -------  ------------------------------------
  1          AzureCloud         aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  Enabled  Microsoft Azure Internal Consumption
             AzureCloud         aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  Enabled  Microsoft Azure Internal Consumption
             AzureCloud         aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  Enabled  Visual Studio - Data Catalog
             AzureCloud         aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  Enabled  CBA Azure Subscription
```

Using the Azure Portal, select the subscritpions blade and copy the subscription id you wish to make the default and pass it to the `az account` CLI. 

```
az account set --name "[subscription id]"
az account set --name "f8888888-6666-5555-4444-333333333333"
```

## End the Session
Hit [CTRL] + [D] to disconnect the session. This will end the session, however the image is still available to restart with the same credentials and configurations, just as if the CLI was installed directly on your machine. 
Find the container id with `docker ps -a`, start the container, then attach to the running container, hitting [enter] to get a # prompt.

```
docker ps -a
docker start [container id]
docker attach [container id]
[enter]
```

## Next steps

* [Request Access to the ACR Private Preview](./container-registry-get-access.md)
* [Create a new Azure Container Registry using the Azure Portal ](./container-registry-get-started-portal.md)
* [Logging into the Azure Container Registry](container-registry-authentication.md) 
* [Install Azure Container Registry CLI ](./container-registry-get-started-azure-cli-install.md)
* [Create a new Azure Container Registry using the az CLI](./container-registry-get-started-azure-cli.md)
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)
