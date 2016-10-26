<properties
   pageTitle="Authenticate with a container registry | Microsoft Azure"
   description="Methods to authenticate with an Azure container registry by using the Azure CLI"
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

# Authenticate with a container registry


>[AZURE.NOTE]The Container Registry service and **az acr** commands are currently in private preview.

To push or pull container images from an existing Azure container registry, users must authenticate with the registry. For private preview, users can authenticate with a container registry using the following methods:


* **[Azure Active Directory service principal](https://azure.microsoft.com/documentation/articles/active-directory-application-objects/)** - For private preview, this is the recommended method. This allows you to manage individual users. Service principals also enable headless connectivity for CI/CD solutions (VSTS/Jenkins) to push images and for deployments (for example, with Azure App Service, Container Service, or Batch) to pull images.  
* **Admin account** - To support registry creation from the Azure portal, an admin account is 
added to each new container registry. The admin account is intended as a stopgap, allowing Azure portal users a quick way to login to their newly created registry. 

>[AZURE.IMPORTANT]It is not recommended to share this account with other users. All users will appear as a single user, and changing or disabling this account will disable all users that use the admin name and password. 

For private preview, individual Azure Active Directory identities are not supported to authenticate with a container registry. 
enabling per user access and control. 


## Use service principals 

The easiest way to configure a container registry with a service principal is by creating a registry with the **az acr create** command. The CLI makes it easy to automatically create a default service principal when you create or update a registry, or assign an existing one. 

For example, the following command creates a registry and a new service principal at the same time:

```
az acr create -n myRegistry -g myResourceGroup -l southcentralus --new-sp -p myPassword -r Owner
```

See [Create a container registry with the Azure CLI](./container-registry-get-started-azure-cli.md) for more background and examples to assign a service principal to a registry.

For example, if you would like to create your own service principal using the Azure Active Directory CLI commands, see [Create a service principal](./container-registry-get-started-azure-cli.md#create-a-service-principal). You can then specify the service principal when you create a registry, or assign the service principal to an existing registry using the **az acr update** command.


## Docker login using a service principal

You can login to Docker using your service pricipal credentials (tips: you can always regenerate a new password):
```
docker login myRegistry.azurecr.io -u 7fcc3bb8-98d3-4324-87a5-a7d2fffdc703 -p myPassword
```

Once logged in, Docker will cache the credentials, avoiding the need to remember the Service Principal GUID.


# Admin Credentials
To support creation from the Azure Portal an admin account will be created. The admin account is intended as a stop gap, allowing Azure Portal users a quick way to login to their newly created registry. 
 
**This feature will be removed once AAD is integrated into the new Azure Portal and/or integration with individual AAD Identity is completed. It is NOT recommended to use the admin account for access as individual as all users will use the same identity. Disabling the account or resetting the password will disable all users that have used the admin username/password.** 

See Service Principals for adding individual users. 

## Obtain admin user credentials

```
az acr credential show -n myRegistry
```

## Enable admin user for an existing registry

```
az acr update -n myRegistry --enable-admin
```

## Disable admin user for an existing registry

```
az acr update -n myRegistry --disable-admin
```

## Next steps

* [Create a new Azure Container Registry using the Azure Portal ](./container-registry-get-started-portal.md)
* [Logging into the Azure Container Registry](container-registry-authentication.md) 
* [Install Azure Container Registry CLI ](./container-registry-get-started-azure-cli-install.md)
* [Create a new Azure Container Registry using the az CLI](./container-registry-get-started-azure-cli.md)
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)
