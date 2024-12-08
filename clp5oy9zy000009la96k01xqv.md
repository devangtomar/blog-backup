---
title: "Beginners Guide to Argo CD 🐙"
datePublished: Sun Dec 18 2022 14:11:58 GMT+0000 (Coordinated Universal Time)
cuid: clp5oy9zy000009la96k01xqv
slug: argo-cd-for-beginners-7ccc8e2e5d4f
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700411241823/f1848723-b2e7-4c0e-b91d-017a6bc211fe.png

---

> Learn, Implement and Share about Argo CD after this article read. 💭

Before we get started with Argo CD, we’ll go through what it is, how it works, and what qualifications you’ll need.

### What exactly is Argo CD ? 🤔

Argo CD is a continuous deployment (CD) solution for Kubernetes. Unlike external CD solutions, which only support push-based deployments, Argo CD can extract updated code from Git repositories and publish it to Kubernetes resources directly. It allows developers to handle infrastructure settings as well as application upgrades in a single system.

In a nutshell, Argo CD is a GitOps agent that keeps a cluster in the appropriate condition.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411202601/1500c029-89cf-497f-bcdd-bd517eb55968.png)

Let me clarify 🤔. Assume you created an application and want it to run on a cluster with three Pods and two Services for external IPs. This is the intended state, and whenever changes occur in your application’s repository, or if your desired state is not available in that cluster at any time, you must manually check and make changes to the cluster to have your desired state operating. And here comes Argo CD to automate the entire process using GitOps concepts, with Git serving as the application and cluster’s state.

### How does Argo CD work ? 💪🏻

It’s simple: there will be two repositories, one containing the application you create and the other containing the cluster’s declaratively expressed desired state. Argo CD, as a Kubernetes controller, can be installed in the same cluster as our application, or it can perform its functions from a different cluster. If the present state of the running cluster does not match the written desired state, Argo CD will attempt to create the required state and synchronise everything.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411204833/6eacb0f2-a07f-41ea-8e37-21d21c9430c3.jpeg)

For a better understanding of its architecture, visit [Argo CD Documentation](https://argo-cd.readthedocs.io/en/stable/operator-manual/architecture/).

When Argo CD determines that the live and desired states are not in sync, it displays `OutOfSync` in its UI (yes, it has a UI as well as a CLI, whichever you like). If it matches, all is fine, and the status returns Synced.

It is compatible with simple Kubernetes manifests, Helm charts, Kustomize definitions, and other templating mechanisms.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411206334/bd635119-e8c3-491f-aec6-73e9960ee5b3.png)

