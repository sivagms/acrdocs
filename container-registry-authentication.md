<properties
   pageTitle="Authenticate with a container registry | Microsoft Azure"
   description="How to authentiate with an Azure container registry with a service principal or a user account"
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



To push or pull container images from an existing Azure container registry, first authenticate with the registry by using the [docker login](https://docs.docker.com/engine/reference/commandline/login/) command. This article provides background about the identities you can use for authentication. 

For more Docker CLI commands you use with container registries, see [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md).

>[AZURE.NOTE]Container Registry is currently in private preview.

Login to a container registry using one of the following identities:


* **[Azure Active Directory service principal](https://azure.microsoft.com/documentation/articles/active-directory-application-objects/)** - For private preview, this is the recommended method. This allows you to assign roles to individual users. Service principals also enable headless connectivity for CI/CD solutions (VSTS/Jenkins) to push images, and for deployments (for example, with Azure App Service, Container Service, or Batch) to pull images.  

* **Admin account** - To support registry creation from the Azure portal, an admin account is 
added to each new container registry. The admin account is intended only to allow an Azure portal user a quick way to login to their newly created registry. It is not recommended to share the admin account with other users. 

    

At this time, individual Azure Active Directory identities (which enable per-user access and control) are not supported to authenticate with a container registry. 



## Service principal 

A straightforward way to configure a container registry with a service principal is by creating a registry with the [**az acr** commands](./container-registry-get-started-azure-cli.md). You can automatically create a default service principal when you create or update a registry, or assign an existing one.

For example, the following command creates a registry and a new service principal and password at the same time, in a resource group you previously created. Make sure to substitute your own resource names. 

```
az acr create -n myRegistry -g myResourceGroup -l southcentralus --new-sp -p myPassword -r Owner
```

See [Create a container registry with the Azure CLI](./container-registry-get-started-azure-cli.md) for more background and examples to assign a service principal to a registry.

For example, if you would like to create your own service principal using the Azure Active Directory CLI commands, see [Create a service principal](./container-registry-get-started-azure-cli.md#create-a-service-principal). You can then specify the service principal when you create a registry, or assign the service principal to an existing registry using the **az acr update** command.




## Admin account
To support registry creation from the Azure portal, an admin account and password are automatically created. (The admin account is also automatically created and enabled when you use Azure CLI commands to create a registry.) The admin account is intended as a stopgap, allowing Azure portal users a quick way to login to their newly created registry. This feature will be removed in later versions of Container Registry that support Azure Active Directory identities.

>[AZURE.IMPORTANT]It is not recommended to share the admin account with other users. All users will appear as a single user, and changing or disabling this account will disable all users that use the admin name and password. 
 
In the [Azure portal](./container-registry-get-started-portal.md#manage-registry-settings), you can obtain and manage the admin user account credentials in the **Access key** settings blade for a container registry.

Using the [**az acr** commands](./container-registry-get-started-azure-cli.md#manage-admin-credentials), you can also manage the user account credentials.



## Docker login example



You can authenticate with your container registry using the [docker login](https://docs.docker.com/engine/reference/commandline/login/) command and your registry credentials. The following example shows how to pass the service principal credentials (Id and password), which is recommended:

```
docker login myregistry-exp.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Once logged in, Docker caches the credentials, so you don't need to remember the service principal Id.

>[AZURE.TIP] If you want, you can regenerate the password of the service principal by running the **az ad sp reset-credentials** command.



### Next steps

* [Create a new Azure Container Registry using the Azure Portal ](./container-registry-get-started-portal.md)
* [Logging into the Azure Container Registry](container-registry-authentication.md) 
* [Install Azure Container Registry CLI ](./container-registry-get-started-azure-cli-install.md)
* [Create a new Azure Container Registry using the az CLI](./container-registry-get-started-azure-cli.md)
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)
