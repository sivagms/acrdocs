<properties
   pageTitle="Install the az acr commands | Microsoft Azure"
   description="Install the Azure CLI 2.0 Preview for Azure Container Registry private preview"
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
   ms.date="10/25/2016"
   ms.author="stevelas"/>

# Install the Azure CLI for Container Registry preview

For Container Registry private preview, the Azure Container Registry CLI commands (**az acr** commands) can only be acquired using a Docker image of the Azure CLI 2.0 Preview.  


## Prerequisites


* **Container Registry private preview** - See the [instructions](container-registry-get-access.md) to register your Azure subscription and request access.

* **Docker host** - To set up your local computer as a Docker host, see the [Docker documentation](https://docs.docker.com/engine/installation/).

## Download the Azure CLI Docker image

To download the Azure CLI 2.0 Preview image in a Docker host on your computer, use the preview username and password shown in the following **docker login** command. 

```
docker login tryacr.azurecr.io -u 9489be1b-1dfb-4a71-9f03-bc7f8a09384e -p Microsoft
```

To run the Docker image:
```
docker run -it tryacr.azurecr.io/cli
```

To avoid having to login each time, it's recommended to stop and restart the container. Killing, removing the container, and issuing a new **docker run** will require reauthenticating.

## Configure the  CLI
To get started, there are a few configurations you'll likely want to make.

```
az configure
```
   
Follow the prompts to configure the output format, data collection, and Azure environment (public azure, us-gov, china-cloud, azure-stack)

## Login to Azure
To access resources in Azure, you need to complete the device login:

```
az login
```

Once you complete the device login flow, you'll have access to your Azure resources.


## Set the default subscription
If you have multiple subscriptions, you'll likely want to verify, or possibly change the default

```
az account list
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

Using the [Azure portal](https://portal.azure.com), select the [Subscriptions blade](https://ms.portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) and copy the subscription Id you wish to make the default. Pass it to the **az account set** command as follows:

```
az account set --name "mySubscriptionId"

```

##End the Session
Hit [CTRL]+[D] to disconnect the session. This ends the session. However, the image is still available to restart with the same credentials and configurations, just as if the CLI was installed directly on your machine. 
Find the container Id with `docker ps -a`, start the container, then attach to the running container, hitting [Enter] to get a # prompt.

```
docker ps -a
docker start [container Id]
docker attach [container Id]
[Enter]
```

## Next steps

* [Create a container registry using the Azure CLI](./container-registry-get-started-azure-cli.md)

## Additional docs

* [Request access to the ACR private preview](./container-registry-get-access.md)
* [Create a container registry using the Azure portal ](./container-registry-get-started-portal.md)
* [Login to a container registry](container-registry-authentication.md) 
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)
