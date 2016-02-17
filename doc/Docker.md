# Docker Container Instructions
These are preliminary instructions for loading software and infrastructure using Docker.  The initial example will show the steps for loading shiny.


For bevity this document will only show the configuration of the instance, not initial set up of keys and such.  All Docker related steps will be included.


## Instance Specifications

The instance used for this tutorial is shown below.

![GCP_Instance_Specs](/img/docker1.jpg)


I also attached a previously used static IP.

##  SSH Instructions

You could use Putty and the key structure that we use, or you could log in to the cloud console and use that SSH.

I'm using the cloud console.

## Docker installation

I like to start with updating what is already on the server using apt-get.

```
sudo apt-get update

```

Docker is installed using the instructions for Ubuntu 14.04 Trusty shown here:
 - http://www.liquidweb.com/kb/how-to-install-docker-on-ubuntu-14-04-lts/
 - I do skip the `sed '$acomplete -F _docker docker' /etc/bash_completion.d/docker.io'` since it doesn't run, but docker still does.
 - Test the install using the Ubuntu image like the post says

## Installing Shiny server

I want to be able to install shiny server using the rocker/shiny docker hub image to start (I may create my own Dockerfile later using the Google Container Registry).

Here are the steps I'm using to install the container.

1. Check out the docker hub page: https://hub.docker.com/r/rocker/shiny/
2. Run container using the following command [this is actually what installs it]:
```
docker run --rm -p 3838:3838 rocker/shiny &
```
3. Verify installation by checking the IP for your instance and adding ':3838' to the IP in a browser.
