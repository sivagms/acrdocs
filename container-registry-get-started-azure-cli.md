<properties
   pageTitle="Create a container registry with the CLI | Microsoft Azure"
   description="Get started creating and managing Azure container registries with the Azure CLI 2.0 Preview"
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

# Create a container registry using the Azure CLI


Use Azure Command-Line Interface (CLI) commands to create a container registry and manage its settings from your Linux, Mac, or Windows computer. You can also work with container registries using the [Azure portal](container-registry-get-started-portal.md) or programmatically with the Container Registry APIs.

* For help on Container Registry CLI commands (**az acr** commands), pass the `-h` parameter to any command.

* For background and concepts, see [What is Azure Container Registry?](container-registry-intro.md)

* To get started with Docker images in your registry, see [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md).

>[AZURE.NOTE]Container Registry is currently in private preview.

## Prerequisites

* **Container Registry private preview** - See the [instructions](container-registry-get-access.md) to register your Azure subscription and request access.

* **Azure CLI 2.0 Preview** - To install and get started with the **az acr** commands, see the [installation instructions](container-registry-get-started-azure-cli-install.md). *For private preview, the az acr commands are only available by running a Docker image of the Azure CLI 2.0 Preview.*

* **Resource group** - Create a new resource group before creating a container registry, or use an existing resource group. Make sure the resource group is in a location where the Container Registry service is available. *For private preview, the service is available in the South Central US region.* To create a resource group using the CLI 2.0 Preview, see [the CLI 2.0 Preview samples](https://github.com/Azure/azure-cli-samples/tree/master/arm). 

* **Storage account** (optional) - Create a storage account to back the container registry in the same resource group. If you don't specify a storage account when creating a registry with **az acr create**, the command creates one for you. To create a storage account using the CLI 2.0 Preview, see [the CLI 2.0 Preview samples](https://github.com/Azure/azure-cli-samples/tree/master/storage).

* **Service principal** (optional) - For private preview, we recommend using an Azure Active Directory [service principal](https://azure.microsoft.com/documentation/articles/active-directory-application-objects/) to access the registry. For more information, see [Authenticate with the container registry](container-registry-authenticate.md). The CLI makes it easy to automatically create a default service principal when you create or update a registry, or assign an existing one. To create a service principal that you assign to a registry, see [Create a service principal](#create-a-service-principal). 


## Create a container registry

Run the **az acr create** command to create a container registry, as shown in the following examples. 

>[AZURE.TIP]When you create a registry, specify a globally unique top-level domain name, such as an organizational name, containing only letters and numbers. The registry name in the examples is **myRegistry**, but substitute a unique name of your own. When you [login to the registry](./container-registry-authentication.md), use the fully qualified name **myregistry-exp.azurecr.io** (all lowercase; the "-exp" in the prefix is only required for preview).
  

### Create a container registry with the minimal parameters

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

The service principal Id is returned in the command output.


### Create a container registry with an existing service principal

If you already created an Azure Active Directory service principal, you can specify its Id using a command similar to the following:

```
az acr create -n myRegistry -g myResourceGroup -l southcentralus --app-id xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -r Owner
```

* `--app-id` is the Id for an existing service principal.

* `--role` or `-r` grants the service principal access to the registry with the specified role name (in this example, Owner).


## Assign a service principal to an existing registry

The following examples show different ways to run the **az acr update** command to assign a service principal to an existing container registry.

### Assign a new service principal to a registry

The following example creates a new service principal for the existing registry **myRegistry**.
 
```
az acr update -n myRegistry --new-sp -p myPassword -r Owner
```

* `--password` or `-p` is optional. A random password is generated if not specified.

* `--role` or `-r` grants the service principal access to the registry with the specified role name (in this example, Owner).

The service principal Id is returned in the command output.

### Assign an existing service principal to a registry

```
az acr update -n myRegistry --app-id xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -r Owner
```

* `--app-id` is the Id for an existing service principal.

* `--role` or `-r` grants the service principal access to the registry with the specified role name (in this example, Owner).


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


## Manage admin credentials
To support registry creation from the Azure portal, an admin account is created for each container registry. The admin account is intended only as a stopgap, allowing Azure portal users a quick way to login to their newly created registry. For Container Registry preview, use of a service principal is recommended. For more information, see [Authenticate with a container registry](./container-registry-authentication.md).
 
The following examples show **az acr** CLI commands  to manage the admin credentials for your container registry.

### Obtain admin user credentials

```
az acr credential show -n myRegistry
```

### Enable admin user for an existing registry

```
az acr update -n myRegistry --enable-admin
```

### Disable admin user for an existing registry

```
az acr update -n myRegistry --disable-admin
```

## List images and tags 
Container Registry doesn't currently support **docker search**, nor is there a graphical UI to list images and tags.

However, use the **az acr** CLI commands to query the list of images and tags.

### List repositories 

The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:

```
az acr repository list -n myRegistry -o json`
```

### List tags
The following example lists the tags on the **samples/nginx** repository, in JSON format:

```
az acr repository show-tags -n myRegistry --repository samples/nginx -o json`
```

## Next steps
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)

## Additional docs
* [Create a container registry using the Azure portal](./container-registry-get-started-portal.md)
* [Login to a container registry](container-registry-authentication.md) 
* [Install the Azure CLI for Container Registry preview](./container-registry-get-started-azure-cli-install.md)
