---
title: "Unleashing the Full Potential of GitHub Actions: A Beginner’s Guide 🚀"
datePublished: Fri Mar 31 2023 07:06:01 GMT+0000 (Coordinated Universal Time)
cuid: clfy8mxo305ku7vnv4hmqer6d
slug: unleashing-the-full-potential-of-github-actions-a-beginners-guide-2674f47db22a
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680369535116/c3c81631-d115-4b72-8b8d-5467f706e533.png
tags: introduction, github, github-actions, githubpages, githubaction

---

I just recently started using GitHub Actions, and I’m blown away by what it’s capable of. Simply put, GitHub Actions facilitates the creation of workflows within the GitHub code repository. This is not limited to a CI/CD pipeline; you can also create a variety of automation tasks such as automatically labelling issues when they are created, linting code with each pull request, and notifying a Slack channel when a package is updated in the GitHub registry.

We’ll examine the core elements of GitHub Actions in this article so you Day use them with confidence in your repositories.

### How can an action file be edited? 📝

It’s crucial to prepare your tools before starting. I’d strongly advise using [VS Code](https://code.visualstudio.com/) to change the workflow file for your GitHub actions. Installing this [VS Code addon](https://marketplace.visualstudio.com/items?itemName=me-dutour-mathieu.vscode-github-actions) also adds real-time code linting and IntelliSense.

Let’s start now that that is out of the way.

### Introduction 👶🏻

GitHub Actions is a powerful tool that allows you to automate various tasks in your software development workflow. It enables you to define workflows using YAML syntax and execute them automatically whenever an event occurs, such as a pull request, push to the repository, or a scheduled time.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680369526423/656c7535-dd6a-4f19-83a5-090529b96078.jpeg align="left")

In this article, we will cover the fundamentals of GitHub Actions, including its syntax, components, and best practices. We’ll also provide numerous code examples to make it easy for you to understand how to use GitHub Actions effectively. But before we dive into the technical details, let’s have some fun and imagine GitHub Actions as a person!

### How to get started? ⭐

Add a YAML file to your repository’s `.github/workflows` directory to build a GitHub Actions workflow file. One workflow file or several workflow files may exist in this directory. Depending on the trigger event you’ve selected, each process will execute.

You can give your GitHub Actions workflow file any name you wish, although I wouldn’t suggest calling it `action.yml`. The reason is that when you create a custom action for usage by others, you must provide a [metadata file](https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions) with the name `action.yml` (or `action.yaml`) and a slightly different syntax from standard workflow files. If the file is called `action.yml`, the VS Code extension listed above verifies the syntax of this metadata file (or `.yaml`). So, it’s recommended to rename your workflow file to minimize code linting conflicts.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680369527775/e154d241-dd74-4b2f-aaa2-00e62cc801e4.jpeg align="left")

> I used two distinct YAML file extensions above, as you may have observed. This is due to the fact that both `build.yml` and `build.yaml` are legitimate filenames.

While we’re talking about names, your workflow is given a suitable name using the `name` keyword in the YAML file. You may wish to write this as the first line of code in your workflow file.

name: Build & deploy

Adding this term would improve readability even though it is optional because the GitHub Actions UI uses this value.

### GitHub Actions Syntax 🎬

Now that you’ve met Git and some of his team members, let’s dive into the syntax of GitHub Actions.

GitHub Actions is defined using YAML syntax, which stands for “YAML Ain’t Markup Language.” YAML is a human-readable data serialization language that is often used for configuration files.

Here’s an example of a basic GitHub Actions workflow :

```yaml
name: My Workflow

on:
  push:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v2
    - name: Build code
      run: make build
    - name: Test code
      run: make test
```

Let’s break down the syntax of this workflow:

* `name`: The name of your workflow, which is displayed in the Actions tab.
    
* `on`: The event that triggers your workflow. In this example, the workflow is triggered when someone pushes code to the main branch.
    
* `jobs`: The tasks that you want to run when your workflow is triggered.
    
* `build`: The name of your job.
    
