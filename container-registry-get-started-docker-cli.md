<properties
   pageTitle="Work with images in a container registry | Microsoft Azure"
   description="Get started using the Docker CLI to push and pull images to/from an Azure container registry..."
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

>[AZURE.NOTE]Container Registry is currently in preview.

# Get started working with images in an Azure container registry

The Azure Container Registry is a private instance of the public [Docker Hub](http://hub.docker.com). The Azure Container Registry integrates with Docker CLI for login, push and pull operations. 


## Walk through
The follow example will download an NGINX image from Docker Hub, tag it for your private Azure Container Registry, push it to your registry, then pull it again.

* `docker pull nginx` will pull the Docker official image for NGINX
* `docker run -it --rm -p 8080:80 nginx` will start the NGINX container, interactively to see output from NGINX, listening on port 8080 and remove the running container once stopped.
* Browse to [http://localhost:8080](http://localhost:8080) to view the running container
* [CTRL] + [C] to stop the running container
* `docker tag nginx myregistry.azurecr.io/samples/nginx` will create an alias of the image, with a fully qualified path to your new registry. Note, we used the sample namespace to avoid polluting the root of our registry. 
* `docker push myregistry.azurecr.io/samples/nginx` will push this image to your private registry
* `docker rmi myregistry.azurecr.io/samples/nginx` will remove the image
* `docker pull myregistry.azurecr.io/samples/nginx` will pull the image from your private registry  
* `docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx` will start the NGINX container which was sourced from your private registry 






## Next Steps
Start deploying images to the [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/)
 

## Additional Docs

* [Create a new Azure Container Registry using the Azure Portal ](./container-registry-get-started-portal.md)
* [Logging into the Azure Container Registry](container-registry-authentication.md) 
* [Install Azure Container Registry CLI ](./container-registry-get-started-azure-cli-install.md)
* [Create a new Azure Container Registry using the az CLI](./container-registry-get-started-docker-cli.md)
* [Push your first image using the Docker CLI](./container-registry-get-started-docker-cli.md)
