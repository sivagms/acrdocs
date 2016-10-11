<properties
   pageTitle="Container registries with the CLI | Microsoft Azure"
   description="Get started using the Azure Container Registry with the az CLI..."
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

# Get started working with container registries through the Azure CLI


>[AZURE.NOTE]Container Registry and Azure CLI 2.0 are currently in preview.


# Create a Registry
For Preview, Container Registry access is secured using [service principals](https://azure.microsoft.com/documentation/articles/active-directory-application-objects/). You can create a new container registry with or without an associated service principal and add one after creation.  

## Create a Container Registry with the minimal parameters

```
az acr create -n myRegistry -g myResourceGroup -l southcentralus
```

* `--storage-account-name` or `-s` is optional. A random storage account name will be generated if not specified.

## Create a Registry with a new Service Principal

```
az acr create -n myRegistry -g myResourceGroup -l southcentralus --new-sp -p myPassword -r Owner
```

* `--password` or `-p` is optional. A random password will be generated if not specified.
* `--role` or `-r` will grant the service principal access to the registry with the specified role name.

## Create a Registry with an existing Service Principal

```
az acr create -n myRegistry -g myResourceGroup -l southcentralus --app-id 7fcc3bb8-98d3-4324-87a5-a7d2fffdc703 -r Owner
```

* `app-id` is the app id for an existing service principal.
* `--role` or `-r` will grant the service principal access to the registry with the specified role name.

# Assign a new Service Principal to an existing registry

```
az acr update -n myRegistry --new-sp -p myPassword -r Owner
```

* `--password` or `-p` is optional. A random password will be generated if not specified.<br>
* `--role` or `-r` will grant the service principal access to the registry with the specified role name.

# Assign an existing Service Principal to an existing registry

```
az acr update -n myRegistry --app-id 7fcc3bb8-98d3-4324-87a5-a7d2fffdc703 -r Owner
```

* `app-id` is the app id for an existing service principal.<br>
* `---role` or `-r` will grant the service principal access to the registry with the specified role name.

# Docker login using a Service Principal

You can login to Docker using your service pricipal credentials (tips: you can always regenerate a new password):
```
docker login myRegistry.azurecr.io -u 7fcc3bb8-98d3-4324-87a5-a7d2fffdc703 -p myPassword
```

Once logged in, Docker will cache the credentials, avoiding the need to remember the Service Principal GUID.

# Create a new Service Principal

If you would like to create a new service principal using AAD command module, you will need to create an application first if you don't have one. 

```
az ad app create --display-name sp-test --homepage http://sp-test --identifier-uris http://sp-test --password myPassword
```

* `--password` is optional, and you can always regenerate a new password.<br>
* `--homepage` and `--identifier-uris` can be anything, but they at least should be an URI. Use the login url, myregistry.azurecr.io as a default.

1. Save the `appId` from the output, you will use it to create a service principal.
2. Then you can create an service pricipal from the created application:

```
az ad sp create --id 7fcc3bb8-98d3-4324-87a5-a7d2fffdc703
```


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

