---
title: "Mastering Dockerfile ️🐳: 10 Advanced Tips and Best Practices ⚔"
seoTitle: "Mastering Dockerfile ️🐳: 10 Advanced Tips and Best Practices ⚔"
seoDescription: "Dockerfile is a robust tool that empowers developers to create and deploy applications within Docker containers."
datePublished: Sat Sep 02 2023 06:44:24 GMT+0000 (Coordinated Universal Time)
cuid: clm1pyo4a01x674nvdhl9f6kq
slug: mastering-dockerfile-efb88f-10-advanced-tips-and-best-practices-ea6ea3162d8c
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693640729187/48c347a0-34dd-435a-9193-ab504a32c219.jpeg
tags: best-practices, dockerfile, docker-compose, devops-articles, multi-stage-docker-file

---

Dockerfile is a robust tool that empowers developers to create and deploy applications within Docker containers. While many developers are acquainted with the fundamentals of Dockerfile, there exists a treasure trove of advanced features and best practices that may not have yet graced your Docker repertoire.

![](https://miro.medium.com/v2/resize:fit:630/1*WxOtSjZrTjlr6D2OJlLD5A.jpeg align="left")

In this exploration, we will unearth ten lesser-known Dockerfile tricks and tips to elevate your Docker skills, optimizing your builds and streamlining your containerized applications.

#### 1. .dockerignore File: Reducing Build Context Size

A `.dockerignore` file is your secret weapon to exclude unnecessary files and directories from the build context. Shrinking the build context proves invaluable when dealing with large files or directories that need not clutter your image. [Learn more](https://docs.docker.com/engine/reference/builder/#dockerignore-file).

```javascript
# Example .dockerignore file
node_modules
*.log
```

#### 2\. COPY vs. ADD: Know the Differences

The `COPY` and `ADD` instructions may seem similar, but they harbor distinct nuances. Learn when to employ each, and why `COPY` is generally preferred according to Docker’s official documentation. [Read more](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#add-or-copy).

```javascript
# Using COPY
COPY src/ /app/
# Using ADD with tar extraction
ADD src.tar.gz /app/
```

#### 3\. Multi-Stage Builds: Streamlining for Production

Discover the power of multi-stage builds. Employ multiple `FROM` statements in a single Dockerfile to craft an environment for building your application, then efficiently copy the results into a lean, production-ready image. [More details](https://docs.docker.com/build/building/multi-stage/).

```javascript
# Stage 1: Build your golang executable
FROM golang as buildStage
WORKDIR /app
COPY . .
RUN go build -o /go/bin/myapp

# Stage 2: Run the application
FROM alpine:latest
COPY --from=buildStage /go/bin/myapp /usr/local/bin/myapp
CMD ["myapp"]
```

#### 4\. Multi-Layers and Caching: Speeding Up Builds

Docker leverages caching to expedite builds. Understand how layers, `RUN`, `COPY`, and `ADD` instructions influence caching, and when to employ techniques like chaining `RUN` commands. [Dig deeper](https://docs.docker.com/build/cache/).

```javascript
# Good practice: Chaining RUN commands
RUN yum --disablerepo=* --enablerepo="myrepo" && yum update -y && yum install nmap
```

#### 5\. ONBUILD Instruction: Automation Beyond Your Image

Explore the `ONBUILD` instruction, a nifty tool to automate tasks when your Docker image serves as the base for another image. Unearth strategies to prevent resource conflicts and optimize your workflow. [Learn more](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#onbuild).

```javascript
ONBUILD COPY . /app/src
ONBUILD RUN /build.sh
```

#### 6\. Change Your User: Enhancing Security

Improve security by modifying the default container user. Learn how to switch to a non-root user, bolstering security and reducing potential vulnerabilities. [Read about it](https://docs.docker.com/engine/reference/builder/#user).

```javascript
FROM alpine:latest

# Create a new user and switch to that user
RUN adduser -D -u 1000 appuser
USER appuser

# Set the working directory to /app
WORKDIR /app

# Copy the script to the container and make it executable
COPY script.sh .
RUN chmod +x script.sh

# Run the script
CMD ["./script.sh"]
```

#### 7\. Container Health Checks: Ensuring Reliability

Docker’s `HEALTHCHECK` instruction monitors container health. Configure checks to detect failures and automate container restarts. Ensure your applications stay robust and reliable. [Discover more](https://docs.docker.com/engine/reference/builder/#healthcheck).

```javascript
# Set the command to start the web server
CMD ["python", "app.py"]

# Add a healthcheck for the web server
HEALTHCHECK --interval=5s \\
            --timeout=5s \\
            CMD curl --fail <http://localhost:5000/health> || exit 1
```

#### 8\. Shell Form: Leveraging Shell-Specific Features

In addition to the exec form, Dockerfiles support a shell form that offers features like environment variable substitution and command chaining. Unearth the power of this form to customize your commands. [Explore it](https://docs.docker.com/engine/reference/builder/#run).

```javascript
# Using Shell Form
SHELL ["/bin/bash", "-c"]
RUN echo "This is a shell command."
```

#### 9\. Metadata Instructions: Organizing Your Images

`EXPOSE` and `LABEL` instructions provide essential metadata. Be explicit about exposed ports and utilize labels to convey image purpose, authorship, and more. [Dive into details](https://docs.docker.com/engine/reference/builder/#expose).

```javascript
FROM ubuntu:latest
LABEL maintainer="Your Name <youremail@example.com>"
LABEL description="This is a simple Dockerfile example that uses the LABEL and EXPOSE instructions."
RUN apt-get update && \\
    apt-get install -y nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

#### 10\. Docker Images: Tar File Magic

Did you know? Docker images are essentially compressed tar files with metadata. Understand how Docker packages your files, compresses them, and maintains them as an efficient `tarball`. Learn why this knowledge is essential for efficient Docker practices.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693640725531/8f98e310-3696-480c-b195-01b7deddb52e.png align="center")

#### Conclusion 💭

With a touch of finesse and these advanced Dockerfile techniques, you can bolster security, enhance readability, expedite build times, and ultimately improve your continuous integration pipeline and productivity.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693640726966/96c62035-68c4-4ac8-bcb4-ba363cdc9e78.gif align="center")

By running containers as non-root users, streamlining Dockerfiles, and using efficient build practices, you’ll not only optimize images but also create a more secure and efficient development environment. It’s time to unlock the full potential of Dockerfile and elevate your containerization game.

#### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on Dev.to: [devangtomar](https://dev.to/devangtomar)

![](https://cdn-images-1.medium.com/max/800/0*wCUcUcpsOEIO2vlF align="center")