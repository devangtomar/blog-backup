---
title: "Beginners Guide to Argo CD 🐙"
datePublished: Sun Dec 18 2022 14:11:58 GMT+0000 (Coordinated Universal Time)
cuid: clbtgyj6m02c7n5nvatcj5td9
slug: argo-cd-for-beginners
canonical: https://devangtomar.medium.com/argo-cd-for-beginners-7ccc8e2e5d4f
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1671374052304/koSJsONDg.png
tags: kubernetes, gitops, devops-articles, argocd, argo

---

> Learn, Implement and Share about Argo CD after this article read. 💭

Before we get started with Argo CD, we’ll go through what it is, how it works, and what qualifications you’ll need.

### What exactly is Argo CD? 🤔

Argo CD is a continuous deployment (CD) solution for Kubernetes. Unlike external CD solutions, which only support push-based deployments, Argo CD can extract updated code from Git repositories and publish it to Kubernetes resources directly. It allows developers to handle infrastructure settings as well as application upgrades in a single system.

In a nutshell, Argo CD is a GitOps agent that keeps a cluster in the appropriate condition.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374012752/mGlcl5qEJj.png align="left")

Let me clarify 🤔. Assume you created an application and want it to run on a cluster with three Pods and two Services for external IPs. This is the intended state, and whenever changes occur in your application’s repository, or if your desired state is not available in that cluster at any time, you must manually check and make changes to the cluster to have your desired state operating. And here comes Argo CD to automate the entire process using GitOps concepts, with Git serving as the application and cluster’s state.

### How does Argo CD work? 💪🏻

It’s simple: there will be two repositories, one containing the application you create and the other containing the cluster’s declaratively expressed desired state. Argo CD, as a Kubernetes controller, can be installed in the same cluster as our application, or it can perform its functions from a different cluster. If the present state of the running cluster does not match the written desired state, Argo CD will attempt to create the required state and synchronise everything.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374015073/9k7E-4hZlI.jpeg align="left")

For a better understanding of its architecture, visit [Argo CD Documentation](https://argo-cd.readthedocs.io/en/stable/operator-manual/architecture/).

When Argo CD determines that the live and desired states are not in sync, it displays `OutOfSync` in its UI (yes, it has a UI as well as a CLI, whichever you like). If it matches, all is fine, and the status returns Synced.

It is compatible with simple Kubernetes manifests, Helm charts, Kustomize definitions, and other templating mechanisms.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374016927/MKNiPx6Pu.png align="left")