* `runs-on`: The type of virtual machine that your job runs on. In this example, we're using Ubuntu.
    
* `steps`: The individual tasks that make up your job.
    
* `name`: The name of your step.
    
* `uses`: The action that you want to use. In this example, we're using the `actions/checkout` Action to check out the code.
    
* `run`: The command that you want to run. In this example, we're using `make` to build and test the code.
    

### GitHub Actions Components 🔨

GitHub Actions is made up of several components that work together to automate your workflow. Let’s take a closer look at each of these components:

1. **Actions**: Actions are reusable units of code that perform a specific task, such as building your code, running tests, or deploying your application.
    
2. **Workflows**: Workflows are a set of actions that you want to run in response to an event, such as pushing code to the repository or creating a pull request.
    
3. **Events**: Events are triggers that start a workflow, such as a push to the repository, a pull request, or a schedule.
    
4. **Jobs**: Jobs are a set of steps that you want to run in parallel or sequentially in a workflow.
    
5. **Steps**: Steps are individual tasks that make up a job, such as checking out the code or running a command.
    

### Triggers and GitHub events ✅

To determine when this workflow will be triggered, use the on keyword. For instance, the workflow can be started whenever a push event or a pull request takes place using the code snippet below. You can get a complete list of the events that can start a workflow [here](https://docs.github.com/en/actions/reference/events-that-trigger-workflows).

on: \[push, pull\_request\]

Moreover, you can define the branches to which these rules will apply. For instance, in the code snippet below, we’re starting this workflow whenever the main branch is pushed to and whenever a pull request is filed to merge modifications into the main branch.

```yaml

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
```

The [cron syntax](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/crontab.html#tag_20_25_07) can also be used to [schedule](https://docs.github.com/en/actions/reference/events-that-trigger-workflows#scheduled-events) the execution of a workflow. The following line of code will start this job each day at eight o’clock (all times are in UTC). You should find this [useful web tool](https://crontab.guru/) quite helpful when writing cron rules like this.

```yaml
on: 
  schedule: 
    — cron: ‘0 8 * * *’
```

### Understanding Jobs 📃

Many jobs can be included in a process. Each job can have numerous steps and will have some meta-information about it. Here is a general description of a job’s structure.

```yaml
jobs:
  # General structure of a job
  # ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ 
  
  this_job_key:
  
    # Meta-information about this job
    # ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ 
    
    name: This job 
    runs-on: ubuntu-latest  
    needs: previous_job_key 
    if: github.ref == 'refs/heads/main' 
    
    # Other properties of the job can go here
    # ...
    
    steps:
    # Properties and values defining various steps in this job goes here
    # ...
```

### Steps 🪜

Steps allow us to flesh out what this job should really do.

```yaml
steps:
  # General structure of steps
  # ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓  
  
  - name: Your step name
    uses: third-party-action@version
    if: always()  
    with:
      other-properties: property-value
      # Other properties of this property can go here
      # ...
      
  - name: Your step name
    run: npm run build
    # Other properties of this step can go here
    # ...
```

* `name`: Just like the job name, this keyword is optional but I’d highly recommend using this because it provides better readability. Without specifying a step name, GitHub Actions will automatically assign a name based on your task.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680369529229/b5252c68-21e4-4b50-a1c2-7bc5204978e7.png align="left")

Every step above uses the name keyword to describe what it’s meant to do.

* `if`: Conditionally execute a step, similar to the `if` keyword in the jobs section above.
    

### Using an action from the marketplace

One or more actions from the [GitHub Actions Marketplace](https://github.com/marketplace?type=actions) can be used. These community-developed solutions address particular issues. When employing a third-party activity from the marketplace, you would utilise these terms.

* `uses`: This value is of the format `action-name/version`. The action name will usually be provided by the creator of the action. If not, the action name is usually of the format `github-repo-owner/repo-name`. For the version, you could either use `@latest` or a specific version like `@v2`. If you do use `@latest`, you would need to be wary of any breaking changes being introduced in the near future which may cause your workflow to fail.
    
* `with`: If the action needs some inputs, you can supply them using this keyword.
    

### Running a custom command

When employing third-party actions is not an option, you are presumably running certain commands. The steps where you want to run a command-line are for which these keywords are used.

* `run`: If you’d like to execute a command-line program, you may supply the command here.
    
* `working-directory`: You can specify the directory to run this command in.
    
* `shell`: By default, `bash` is used in a non-Windows runner and `pwsh` (PowerShell Core) is used in a Windows runner. If you’d like to change this, you can select one of the many [pre-defined shell options](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#using-a-specific-shell).
    

> **Note** : A step will either have `run` or `uses` but not both.

### Artifacts

If you’ve ever used other CI/CD systems, you might be curious in how artefacts function in GitHub Actions. Data is shared between jobs via artefacts, and they are also used to store data when a process is finished. We’ll need a method for uploading and downloading artefacts in GitHub Actions. Let’s look at it.

#### 1) Uploading an artifact

To upload an artifact, we’ll make use of the [Upload a Build Artifact](https://github.com/marketplace/actions/upload-a-build-artifact) GitHub Action created by GitHub.

```yaml
# In a previous step you would generate a deployable package
# Example: Executing `npm run build` in a React app will generate 
# your production-ready website in the 'build' folder.

- name: Upload deployable package
  uses: actions/upload-artifact@v2
  with:
    name: my-artifact
    path: path/to/artifact
```

The above code snippet shows how you’d use this action. The `uses` property tells us that we’re using the action `actions/checkout` version 2. The `name` keyword allows us to name the artifact and the `path` keyword indicates the directory that contains the data that needs to be uploaded.

After a successful build, you should see the generated artifact in the GitHub Actions UI.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680369531066/0548e19a-7d4c-404a-b4a7-3ccdba7f6e0e.png align="left")

It has the name that you set in the YAML above, as you can see. The artefacts you just uploaded will be downloaded in a ZIP file if you click on that.

#### 2) Downloading an artifact

Similar to the upload artifact step, we’ll be using another action from the marketplace called [Download a Build Artifact](https://github.com/marketplace/actions/download-a-build-artifact).

\# Start of a new job

```yaml
# Start of a new job

- name: Download artifact
  uses: actions/download-artifact@v2
  with:
    name: my-artifact
    path: path/to/artifact
    
# Remainder of the steps
```

The `name` keyword tells the action what artifact to download. The `path` keyword indicates where to place the downloaded artifact files — it will create this directory if one doesn’t already exist. Later in the deployment pipeline, if you need any files from this directory, you can reference them straight-away.

### Meet Git, the GitHub Actions guy 🤝

Git is a handsome and charming guy who loves to automate tasks and make your life easier. He’s always willing to lend a hand, and he’s very knowledgeable about software development. Git’s favorite hobby is tinkering with code, and he enjoys automating workflows.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680369532218/e6412acc-bdbb-4672-af7e-2370deeeb3d2.jpeg align="left")

One day, Git decided to open a business to help developers automate their tasks. He called his business GitHub Actions, and it quickly became popular among developers. Git’s business became so successful that he decided to hire a team of experts to help him out.

Git’s team is made up of various GitHub Actions, each with their own unique abilities. Let’s take a closer look at some of them :

### Action : Pull Request 💪🏻

This GitHub Action is very helpful for developers who want to keep their codebase up-to-date. Whenever someone creates a pull request, this Action automatically reviews the code and suggests any necessary changes. It also alerts the developer if the code doesn’t meet the requirements.

Here’s an example of how you can use this Action :

```yaml
name: Pull Request

on:
  pull_request:
    branches: [ main ]
    
jobs:
  review:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v2
    - name: Run tests
      run: pytest
    - name: Review code
      uses: reviewdog/action-eslint@v1
      with:
        eslint-github-token: ${{ secrets.GITHUB_TOKEN }
```

> ***Tip :*** *Comments can be added to your workflow file by prefixing your comment with a hash* `*#*` *symbol.*

A job key is used to identify each job specifically. All other information concerning this work is contained in this key, which serves as its keyword.

### Action : Push 📌

This GitHub Action is all about pushing your code to the repository. Whenever you push your code, this Action will automatically build and test it. If there are any errors or warnings, it will notify you.

Here’s an example of how you can use this Action :

```yaml
name: Push

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v2
    - name: Build code
      run: make build
    - name: Test code
      run: make test
```

### Action : Schedule ⌚

This GitHub Action is perfect for developers who want to run certain tasks on a regular schedule. It allows you to specify the date and time when you want a particular workflow to run.

Here’s an example of how you can use this Action :

name: Schedule

```yaml
name: Schedule

on:
  schedule:
    - cron: '0 0 * * *'

jobs:
  backup:
    runs-on: ubuntu-latest
    steps:
    - name: Backup database
      run: mysqldump -h $DB_HOST -u $DB_USER -p$DB_PASSWORD $DB_NAME > backup.sql
    - name: Upload backup
      uses: actions/upload-artifact@v2
      with:
        name: backup
        path: backup.sql
```

### Action : Workflow Dispatch ⚙️

This GitHub Action is like a secret agent who waits for a signal to take action. Whenever you send a request to it, it will trigger a workflow, allowing you to perform specific actions on your code.

Here’s an example of how you can use this Action :

name: Workflow Dispatch

```yaml
name: Workflow Dispatch

on:
  workflow_dispatch:
    inputs:
      name:
        description: 'Enter your name'
        required: true

jobs:
  greet:
    runs-on: ubuntu-latest
    steps:
    - name: Greet user
      run: echo "Hello, ${{ github.event.inputs.name }}!"
```

### **Best Practices for GitHub Actions 😎☀️**

Now that you understand the syntax and components of GitHub Actions, let’s go over some best practices for using this tool effectively:

1. **Keep your workflows organized**: Use descriptive names for your workflows and organize them into folders if you have multiple workflows.
    
2. **Use environment variables**: Use environment variables to store sensitive information, such as API keys or passwords. GitHub provides a feature called “secrets” that allows you to store encrypted values as environment variables.
    
3. **Test your workflows**: Test your workflows in a sandbox environment before using them in production. This will help you catch any errors before they affect your code.
    
4. **Use version control**: Keep your workflows under version control using Git so that you can roll back to previous versions if necessary.
    
5. **Use community actions**: Don’t reinvent the wheel. Use community actions that have already been developed and tested by others. You can find community actions in the GitHub Marketplace.
    
6. **Use caching**: If your workflow involves building or testing code, use caching to speed up the process. Caching allows you to store files or dependencies between runs of the workflow.
    
7. **Use matrix strategies**: If you need to test your code on multiple versions of an operating system or programming language, use matrix strategies to run your workflow in parallel across multiple configurations.
    
8. **Use conditional logic**: Use conditional logic to run specific steps based on the outcome of previous steps. This can help you save time and resources by only running the necessary steps.
    
9. **Monitor your workflows**: Monitor your workflows using the GitHub Actions dashboard to ensure that they are running smoothly and to catch any errors.
    
10. **Document your workflows**: Document your workflows so that others can understand what they do and how they work.
    

### Conclusion 💭

GitHub Actions is a powerful tool that can automate many tasks in your software development workflow. With its rich ecosystem of Actions and flexible syntax, you can easily customize your workflows to suit your needs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680369533581/aaa2509c-d9e2-4621-a248-1dcff99a9bf1.jpeg align="left")

By following best practices and testing your workflows thoroughly, you can ensure that your code is built, tested, and deployed quickly and reliably. So go ahead and give GitHub Actions a try — your future self will thank you!

### GitHub repo for the article 💻

[**GitHub - devangtomar/github-action-fundamentals: Unleashing the Full Potential of GitHub Actions: A…**  
\*This repository contains a beginner's guide to Github Actions, designed for users who are new to the concept of…\*github.com](https://github.com/devangtomar/github-action-fundamentals)

### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on [Dev.to](http://Dev.to): [devangtomar](https://dev.to/devangtomar)