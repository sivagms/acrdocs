<properties
   pageTitle="Container registries with the CLI | Microsoft Azure"
   description="Get started using the Azure Container Registry service with the Azure CLI 2.0 Preview"
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
   ms.date="10/19/2016"
   ms.author="stevelas"/>

# Get started with container registries using the Azure CLI 2.0 Preview


Use commands in the Azure CLI 2.0 Preview to create and manage container registries from the command line of your Linux, Mac, or Windows computer. You can also work with container registries using the [Azure portal](container-registry-get-started-portal.md) or programmatically with the container registry APIs.

For help on Azure CLI 2.0 Preview commands, pass the `-h` parameter to any command.

For background and concepts, see [What is Azure Container Registry?](container-registry-intro.md)

>[AZURE.NOTE]The Container Registry service and **az acr** commands are currently in Private Preview.

## Prerequisites

* **Container Registry Private Preview** - See the [instructions](container-registry-get-access.md) to register your Azure subscription and request access.

* **Azure CLI 2.0 Preview** - To install and get started with the Container Registry CLI commands, see the [installation instructions](container-registry-get-started-azure-cli-install.md). *For Private Preview, the **az acr** commands are only available by using a Docker image.*

* **Resource group** - Create a new resource group before creating a container registry, or use an existing resource group. Make sure the resource group is in a location where the Container Registry service is available. *For Private Preview, the service is available in the South Central US region.* To create a resource group using the CLI 2.0 Preview, see [the CLI 2.0 Preview samples](https://github.com/Azure/azure-cli-samples/tree/master/arm). 

* **Storage account** (optional) - Create a storage account to back the container registry in the same resource group. If you don't specify a storage account when creating a registry with **az acr create**, the command creates one for you. To create a storage account using the CLI 2.0 Preview, see [the CLI 2.0 Preview samples](https://github.com/Azure/azure-cli-samples/tree/master/storage).

* **Service principal** (optional) - For Preview, we recommend using an Azure Active Directory [service principal](https://azure.microsoft.com/documentation/articles/active-directory-application-objects/) to access the registry. For more information, see [Authenticate with the container registry](container-registry-authenticate.md). The CLI makes it easy to automatically create a default service principal when you create or update a registry, or assign an existing one. To create a service principal that you assign to a registry, see [Create a service principal](#create-a-service-principal). 


## Create a container registry

Run the **az acr create** command to create a container registry, as shown in the following examples. 

>[AZURE.TIP]When you create a registry, specify a globally unique top-level domain name, such as an organizational name, containing only letters and numbers. The registry name in the examples is **myRegistry**, but substitute a unique name of your own. To access the registry, use the fully qualified name myRegistry.azurecr.io.
  

## Create a container registry with the minimal parameters

The following command creates container registry **myRegistry** in the resource group **myResourceGroup** in the South Central US location:

```
az acr create -n myRegistry -g myResourceGroup -l southcentralus
```

* `--storage-account-name` or `-s` is optional. If not specified, a storage account is created with a random name in the specified resource group.

When you create a registry with minimal parameters, by default it is not set up for access. To allow access to the registry, you can assign a service principal. See [Assign a service principal to an existing registry](#assign-a-service-principal-to-an-existing-registry).

### Create a container registry with a new service principal

The following command creates container registry **myRegistry** and a new service principal in the resource group **myResourceGroup** in the South Central US location:


```
az acr create -n myRegistry -g myResourceGroup -l southcentralus --new-sp -p myPassword -r Owner
```

* `--password` or `-p` is optional. A random password is generated if not specified.

* `--role` or `-r` grants the service principal access to the registry with the specified role name (in this example, Owner).




### Create a container registry with an existing service principal

If you already created an Azure Active Directory service principal, you can specify its Id using a command similar to the following:

```
az acr create -n myRegistry -g myResourceGroup -l southcentralus --app-id xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -r Owner
```

* `app-id` is the Id for an existing service principal.

* `--role` or `-r` grants the service principal access to the registry with the specified role name (in this example, Owner).


## Assign a service principal to an existing registry

The following examples show different ways to run the **az acr update** command to assign a service principal to an existing container registry.

### Assign a new service principal to a registry

The following examplecreates a new service principal for the existing registry **myRegistry**.
 
```
az acr update -n myRegistry --new-sp -p myPassword -r Owner
```

* `--password` or `-p` is optional. A random password is generated if not specified.

* `--role` or `-r` grants the service principal access to the registry with the specified role name (in this example, Owner).

### Assign an existing service principal to a registry

```
az acr update -n myRegistry --app-id xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -r Owner
```

* `app-id` is the app id for an existing service principal.<br>
* `---role` or `-r` will grant the service principal access to the registry with the specified role name.


## Create a service principal

If you would like to create a new service principal using the Azure Active Directory command module, you need to create an application first (if you don't have one). 

```
az ad app create --display-name sp-test --homepage http://myRegistry.azurecr.io --identifier-uris http://myRegistry.azurecr.io --password myPassword
```

* `--password` is optional, and you can always regenerate a new password.
* `--homepage` and `--identifier-uris` can be anything, but they at least should be an URI. Use the login URL, myRegistry.azurecr.io, as a default.

Save the `appId` from the output. It's an Id of the form xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx*. You use it to create a service principal. Then, run the following command to create an service pricipal from the created application, passing the Id:

```
az ad sp create --id xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```


# Admin credentials
To support registry creation from the Azure portal an admin account is created. The admin account is intended as a stopgap, allowing Azure portal users a quick way to login to their newly created registry. 
 
**This feature will be removed once AAD is integrated into the new Azure Portal and/or integration with individual AAD Identity is completed. It is NOT recommended to use the admin account for access as individual as all users will use the same identity. Disabling the account or resetting the password will disable all users that usethe admin username and password.** 

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

## Listing images and tags 
Container Registry doesn't currently support **docker search**, nor is there a graphical UI to list images and tags.

However, use the **az acr** commands CLI to query the list of images and tags.

## List repositories 

```
az acr repository list -n myRegistry -o json`
```

## List tags

```
az acr repository show-tags -n Registry --repository samples/nginx -o jsonz`
```

## Next steps
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)

# Additional docs
* [Create a new Azure Container Registry using the Azure Portal](./container-registry-get-started-portal.md)
* [Logging into the Azure Container Registry](container-registry-authentication.md) 
* [Install Azure Container Registry CLI ](./container-registry-get-started-azure-cli-install.md)
* [Create a new Azure Container Registry using the az CLI](./container-registry-get-started-azure-cli.md)