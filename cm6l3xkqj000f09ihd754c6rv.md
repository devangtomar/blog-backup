---
title: "How to Write Your Own Terraform Provider: A Step-by-Step Guide 🛠️ ️"
datePublished: Fri Jan 31 2025 18:31:02 GMT+0000 (Coordinated Universal Time)
cuid: cm6l3xkqj000f09ihd754c6rv
slug: how-to-write-your-own-terraform-provider-a-step-by-step-guide
canonical: https://dev.to/devangtomar/how-to-write-your-own-terraform-provider-a-step-by-step-guide-g0i
tags: terraform, terraform-state, terraform-cloud, terraform-module, custom-providers

---

---

Terraform has become the go-to tool for infrastructure as code (IaC), enabling developers to define and provision infrastructure using a declarative configuration language. While Terraform supports a wide range of cloud providers and services out of the box, there may come a time when you need to manage a custom resource or integrate with a proprietary API. That’s where writing your own Terraform provider comes in! 🌟

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738348695560/acd7d13b-cfe9-4835-8a36-802b26acc7f5.png align="left")

In this article, we’ll walk through the process of creating your very own Terraform provider from scratch. Whether you’re managing a niche cloud service or an internal tool, this guide will help you get started. Let’s dive in! 💻

#### 🤔 Why Write a Custom Terraform Provider?

Before we jump into the \*how\*, let’s talk about the \*why\*. Here are a few reasons you might want to create your own Terraform provider:

1. **Custom Resources** : You have a unique service or tool that isn’t supported by existing providers.
    
2. **Proprietary APIs** : Your organization uses internal APIs that need to be managed as infrastructure.
    
3. **Extending Terraform** : You want to add functionality to Terraform that aligns with your specific workflows.
    

If any of these resonate with you, it’s time to roll up your sleeves and start building! 🛠️

#### 🧰 Prerequisites

Before we begin, make sure you have the following tools installed:

1. **Go (Golang)**: Terraform providers are written in Go. Install it from [golang.org](%5Bhttps://golang.org/%5D\(https://golang.org/\)).
    
2. **Terraform** : You’ll need Terraform installed to test your provider. Download it from [terraform.io](%5Bhttps://www.terraform.io/%5D\(https://www.terraform.io/\)).
    
3. **Git** : For version control and managing your provider’s code.
    

#### 🚀 Step 1: Set Up Your Go Environment

First, let’s set up your Go workspace. Create a new directory for your provider and initialize a Go module:

```plaintext
mkdir terraform-provider-myprovider
cd terraform-provider-myprovider
go mod init github.com/yourusername/terraform-provider-myprovider
```

This will create a go.mod file, which manages your project’s dependencies.

#### 🛠️ Step 2: Create the Provider Skeleton

Terraform providers follow a specific structure. Start by creating the basic files and directories:

1. Create the main.go file:  
    This is the entry point for your provider.
    

```plaintext
package main

import (
    "github.com/hashicorp/terraform-plugin-sdk/v2/plugin"
    "github.com/yourusername/terraform-provider-myprovider/myprovider"
)

func main() {
    plugin.Serve(&plugin.ServeOpts{
        ProviderFunc: myprovider.Provider,
    })
}
```

2. Create the provider file:  
    In a new directory called myprovider, create a file named provider.go.
    

```plaintext
package myprovider

import (
    "github.com/hashicorp/terraform-plugin-sdk/v2/helper/schema"
)

func Provider() *schema.Provider {
    return &schema.Provider{
        ResourcesMap: map[string]*schema.Resource{},
        DataSourcesMap: map[string]*schema.Resource{},
    }
}
```

This sets up the basic structure of your provider. Right now, it doesn’t do much, but we’ll add resources and data sources soon.

#### 🔧 Step 3: Define Your First Resource

A Terraform provider is useless without resources. Let’s define a simple resource. For example, let’s say we’re creating a provider to manage “widgets” in a fictional API.

1. Create a resource file:  
    In the myprovider directory, create a file named resource\_widget.go.
    

```plaintext
package myprovider

import (
    "github.com/hashicorp/terraform-plugin-sdk/v2/helper/schema"
)

func resourceWidget() *schema.Resource {
    return &schema.Resource{
        Create: resourceWidgetCreate,
        Read: resourceWidgetRead,
        Update: resourceWidgetUpdate,
        Delete: resourceWidgetDelete,

        Schema: map[string]*schema.Schema{
            "name": {
                Type: schema.TypeString,
                Required: true,
            },
            "description": {
                Type: schema.TypeString,
                Optional: true,
            },
        },
    }
}

func resourceWidgetCreate(d *schema.ResourceData, m interface{}) error {
    // Implement logic to create a widget.
    d.SetId("widget-id") // Set a dummy ID for now.
    return nil
}

func resourceWidgetRead(d *schema.ResourceData, m interface{}) error {
    // Implement logic to read a widget.
    return nil
}

func resourceWidgetUpdate(d *schema.ResourceData, m interface{}) error {
    // Implement logic to update a widget.
    return nil
}

func resourceWidgetDelete(d *schema.ResourceData, m interface{}) error {
    // Implement logic to delete a widget.
    return nil
}
```

2. Register the resource:  
    Update the provider.go file to include the new resource.
    

```plaintext
func Provider() *schema.Provider {
    return &schema.Provider{
        ResourcesMap: map[string]*schema.Resource{
            "myprovider_widget": resourceWidget(),
        },
        DataSourcesMap: map[string]*schema.Resource{},
    }
}
```

#### 🧪 Step 4: Test Your Provider

Now that you’ve defined a resource, it’s time to test your provider. First, build the provider:

```plaintext
go build -o terraform-provider-myprovider
```

Next, create a Terraform configuration file (main.tf) to test the provider:

```plaintext
provider "myprovider" {}

resource "myprovider_widget" "example" {
  name = "example-widget"
  description = "This is an example widget."
}
```

Finally, initialize and apply your Terraform configuration:

```plaintext
terraform init
terraform apply
```

#### 🚀 Step 5: Publish and Share Your Provider

Once your provider is working, you can publish it to the Terraform Registry or share it with your team. To publish it:

1. Tag your release:  
    Use Git to tag your release.
    

```plaintext
git tag v1.0.0
git push origin v1.0.0
```

2. Submit to the Terraform Registry:  
    Follow the [Terraform Registry documentation](https://www.terraform.io/docs/registry/providers/publishing.html) to publish your provider.
    

#### 🎉 Congratulations! You’ve Built a Terraform Provider!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738348697100/77aa0a16-f05c-4469-bd2f-ae57862dc1eb.png align="left")

Writing a custom Terraform provider might seem daunting at first, but once you break it down into steps, it’s entirely manageable. By following this guide, you’ve learned how to:

* Set up a Go project for your provider.
    
* Define resources and data sources.
    
* Test and publish your provider.