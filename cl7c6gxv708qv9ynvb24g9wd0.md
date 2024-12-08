---
title: "Podman (An alternative to Docker !?!) 🦭"
datePublished: Sat Jul 30 2022 11:00:56 GMT+0000 (Coordinated Universal Time)
cuid: cl7c6gxv708qv9ynvb24g9wd0
slug: podman-an-alternative-to-docker-desktop-c30370edc98b
canonical: https://medium.com/@devangtomar123/podman-an-alternative-to-docker-desktop-c30370edc98b
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1661621354394/y2heDM_cb.jpeg
tags: docker, devops, alternative, podman

---

#### Exploring new tech

#### What is Podman? 🤔

![Podman logo](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621354394/y2heDM_cb.jpeg align="left")

Podman is a daemonless, open source, Linux native tool for finding, running, building, sharing, and deploying applications that use Open Containers Initiative (OCI) Containers and Container Images.

> It operates very similar to Docker and is simple to set up.

> Containers can run as root or in a rootless manner.

Documentation : [https://podman.io/](https://podman.io/)

### How different from Docker? 🐳

![Podman VS Docker](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621356180/UzyCvGA7M.jpeg align="left")

The primary distinctions between Docker and Podman (Pod Manager Tool) are as follows:

* **Daemonless** — *This characteristic distinguishes itself from Docker, which executes operations via a docker daemon. Podman is lightweight and does not require an instance to be active at all times in order to execute containers.*
    
* **Rootless** — *Podman can be operated as root or as a non-root user. We can run Podman containers as non-root users while being compatible with container running.*
    
* **Pods** — *The word Pods was coined by Kubernetes. Pods are groups of containers that run as close together as feasible. Podman includes this capability by default for running many containers concurrently.*
    

### Architecture 🏛️:

![[Architecture] Docker VS Podman](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621357724/Aulls7TgO.png align="left")

> ***Many individuals still refer to a “container” as a “Docker container.”***

This does not accurately represent the existing container ecosystem. Docker generates OCI container images that may be used with different runtimes. *Kubernetes is one such example, as is Podman.*

As a result, the essential functionality of Podman and Docker overlaps. Both generate images that may be used to run containers by the other. On top of the basic containerization functionality, the two runtimes provide their own specializations.

### Setup ⚙️

And as it’s OCI-compliant, Podman can be used as a drop-in replacement for the better-known Docker runtime. Most Docker commands can be directly translated to Podman commands.

> *Simply* ***put alias as, ‘docker=podman’*** *on your machine and you’re set*

Installation of Podman is pretty straightforward over a Mac. If you’re on other OS, follow this [documentation](https://podman.io/getting-started/installation). WSL over Windows works.

Request admin access from Self-service app and then open terminal. The Mac client is available through [Homebrew](https://brew.sh/).

`brew install podman`

![Installing podman on MacOS](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621360144/_oZnhQx-8q.png align="left")

To start the Podman-managed VM:

`podman machine init`

And then

`podman machine start`

![Starting podman machine](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621362263/XRFjIYp5B.png align="left")

Once the installation is complete, you can then verify the installation information using:

`podman info`

![podman info](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621364957/eT3S6g3Q2.png align="left")

### TLDR 📌

As stated before, Podman is just an alias for docker. Whatever commands you can execute with docker, you can execute with Podman.

#### Building an Image

`podman build -t “containername”`

#### Docker file :

![Dockerfile](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621367528/ZqaRJJE7f.png align="left")

#### Image building via the command :

`podman build`

#### Push Image

`podman push “registryname/imagename:tag”`

#### List images

`podman images`

> Command screenshot :

![podman images](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621370128/r3FrNemN0.png align="left")

#### Run container

`podman run “imagename”`

> Command screenshot :

![Podman run](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621372570/MfON-isSO.png align="left")

#### Remove image

`podman rmi imagename`

> Command screenshot :

![Podman container](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621375020/WOmGz_xTa.png align="left")

#### Show Podman process status

`podman ps -a`

> Rest of the support commands is shown as below :

![Podman help](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621381320/kgGEzVmxU.png align="left")

If you use docker-compose , there is an alternative for this [podman-compose](https://github.com/containers/podman-compose).

> ***Note :*** *Natively docker-compose is yet not supported by Podman yet at the time of my testing of Podman Release v4.0.0 version. And the one available is very unreliable.*

The setup is straightforward. Install Python if you don’t already have it, and then podman-compose.

`brew install python@3.10pip3 install podman-compose`

Podman in conjunction with podman-compose works well.

I’ve had trouble getting podman-compose over Mac because there isn’t an official document for installation other than the one mentioned above.

### Conclusion 💁🏻‍♂️

Podman wraps around Docker’s capabilities to provide a lightweight container runtime that can be used in Daemonless and Rootless modes.

### Limitations of Podman 🥲

* Linux based.
    
* No support for Windows OS based Containers. *(Supported now with the help of WSL)*
    
* Docker-Compose component is still non-reliant
    
* No GUI unlike Docker Desktop, Rancher Desktop.
    
* New product with bugs and still coming features.
    
* No Docker Swarm.
    

That being said, Podman is still a new technology that is improving, and it may be best to ‘wait and see’ until we see community acceptance of Podman and it becomes a more developed and reliable tool.

You can certainly experiment with it on your local workstations and learn more about it, but bringing it into your production system may take some time.

Please share your opinions about Podman and this topic in the comments section.

### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on [Dev.to](http://Dev.to): [devangtomar](https://dev.to/devangtomar)