Argo CD checks our repository for changes every 3 minutes by default. If anything changes in our repository, Argo CD will update our cluster with the new modifications. But if we want Argo CD to look for changes every second, we can do that as well. If you don’t like this mechanism of checking for changes, you can use [webhooks](https://docs.github.com/en/developers/webhooks-and-events/webhooks/about-webhooks), in which Argo CD receives notifications from your git provider and looks for changes when it receives a notification from your application’s repo.

### Prerequisites 🐣

*   Basic knowledge of Git, K8s, and [Networking](https://www.youtube.com/watch?v=IPvYjXCsTg8&list=PL9gnSGHSqcnoqBXdMwUTRod4Gi3eac2Ak&index=3).
*   **Tools** — [kubectl](https://kubernetes.io/docs/reference/kubectl/), [minikube](https://minikube.sigs.k8s.io/docs/start/) (*optional*), [docker](https://docs.docker.com/get-started/overview/) (*optional*).

Here are some resources to help you with the above :

[**These command line tricks will help you expedite your Kubernetes tasks 🏃🏻‍♂️💨**  
*The most crucial Kubernetes command-line tool, kubectl, enables you to execute commands against clusters. You control…*devangtomar.medium.com](https://devangtomar.medium.com/these-command-line-tricks-will-help-you-expedite-your-kubernetes-tasks-%EF%B8%8F-9db8cf1049d5 "https://devangtomar.medium.com/these-command-line-tricks-will-help-you-expedite-your-kubernetes-tasks-%EF%B8%8F-9db8cf1049d5")[](https://devangtomar.medium.com/these-command-line-tricks-will-help-you-expedite-your-kubernetes-tasks-%EF%B8%8F-9db8cf1049d5)

[**Kubernetes for Dummies, yes literally! ⚓**  
*Kubernetes, an often coupled technology with Docker, was something I wanted to write about after receiving a lot of…*devangtomar.medium.com](https://devangtomar.medium.com/kubernetes-for-dummies-yes-literally-2734cf1a2291 "https://devangtomar.medium.com/kubernetes-for-dummies-yes-literally-2734cf1a2291")[](https://devangtomar.medium.com/kubernetes-for-dummies-yes-literally-2734cf1a2291)

[**Docker for rookies 🐳**  
*One of those services you may have never used but always hear about is Docker. Prior to my investigation into the…*devangtomar.medium.com](https://devangtomar.medium.com/how-to-get-started-with-docker-b2d924cbe9bb "https://devangtomar.medium.com/how-to-get-started-with-docker-b2d924cbe9bb")[](https://devangtomar.medium.com/how-to-get-started-with-docker-b2d924cbe9bb)

### Implementation of Argo CD 🚧

Deploy a Docker application in a Kubernetes cluster that is stated declaratively in plain Kubernetes manifest files in a Github repo.

#### Installation of Argo CD ⚙️

Argo CD can be used to deploy and administer other apps, but it is also an application in its own right. There are numerous methods for installing it on a Kubernetes cluster.

You can deploy Argo CD directly using the manifest for the experiment.

kubectl create namespace argocd  
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

We recommend utilising [Autopilot](https://github.com/argoproj-labs/argocd-autopilot) a companion project that not only installs Argo CD but also commits all configuration to git so Argo CD can maintain itself using GitOps.

The manifests directory provides several modes of installation with or without High Availability for more traditional installation options. The “namespace” installs allow you to install Argo CD on a specific namespace without requiring cluster-wide rights. This is useful when you want Argo CD to be installed on one cluster but manage other external clusters.

To see all resources created by Argo CD :

kubectl get all \-n argocd

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411208666/efe21f6c-2521-459c-b0bb-d83121f0ba7a.png)

#### Expose Argo CD UI 🌍🌐

Argo CD is only accessible from within the cluster by default. You can expose the UI using any of the standard Kubernetes networking techniques, such as -

*   Ingress (recommended for production) (recommended for production)
*   Load balancing device (affects cloud cost)
*   NodePort (basic but not very flexible) (simple but not very flexible)

When the external URL is complete, you must decide how users will access the Argo CD UI. There are two main approaches:

*   Make use of a limited number of local users. Argo CD is in charge of authentication. Ideal for very small businesses (e.g. 2–5 people).
*   Make use of an SSO provider. The supplier handles authentication. Perfect for businesses and large groups.

In order to expose using Ingress,

kubectl port-forward svc/argocd-server -n argocd 8085:443

Now, go to [localhost:8085](https://localhost:8085/) to access the Argo CD UI.

For the administrator’s username and password, Open a new terminal window and type :

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath=”{.data.password}” | base64 -d > admin-pass.txt

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411210338/7be3c510-ba53-443c-bbe2-4865f6212aa6.png)

Log in to the “admin” account now :

> Note : Password inside the file admin-pass.txt

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411212020/b73595da-d676-47e9-91c6-2168774e7db0.png)

#### Creating and Syncing Application in Argo CD 🗣️🦜

In Argo CD, an application can be created via the UI, CLI, or by generating a Kubernetes manifest, which can then be passed to kubectl to create resources.

Using UI

*   Click on “NEW APP”

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411213763/fe6cc6fd-4981-4bbe-84f8-0250beb5e21c.png)

*   **Put only necessaries as mentioned below :**

General  
Application Name: `demo-app  
`Project Name: `default`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411215031/2c452fb9-b499-4431-a57f-ca6e46eca62a.png)

*   **Source :**

Repository URL: `[https://github.com/devangtomar/Sample-GO-WebApp](https://github.com/sarkartanmay393/Sample-GO-WebApp)  
`Revision: `HEAD  
`PATH: `.`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411216382/f1ca5ed3-1ec4-48fd-a185-2b3983792766.png)

*   **Destination :**

Cluster URL: `[https://kubernetes.default.svc](https://kubernetes.default.svc)  
`namespace: `default`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411218362/11850719-d9f3-4dc4-82f7-44b2ae66d73c.png)

**YAML file**

apiVersion: argoproj.io/v1alpha1  
kind: Application  
metadata:  
  name: demo-app  
spec:  
  destination:  
    name: ''  
    namespace: default  
    server: 'https://kubernetes.default.svc'  
  source:  
    path: .  
    repoURL: 'https://github.com/devangtomar/sample-go-webapp.git'  
    targetRevision: HEAD  
  project: default

Check your YAML by hitting `EDIT AS YAML` and try to understand.

Now, Press on `Create` and You will see this on screen.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411220049/317b2363-373a-4823-a519-08bdbe692aa3.png)

