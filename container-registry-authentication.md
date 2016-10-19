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

# Authenticating with the Azure Container Registry


>[AZURE.NOTE]Azure Container Registry and az CLI are currently in preview.


Users can authenticate with the Azure Container Registry using 3 methods:

* **Azure Active Directory Individual Identity** </br>
enabling per user access and control. *[not yet supported.]*
* **[Azure AD Service Principals](https://azure.microsoft.com/documentation/articles/active-directory-application-objects/)** </br> 
which enables headless connectivity for CI/CD solutions (VSTS/Jenkins) to push images and deployments (App Service, ACS, Batch) to pull images.  
* **Admin Account**</br>
added to each newly created Container Registry. This account was added as a workaround for getting started quickly, until AAD Individual Identities are supported. **Note: it is not recommended to share this account with other users. All users will appear as a single user. Changing or disabling this account will disable all users. By using Service Principals, you can manage individual users.    

The easiest way to configure a Container Registry with service principals uses the az CLI. See [Getting Started with the acr CLI](./container-registry-get-started-azure-cli.md)

## Using Service Principals 

### Assign a new Service Principal to an existing registry

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

## Next steps

* [Create a new Azure Container Registry using the Azure Portal ](./container-registry-get-started-portal.md)
* [Logging into the Azure Container Registry](container-registry-authentication.md) 
* [Install Azure Container Registry CLI ](./container-registry-get-started-azure-cli-install.md)
* [Create a new Azure Container Registry using the az CLI](./container-registry-get-started-docker-cli.md)
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)
