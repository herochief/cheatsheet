# Docker Cheat Sheet

## Content
1. [Starting Up](#STARTING "How to pull, push and start an image")
1. [Dockerfile](#DOCKERFILE "How to create a new image")
1. [Docker Compose](#DOCKERCOMPOSE "How to connect individual containers")
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

> `docker pull <username>/<imageName>:<tagName>`

3. Pull and run image: 

> `docker run -rm -p 5001:5001 <username>/<imageName>:<tagName>`


### Pushing to the Docker Hub 

If we made changes to the image (hence a new image). We want to update the one on docker hub so that next time the image pulled would be the latest version.
1. Tag a version for the image (For our case, it is the Latest version): 

> `docker tag <imageID> <username>/<imageName>:latest`

2. Push the new image to docker hub: 

> `docker push <username>/<imageName>`

-------------------------------------------------------
<!-- <end> Starting up  -->



<!-- <start> Dockerfile  -->
## <a name="DOCKERFILE">  Dockerfile  </a>

What is a Dockerfile: \
Lets start at the end. You end with a running container. In order to create the container you need an image. This image is portable and can be shared with others, furthermore it is secure as each image is unique. However, the image might not be to your needs. A dockerfile will create a new image with added functions from a base image.

Eg. Your basic image may only run python. BUT you need other libraries and extra applications. A dockerfile must be made and run to create a new image with all this functions.

Why do we use dockerfile instead of just updating the libraries in the running container: \
You put it very simply (but not always the case), all the data input and created in the container is only temporary. Hence, you need to create an image with the libraries beforehand, which is using the dockerfile.


**1)Create a docker file:**

First to create a dockerfile is literally create a file with the name `Dockerfile`. **NO** extensions added. \
When running command later, the command will automatically look for the `Dockerfile` file. (like `$ make` will build th `makefile`)

To be on the safe side, lets be case sensitive. ~~dockerfile~~ Dockerfile

> `$ touch Dockerfile`


**2) Contents for the dockerfile:**

Now the dockerfile needs some contents to know what to run. Open your dockerfile with any text editor

> `$ gedit Dockerfile`

        FROM alpine:3.4 
        MAINTAINER <name> <email>

        RUN apt-get update && \
            install gedit \
            vim

        RUN pip install numpy
    
You start with the a base image (in this case is the alpine:3.4) and new we will add gedit, vim and install numpy for python.


**3) Creating the image:**

Now is to build the image. Note that you need a name and version in the format of `<name>:<version>`

> `$ docker build -t <name>:<version> <path/to/dockerfile>` \
eg `$ docker build -t Hero_image:001 .` The fullstop is to say current folder.

**4) Extra notes**

You have now created a new image. \
This is merely a basic example on using Dockerfile. \
There are more commands that can be used in the docker file, visit their [site](https://docs.docker.com/engine/reference/builder/) from more details. \
If you want more in-depth but still basic tutorial, you can try this [video](https://www.youtube.com/watch?v=6Er8MAvTWlI&t=806s) by [takacsmark](https://www.youtube.com/channel/UCNaxXS9VOYKyVbT--ctbHEA).



--------------------------------------------------
<!-- <end> Dockerfile -->



<!-- <start> Docker Compose -->
## <a name="DOCKERCOMPOSE">  Docker Compose  </a>

What is the docker compose function for: \
For the previous times, we have beening working with individual images and containers, Each image and container are isolated from local system. Instead of having an entire application on an image, it would be wiser to separate the entire application into modules , especially if the each part might have their own libraries. 

However, if each container is isolated, how do we connect them each other. That is where docker compose comes in. \
Docker Compose allows (or tells) several container to run. Basically running multi-container. 

I will simplify and go through the docker compose examples from the main docekrsite.

### 1) Setup the necessary files.

We need the files for our project first. For the sake of our example will need 3 files. (All in the same directory)

FILES   | Description 
------  | -------
app.py          | A python file that will be the basis of our example project.
requirements.txt | Libraries that are required for the app.py to run.
Dockerfile | To create the image with the app.py. requirements and the necessary libraries.

> `touch app.py requirements.txt Dockerfile`

Next are the contents of the files

#### i) app.py
```
import time

import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)

@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)

```

#### ii) requirements.txt
```
flask
redis
```

#### iii) Dockerfile
```
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run"]
```
Do not worry about the details as this is merely an example to run.

### 2) Create the Compose file

Like the dockfile for images, Compose files to tell the docker which images to run and how to run.

> `docker-compose.yml`
```
version: "3.9"
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"

```
`services` : Defines the section for the services to be defined. \
`web` and `redis` : This services names are abitary (like a variable), it does not need to be the same as any image or container name. Good to have the name be easy to recognise application or function.

`web`: Define the service for our web function application and the environment of it. 
* `build` defines the dockerfile to built the image to run later. 
* `ports` is the port number to open.

`redis` :  Defines image for storing data. This directly from the dockerhub. 
* `image` defines the redis image to use.

**Note**: If you have not notice, the compose file is written to run 2 images. 
1. Web service: create the image from the docekrfile and run it.
2. redis service: redis image

### 3) Build and run your app with Compose

Let run our Compose file
> `$ docker-compose up`

To test if it is working, go to http://localhost:5000/

### More details

For more details on docker compose, you can visit the [docker site](https://docs.docker.com/compose/gettingstarted/). \
For a live example you can follow this [video](https://www.youtube.com/watch?v=4EqysCR3mjo&t=1255s) by [takacsmark](https://www.youtube.com/channel/UCNaxXS9VOYKyVbT--ctbHEA).

On a side Note: Docker compose only allows you to use within the local machine. How about across several servers. For that, you need to read up on [docker swarm](https://www.youtube.com/watch?v=3-7gZS4ePak).

<!-- <end> Docker Compose -->
------------------------------------------------



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


<