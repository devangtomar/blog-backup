---
title: "Colima (Containers on Linux on Mac) 🐳"
datePublished: Sun Jul 31 2022 04:32:57 GMT+0000 (Coordinated Universal Time)
cuid: cl7c6ex2v097caznv4rzhdgap
slug: colima-containers-on-linux-on-mac-f6396c27e39b
canonical: https://medium.com/@devangtomar123/colima-containers-on-linux-on-mac-f6396c27e39b
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1661621287620/hXRLeEz9J.png
tags: docker, devops, docker-images, colima, docker-desktop

---

### What is Colima? 🤔

Colima is built on Lima, which generates a QEMU VM with an HVF accelerator and handles port forwarding and folder sharing. Lima has ***containerd*** and ***nerdctl***, but a Docker container runtime is necessary for a drop-in replacement, which is what Colima is for.

Colima installs the Docker container runtime in a Lima virtual machine, configures the Docker CLI on macOS, and handles port forwarding and volume mounts. Docker, like Docker Desktop, is now simply accessible on macOS without any settings.

It’s a command line program that builds on top of lima to give a more convenient and full Docker Desktop alternative, and it already shows a lot of potential. Getting started with Colima is very simple as long as you already have [brew](https://brew.sh/) and [Xcode](https://developer.apple.com/xcode/) command line tools installed.

### GitHub Repository link 🔐

> [*https://github.com/abiosoft/colima*](https://github.com/abiosoft/colima)

### Intro GIF 📌

![Colima GIDF](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621271123/Tp_qx_r1e.gif align="left")

### Installation and Setup ⚙️

Installation is easy and can be done through Homebrew:

`brew install colima`

![Installing Colima](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621274844/60lycFePx.png align="left")

To start the VM we run:

`colima start`

![Colima start](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621277634/N9qK9w0_d.png align="left")

![Docker run](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621281080/y_29XGRpa.png align="left")

It will start the docker daemon in the VM and configure the docker CLI on the host. The usage in macOS is no different from Docker Desktop, and all `docker` commands should work as before.

### Features 💯

* Intel and M1 Macs support
    
* Simple CLI interface
    
* Docker and Containerd support
    
* Port Forwarding
    
* Volume mounts
    
* Kubernetes
    

### Changing VM size 🛐

The default VM may be on a tiny side, especially if you opt to run Kubernetes as well.

To give your VM greater resources, use

`colima stop`

followed by

`colima start — cpu 6 — memory 6.`

This will provide your **Colima VM 6 CPU cores and 6GB of RAM**. You can get a full list of options by simply running `colima` and pressing enter.

> More about that here : [https://github.com/abiosoft/colima#customizing-the-vm](https://github.com/abiosoft/colima#customizing-the-vm)

### Kubernetes ☸️

**kubectl** is required for Kubernetes. Installable with

`brew install kubectl`

To enable Kubernetes, start Colima with `--with-kubernetes` flag.

`colima start --with-kubernetes`

### More Usage options 📜

`colima --help`

![Colima help menu](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621285145/YigEy-LFL.png align="left")

### Conclusion 💁🏻‍♂️

When I ran docker containers, I didn’t detect any difference, and all docker commands functioned as before, which is excellent because none of my build scripts had to be altered.

This is a fairly young initiative with a lot of potential. A lot is happening, and the option to construct alternative Colima VMs that operate on different architectures is now in the code base. You may, for example, run arm64 Docker images on your amd64-based Mac or vice versa.

Colima is a young but promising project that can easily replace Docker Desktop, and if you are a Docker user, I highly recommend giving it a try and offering input if you so choose. It is capable of running Docker containers, docker-compose-based programs, Kubernetes, and building images.

Please share your opinions about Podman and this topic in the comments section.

### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on [Dev.to](http://Dev.to): [devangtomar](https://dev.to/devangtomar)