Argo CD checks our repository for changes every 3 minutes by default. If anything changes in our repository, Argo CD will update our cluster with the new modifications. But if we want Argo CD to look for changes every second, we can do that as well. If you don’t like this mechanism of checking for changes, you can use [webhooks](https://docs.github.com/en/developers/webhooks-and-events/webhooks/about-webhooks), in which Argo CD receives notifications from your git provider and looks for changes when it receives a notification from your application’s repo.

### Prerequisites **🐣**

* Basic knowledge of Git, K8s, and [Networking](https://www.youtube.com/watch?v=IPvYjXCsTg8&list=PL9gnSGHSqcnoqBXdMwUTRod4Gi3eac2Ak&index=3).
    
* **Tools** — [kubectl](https://kubernetes.io/docs/reference/kubectl/), [minikube](https://minikube.sigs.k8s.io/docs/start/) (*optional*), [docker](https://docs.docker.com/get-started/overview/) (*optional*).
    

Here are some resources to help you with the above :

%[https://devangtomar.hashnode.dev/how-to-get-started-with-docker-b2d924cbe9bb] 

%[https://devangtomar.hashnode.dev/kubernetes-for-dummies-yes-literally-2734cf1a2291] 

%[https://devangtomar.hashnode.dev/these-command-line-tricks-will-help-you-expedite-your-kubernetes-tasks-efb88f-9db8cf1049d5] 

### Implementation of Argo CD **🚧**

Deploy a Docker application in a Kubernetes cluster that is stated declaratively in plain Kubernetes manifest files in a GitHub repo.

#### Installation of Argo CD **⚙️**

Argo CD can be used to deploy and administer other apps, but it is also an application in its own right. There are numerous methods for installing it on a Kubernetes cluster.

You can deploy Argo CD directly using the manifest for the experiment.

```plaintext
# for creating the namespace
kubectl create namespace argocd

# for deploying argocd on above namespace
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

I recommend utilising [Autopilot](https://github.com/argoproj-labs/argocd-autopilot) a companion project that not only installs Argo CD but also commits all configurations to git so Argo CD can maintain itself using GitOps.

The manifests directory provides several modes of installation with or without High Availability for more traditional installation options. The “namespace” installs allow you to install Argo CD on a specific namespace without requiring cluster-wide rights. This is useful when you want Argo CD to be installed on one cluster but manage other external clusters.

To see all resources created by Argo CD :

```plaintext
# for fetching all pods, services, replicaset, deployments etc.
kubectl get all -n argocd
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374019293/HWvX3l46f.png align="left")

#### Expose Argo CD UI **🌍🌐**

Argo CD is only accessible from within the cluster by default. You can expose the UI using any of the standard Kubernetes networking techniques, such as -

* Ingress (recommended for production) (recommended for production)
    
* Load balancing device (affects cloud cost)
    
* NodePort (basic but not very flexible) (simple but not very flexible)
    

When the external URL is complete, you must decide how users will access the Argo CD UI. There are two main approaches:

* Make use of a limited number of local users. Argo CD is in charge of authentication. Ideal for very small businesses (e.g. 2–5 people).
    
* Make use of an SSO provider. The supplier handles authentication. Perfect for businesses and large groups.
    

To expose using Ingress,

```plaintext
# for port forwarding
kubectl port-forward svc/argocd-server -n argocd 8085:443
```

Now, go to [localhost:8085](https://localhost:8085/) to access the Argo CD UI.

For the administrator’s username and password, Open a new terminal window and type :

```plaintext
# for configuring k8s secrets in a file.
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath=”{.data.password}” | base64 -d > admin-pass.txt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374021412/Ek6-5iSdH.png align="left")

Log in to the “admin” account now :

> **Note:** Password inside the file admin-pass.txt

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374024072/oE9PjnolH.png align="left")

#### Creating and Syncing Application in Argo CD **🗣️🦜**

In Argo CD, an application can be created via the UI, CLI, or by generating a Kubernetes manifest, which can then be passed to kubectl to create resources.

Using UI

* Click on “NEW APP”
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374025832/540YK66N8.png align="left")

Put only necessaries as mentioned below :

* General :
    
    Application Name: `demo-app`
    
    Project Name: `default`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374027127/4wbfqQTi1.png align="left")

* **Source :**
    

Repository URL: `[https://github.com/devangtomar/Sample-GO-WebApp](https://github.com/sarkartanmay393/Sample-GO-WebApp)` Revision: `HEAD` PATH: `.`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374028989/D8i5236dZ.png align="left")

* **Destination :**
    

Cluster URL: `[https://kubernetes.default.svc](https://kubernetes.default.svc)` namespace: `default`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374030422/hH9QB2vqe.png align="left")

**YAML file**

```yaml
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
```

Check your YAML by hitting `EDIT AS YAML` and try to understand.

Now, Press on `Create` and You will see this on the screen.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374032123/Xe_hMXhsC.png align="left")

Now, click on `SYNC` and Proceed without any change.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374033933/1C80HBtEv.png align="left")

#### Using CLI 🎹

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374035291/yj_10yNnd.jpeg align="left")

* **Install Argo CD CLI ⚙️**
    

Run the following command -

For Linux :

```bash
curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
chmod +x /usr/local/bin/argocd
```

**For Windows :**

Replace `$version` in the command below with the version of Argo CD you would like to download :

```bash
$url = "https://github.com/argoproj/argo-cd/releases/download/" + $version + "/argocd-windows-amd64.exe"
$output = "argocd.exe"
Invoke-WebRequest -Uri $url -OutFile $output
```

For Mac :

```bash
brew install argocd
```

Argo CD CLI help screen :

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374037029/rQlDQ_TTq.png align="left")

* **Login Argo CD CLI 🧑🏻‍💻**
    

Run the command :

```bash
argocd login localhost:8085
```

Then continue with `y` and, Username: `admin` Password: `check your admin-pass.txt`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374038950/FdBOHBzF1.png align="left")

* **Create an app in CLI 🤳🏻**
    

Run the following command :

```bash
argocd app create demo-app --project default --repo https://github.com/devangtomar/sample-go-webapp --path . --dest-namespace default --dest-server https://kubernetes.default.svc
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374040440/aVQeWQmwU.png align="left")

* **Sync app in CLI 🌐**
    

Because this app is new, the default sync state will be `OutOfSync`. Run the command — to perform synchronization.

```bash
argocd app sync demo-app
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374042379/OHN1EFVrb.png align="left")

The deployed application has now been synchronized.

In the Argo CD User Interface, this will be the final display of our deployed application.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374044378/XnBj_ZMDI.png align="left")

* **Access the Deployed App 🏗️**
    

Now look for services that are operating under the default namespace in k8s. Execute the command :

```bash
kubectl get services
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374045902/AAcvXIL92.png align="left")

You need to port forward the `sample-service` to access the app. Run the command :

```bash
kubectl port-forward svc/sample-service 8086:8080
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374047321/rTLZ7K1v-.png align="left")

Now, visit [localhost:8086](http://localhost:8086/) to see.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374048720/Rh8EBh7so.png align="left")

This is the Argo CD For Dummies article. I hope you learned something new. See you in my next post.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374050509/OiQ3rfed4.jpeg align="left")

### GitHub repo for the sample GO webapp💻

%[https://github.com/devangtomar/sample-go-webapp] 

### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on [Dev.to](http://Dev.to): [devangtomar](https://dev.to/devangtomar)