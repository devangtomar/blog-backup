---
title: "TOP Docker commands (with examples) that you should know 💻"
datePublished: Fri Nov 18 2022 05:31:48 GMT+0000 (Coordinated Universal Time)
cuid: clao19f9l002jdqnv69sg2rrz
slug: top-docker-commands-with-examples-that-you-should-know-59213db0ab1e
canonical: https://medium.com/@devangtomar/top-docker-commands-with-examples-that-you-should-know-59213db0ab1e
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1668868573722/3d5l7U_fOh.jpeg

---

Docker is an open platform for app development, shipping, and running. Docker allows you to decouple your apps from your infrastructure, allowing you to release software more quickly. Docker allows you to package and run an application in a container, which is a loosely isolated environment. The Docker container trend is unstoppable, with firms actively seeking people that are well-versed in Docker commands.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668868559266/CdyhfF1HVv.jpeg align="left")

### 1\. Docker Registries & Repositories

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668868560783/iWlbc72tmE.jpeg align="left")

#### **Login to a Registry**

`docker login`

`docker login localhost:8080`

#### **Logout from a Registry**

`docker logout`

`docker logout localhost:8080`

#### **Searching an Image**

`docker search nginx`

`docker search \--filter stars=3 --no-trunc nginx`

#### **Pulling an Image**

`docker image pull nginx`

`docker image pull devangtomar/nginx localhost:5000/myadmin/nginx`

#### **Pushing an Image**

`docker image push devangtomar/nginx`

`docker image push devangtomar/nginx localhost:5000/myadmin/nginx`

### 2\. Running Containers

#### **Create and Run a Simple Container**

Start an ubuntu:latest image

> \* Bind the port 80 from the CONTAINER to port 3000 on the HOST

> \* Mount the current directory to /data on the CONTAINER

> **\* Note :** on windows you have to change -v ${PWD}:/data to -v “C:\\Data”:/data

`docker container run — name infinite -it -p 3000:80 -v ${PWD}:/data ubuntu:latest`

#### Creating a Container

`docker container create -t -i devangtomar/infinite — name infinite`

#### Running a Container

`docker container run -it — name infinite -d devangtomar/infinite`

#### Renaming a Container

`docker container rename infinite infinity`

#### Removing a Container

`docker container rm infinite`

A container can be removed only after stopping it using docker stop command. To avoid this, add the — rm flag while running the container.

#### Updating a Container

`docker container update — cpu\-shares 512 \-m 300M infinite`

#### Running a command within a running container

`docker exec -it infinite sh`

In the example above, bash can replace sh as an alternative (if the above is giving an error).

### 3\. Starting & Stopping Containers

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668868562559/BuaBJ7Vuu.jpeg align="left")

#### Starting

`docker container start nginx`

#### Stopping

`docker container stop nginx`

#### Restarting