Now, click on `SYNC` and Proceed without any change.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411221968/94f6abbe-041b-4df3-8026-4ec0a49d683f.png)

#### Using CLI 🎹

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411223881/575a9f9c-b515-4fff-9069-e891d1bb4a08.jpeg)

*   **Install Argo CD CLI ⚙️**

Run the following command -

**For Linux :**

curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64  
chmod +x /usr/local/bin/argocd

**For Windows :**

Replace `$version` in the command below with the version of Argo CD you would like to download :

$url = "https://github.com/argoproj/argo-cd/releases/download/" + $version + "/argocd-windows-amd64.exe"  
$output = "argocd.exe"  
Invoke-WebRequest -Uri $url -OutFile $output

**For Mac :**

brew install argocd

Argo CD CLI help screen :

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411225766/0665e072-134f-4fff-b171-ca9c1395a068.png)

*   **Login Argo CD CLI 🧑🏻‍💻**

Run the command :

argocd login localhost:8085

Then continue with `y` and, Username: `admin` Password: `check your admin-pass.txt`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411227530/305927f6-3798-4a38-ba69-55baeb2466a4.png)

*   **Create an app in CLI 🤳🏻**

Run the following command :

argocd app create demo-app \--project default \--repo https://github.com/devangtomar/sample-go-webap --path . --dest-namespace default --dest-server https://kubernetes.default.svc

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411229216/b169f329-9f7e-420c-a0bb-f499747056d8.png)

*   **Sync app in CLI 🌐**

Because this app is new, the default sync state will be `OutOfSync`. Run the command — to perform synchronization.

argocd app sync demo-app

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411230918/b341b4d9-b9e0-43f5-85ee-e162e769f114.png)

The deployed application has now been synchronized.

In the Argo CD User Interface, this will be the final display of our deployed application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411233335/d03ccda6-66a8-4170-ae3f-979bf2603dfd.png)

*   **Access the Deployed App 🏗️**

Now look for services that are operating under the default namespace in k8s. Execute the command :

kubectl get services

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411235490/06ebfaaa-3bdd-409f-a2a5-4d5cc7973cf3.png)

You need to port forward the `sample-service` to access the app. Run the command :

kubectl port-forward svc/sample-service 8086:8080

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411237038/57c0b905-c9a9-4c66-bd4f-87d1f0eab6fd.png)

Now, visit [localhost:8086](http://localhost:8086/) to see.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411238664/76fa496e-b66e-4bcd-bdbf-dc0f5d0c8f3d.png)

This is the Argo CD For Dummies article. I hope you learned something new. See you in my next post.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700411240031/b467010c-434f-4f5b-9410-ae3bfe69770f.jpeg)

### GitHub repo for the sample GO webapp💻

[**GitHub - devangtomar/sample-go-webapp**  
*You can't perform that action at this time. You signed in with another tab or window. You signed out in another tab or…*github.com](https://github.com/devangtomar/sample-go-webapp "https://github.com/devangtomar/sample-go-webapp")[](https://github.com/devangtomar/sample-go-webapp)

#### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on Dev.to: [devangtomar](https://dev.to/devangtomar)