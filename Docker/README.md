# Docker Cheat Sheet

## Content
1. [Starting Up](#STARTING "How to pull, push and start an image")
2. [Potential Issues](#ISSUES "Too many issues, what do i do?")
3. [Basic Commands](#COMMANDS "There is more that meets the eyes")
4. [STOP and REMOVE](#STOP_REMOVE "STOP IT NOW")




<!-- <start> Starting up  -->
## <a name="STARTING">  Starting up  </a>

To begin we need to start with an image to run to initialise the container.
    
### Pulling from the Docker Hub 

To begin we need to start with an image to run to initialise the container.
1. Login into the Docker account: 

> `To login to docker account: docker login –username:<username>`

2. Pull image from docker hub: 

> `docker pull <username>/<image>:<tagName>`

3. Pull and run image: 

> `docker run -rm -p 5001:5001 <username>/<image>:<tagName>`


### Pushing to the Docker Hub 

If we made changes to the image (hence a new image). We want to update the one on docker hub so that next time the image pulled would be the latest version.
1. Tag a version for the image (For our case, it is the Latest version): 

> `docker tag <imageID> <username>/<docke_page>:latest`

2. Push the new image to docker hub: 

> `docker push <username>/<docke_page>`

-------------------------------------------------------
<!-- <end> Starting up  -->




<!-- <start> Potential Issues  -->
## <a name="ISSUES">  Potential Issues  </a>

Like anything, setting up could pop up some challenges along the way.

**Possible Error 1:** `Docker – Unable to delete image with children`

Attempt to remove the Imame via the command below:

> `docker rmi -f <imageID>`

Else if can’t remove the image, try is commend:

> `docker rmi <imageName>`


**Possible Error 2:** `Docker - Cannot stop container: unified-platform_postgres_1: Cannot kill container / signaling init process caused "permission denied“ : unknown`


```
docker exec -it <containerID> /bin/sh OR bash 
kill 1
docker container stop <containerID>
docker container rm <containerID>
```

**Possible Error 3:** `Error response from daemon: cannot stop container: Cannot kill container: unknown error after kill: runc did not terminate sucessfully: container_linux.go:392: signaling init process caused "permission denied“ `

> `sudo aa-remove-unknown`

So no reinstallation of Apparmor was needed

**Possible Error 4:** Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```
sudo rm /var/run/docker.pid      # you can ignore this
sudo service docker stop
sudo service docker start
```
-------------------------------------------------
<!-- <end> Potential Issues  -->


<!-- <start> Useful Docker Commands  -->
## <a name="COMMANDS">  Useful Docker Commands  </a>

Aside from the commands we went through in the beginning, there are other commands that will help us on our journey.

|Function|command|
|--------|-------|
|List all the Containers | `docker container ls -a`|
|List all the Images | `docker image ls –a`|
|Delect An image: |`docker rmi <dockerID>`|
|Stop a running Container: |`docker container stop <dockerID>`|
|Remove a container: |`docker container rm <dockerID>`|
|Services are built once and then tagged  |`docker-compose build`| 
|Builds, (re)creates, starts, and attaches to containers for a service.|`docker-compose up -d`|
|Stops containers and removes containers, networks, volumes, and images |`docker-compose down -v`|
| Displays log output from services|`docker-compose logs –f`|
| |`docker-compose -f docker-compose.prod.yml up -d --build`|
| |`docker-compose -f docker-compose.prod.yml exec web python manage.py create_db`|

<!--
* List all the Containers | `docker container ls -a`     

* List all the Images | `docker image ls –a`

* Delect An image: `docker rmi <dockerID>`

* Stop a running Container: `docker container stop <dockerID>`

* Remove a container: `docker container rm <dockerID>`


`docker-compose build AND docker-compose up -d`

`docker-compose down -v`

`docker-compose logs –f`

`docker-compose -f docker-compose.prod.yml up -d --build`

`docker-compose -f docker-compose.prod.yml exec web python manage.py create_db`


```
docker container ls -a
docker image ls –a
docker rmi <dockerID>
docker container stop <dockerID>
docker container rm <dockerID>
docker-compose build AND docker-compose up -d
docker-compose down -v
docker-compose logs –f
docker-compose -f docker-compose.prod.yml up -d --build
docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
```
```
Flag
-- rm: Automatically remove the container and its associated file system upon exit
-- name: An identifying name for the container
-e: Expose environment variable of name POSTGRES_PASSWORD with value docker to the container
-d: Launches the container in detached mode or in other words, in the background
-p: Bind port 5432 on localhost to port 5432 within the container. 
-v: Mount $HOME/docker/volumes/postgres on the host machine to the container side volume path /var/lib/postgresql/data created inside the container. 

```
-->
------------------------------------------------------------
<!-- <end> Useful Docker Commands  -->


<!-- <start> Stop and Remove All Docker Containers and Images  -->
## <a name="STOP_REMOVE">  Stop and Remove All Docker Containers and Images </a>
### Handy Shortcuts

|Function|command|
|--------|-------|
| List all containers: | `(only IDs) docker ps -aq.`|
| Stop all running containers: | `docker stop $(docker ps -aq)`| 
| Remove all containers: | `docker rm $(docker ps -aq)`| 
| Remove all images: | `docker rmi $(docker images -q)`| 
| Remove all dangling images: | `docker rmi $(docker images --filter "dangling=true" -q --no-trunc)`| 
| Clean these components: |  `docker system prune` OR `docker image prune`| 

<!--
List all containers: `(only IDs) docker ps -aq.`

Stop all running containers: `docker stop $(docker ps -aq)`

Remove all containers: `docker rm $(docker ps -aq)`

Remove all images: `docker rmi $(docker images -q)`

Remove all dangling images: `docker rmi $(docker images --filter "dangling=true" -q --no-trunc)`

Clean these components: `docker system prune` OR `docker image prune`
-->
------------------------------------------------------------------------------------
<!-- <end> Stop and Remove All Docker Containers and Images   -->




<!-- 
Basic Command
docker container ls -a
docker image ls –a
docker rmi <dockerID>
docker container stop <dockerID>
docker container rm <dockerID>
docker-compose build AND docker-compose up -d
docker-compose down -v
docker-compose logs –f
docker-compose -f docker-compose.prod.yml up -d --build
docker-compose -f docker-compose.prod.yml exec web python manage.py create_db

Flag
-- rm: Automatically remove the container and its associated file system upon exit
-- name: An identifying name for the container
-e: Expose environment variable of name POSTGRES_PASSWORD with value docker to the container
-d: Launches the container in detached mode or in other words, in the background
-p: Bind port 5432 on localhost to port 5432 within the container. 
-v: Mount $HOME/docker/volumes/postgres on the host machine to the container side volume path /var/lib/postgresql/data created inside the container. 



-->