\`docker container restart nginx

#### Pausing

`docker container pause nginx`

#### Unpausing

`docker container unpause nginx`

#### Blocking a Container

`docker container wait nginx`

#### Sending a SIGKILL

`docker container kill nginx`

#### Sending another signal

`docker container kill -s HUP nginx`

#### Connecting to an Existing Container

`docker container attach nginx`

### 4\. Getting Information about Containers

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668868564164/QTcPT8r3g.jpeg align="left")

#### From Running Containers

Shortest way :

`docker ps`

Alternative :

`docker container ls`

#### From All containers.

`docker ps -a`

`docker container ls -a`

#### Container Logs

`docker logs infinite`

#### ‘tail -f’ Containers’ Logs

`docker container logs infinite -f`

#### Inspecting Containers

`docker container inspect infinite`

`docker container inspect \--format ‘{{ .NetworkSettings.IPAddress }}’ $(docker ps -q)`

#### Containers Events

`docker system events infinite`

#### Public Ports

`docker container port infinite`

#### Running Processes

`docker container top infinite`

#### Container Resource Usage

`docker container stats infinite`

#### Inspecting changes to files or directories on a container’s filesystem

`docker container diff infinite`

### 5\. Managing Images

#### Listing Images

`docker image ls`

#### Building Images

From a Dockerfile in the Current Directory

`docker build .`

From a Remote GIT Repository

`docker build github.com/creack/docker-firefox`

#### Instead of Specifying a Context, You Can Pass a Single Dockerfile in the URL or Pipe the File in via STDIN

`docker build - < Dockerfile`

`docker build \- < context.tar.gz`

#### Building and Tagging

`docker build -t devangtomar/infinite .`

#### Building a Dockerfile while Specifying the Build Context

`docker build -f myOtherDockerfile .`

#### Building from a Remote Dockerfile URI

`curl example.com/remote/Dockerfile | docker build -f — .`

#### Removing an Image

`docker image rm nginx`

#### Loading a Tarred Repository from a File or the Standard Input Stream

`docker image load < ubuntu.tar.gz`

`docker image load \--input ubuntu.tar`

#### Saving an Image to a Tar Archive

`docker image save busybox > ubuntu.tar`

#### Showing the History of an Image

`docker image history`

#### Creating an Image From a Container

`docker container commit nginx`

#### Tagging an Image

`docker image tag nginx devangtomar/nginx`

#### Pushing an Image

`docker image push devangtomar/nginx`

### 6\. Networking

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668868569982/ZgaTIhwkK.jpeg align="left")

#### Creating Networks

* Creating an Overlay Network
    

`docker network create -d overlay MyOverlayNetwork`

* Creating a Bridge Network
    

`docker network create -d bridge MyBridgeNetwork`

* Creating a Customized Overlay Network
    

`docker network create -d overlay —-subnet=192.168.0.0/16 -subnet=192.170.0.0/16 --gateway=192.168.0.100 --gateway=192.170.0.100 -- ip-range=192.168.1.0/24 --aux-address=”my-router=192.168.1.5" --aux-address=”my-switch=192.168.1.6" --aux-address=”my-printer=192.170.1.5" --aux-address=”my-nas=192.170.1.6" MyOverlayNetwork`

#### Removing a Network

`docker network rm MyOverlayNetwork`

#### Listing Networks

`docker network ls`

#### Getting Information About a Network

`docker network inspect MyOverlayNetwork`

#### Connecting a Running Container to a Network

`docker network connect MyOverlayNetwork nginx`

#### Connecting a Container to a Network When it Starts

`docker container run -it -d — network=MyOverlayNetwork nginx`

#### Disconnecting a Container from a Network

`docker network disconnect MyOverlayNetwork nginx`

#### Exposing Ports

Using Dockerfile, you can expose a port on the container using :

`EXPOSE <port\_number\>`

You can also map the container port to a host port using :

`docker run -p $HOST\_PORT:$CONTAINER\_PORT — name -t <image>`

e.g.

`docker run -p $HOST\_PORT:$CONTAINER\_PORT — name infinite -t infinite`

### 7\. Security

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1668868571615/pLRlcm6cA.jpeg align="left")

#### Guidelines for Building Secure Docker Images

1. Prefer minimal base images
    
2. Dedicated user on the image as the least privileged user
    
3. Sign and verify images to mitigate MITM attacks
    
4. Find, fix and monitor for open source vulnerabilities
    
5. Don’t leak sensitive information to docker images
    
6. Use fixed tags for immutability
    
7. Use COPY instead of ADD
    
8. Use labels for metadata
    
9. Use multi-stage builds for small secure images
    
10. Use a linter
    

### 8\. Cleaning Docker

#### Removing a Running Container

`docker container rm nginx`

#### Removing a Container and its Volume

`docker container rm -v nginx`

#### Removing all Exited Containers

`docker container rm $(docker container ls -a -f status=exited -q)`

#### Removing All Stopped Containers

`docker container rm \`docker container ls -a -q\`\`

#### Removing a Docker Image

`docker image rm nginx`

#### Removing Dangling Images

`docker image rm $(docker image ls -f dangling=true -q)`

#### Removing all Images

`docker image rm $(docker image ls -a -q)`

#### Removing all Untagged Images

`docker image rm -f $(docker image ls | grep “^” | awk “{print $3}”)`

#### Stopping & Removing all Containers

`docker container stop $(docker container ls -a -q) && docker container rm $(docker container ls -a -q)`

#### Removing Dangling Volumes

`docker volume rm $(docker volume ls -f dangling=true -q)`

#### Removing all unused (containers, images, networks and volumes)

`docker system prune -f`

#### Clean all

`docker system prune -a`

### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on [Dev.to](http://Dev.to): [devangtomar](https://dev.to/devangtomar)