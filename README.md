# Configuring Jenkins on a conatiner attaching the volume to the host machine and running the agents on docker containers

This will guides you to configure jenkins and docker into containers and save your configuration of disasters (stop/restart/deletion and by making an explicit volume we can manage it and attach to another container for upgrades)

## Getting Started

at first you can use whatever image you want in order to configure jenkins and your containers, the images that we will (not all images that we will be used on this guide) use on this guide will be:

* [Oficial Jenkins Image](https://hub.docker.com/r/jenkins/jenkins/)
* [Oficial Jenkins / BlueOcean Image](https://hub.docker.com/r/jenkinsci/blueocean/) - you can find more information about this image on this [link](https://jenkins.io/projects/blueocean/)

BTW, we will being using an unix base SO, so we will explain all the commands based on that.

### Prerequisites

To follow this guide you need to have installed [Docker CE](https://docs.docker.com/v17.12/install/)

### Installing Jenkins

* Pull the jenkins image from docker hub

```
docker pull jenkinsci/blueocean
```

* Run the container on detached mode

```

docker run -d --restart=always -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 --user root -v /var/run/docker.sock:/var/run/docker.sock jenkinsci/blueocean:latest

```

* Go into the running container to get the initial password

```
docker exec -it --user root <the generated container id> /bin/bash
```

```
cat /var/jenkins_home/secrets/initialAdminPassword
```

and go to the installed [jenkins](http://localhost:8080) - http://localhost:8080

![image](https://user-images.githubusercontent.com/29414094/67592030-56e14d00-f724-11e9-87cf-a4d0010bbdef.png)

you need to paste the got password from the previously command into the field and press on continue, now, finish the installation as a common jenkins installation (installed initial plugins and thins like that). And also, create your initial admin user.

## Install Docker plugin

Go to "Manage Jenkins" => click on "Manage Plugins" => Go to "Available" Tab => search and select "Docker". With the Docker plugin integration, a new entry is created for Docker under "Manage Jenkins".

