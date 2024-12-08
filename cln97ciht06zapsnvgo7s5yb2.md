---
title: "Building a Simple Web Server with Go 🐭"
seoTitle: "Building a Simple Web Server with Go 🐭"
seoDescription: "Are you a beginner eager to explore the world of web servers using the Go programming language? 🚀"
datePublished: Mon Oct 02 2023 07:01:12 GMT+0000 (Coordinated Universal Time)
cuid: cln97ciht06zapsnvgo7s5yb2
slug: building-a-simple-web-server-with-go-dfa1f332a50e
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696269966417/1c953197-7ce6-4fee-9518-c3f7b62291e2.png
tags: go, golang, go-cjffccfnf0024tjs1mcwab09t, golang-developer, golang-web-development

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696269966417/1c953197-7ce6-4fee-9518-c3f7b62291e2.png align="left")

Are you a beginner eager to explore the world of web servers using the Go programming language? 🚀 In this comprehensive guide, I’ll take you on a journey to create a basic web server that not only serves static files but also handles essential HTTP requests. By the end of this tutorial, you’ll have a robust grasp of the fundamental concepts required for building a web server with Go. Let’s dive in!

### Understanding Web Servers 🌐

A web server is a software application that processes incoming requests from clients, typically web browsers, and responds by serving web content. It plays a vital role in the architecture of the World Wide Web, enabling the exchange of information between clients and servers. Web servers are the backbone of websites, web applications, and various online services.

### Prerequisites 🛠️

Before we embark on this adventure, make sure you have the following prerequisites:

1. Basic understanding of Go programming concepts.
    
2. Go programming language installed on your machine. You can download and install Go from the official website: [Go Downloads](https://golang.org/dl/).
    

### GitHub repo 👨🏻‍💻

%[https://github.com/devangtomar/simple-go-webserver] 

### Getting Started 🏁

Let’s kickstart our journey by creating a simple web server that serves static HTML files and handles HTTP requests. Follow these steps:

Step 1: Setting Up the Project

```javascript
mkdir simple-go-webserver
cd simple-go-webserver
mkdir static
cd static
# Create index.html, form.html, and hello.html (you can copy the content from the provided GitHub links)
```

Step 2: Writing the Go Code

Create a file named `main.go` in the project directory and add the following code:

```javascript
package main

import (
    "fmt"
    "log"
    "net/http"
)

func helloHandler(w http.ResponseWriter, r *http.Request) {
    // Handler logic for /hello route
}
func formHandler(w http.ResponseWriter, r *http.Request) {
    // Handler logic for /form route
}
func main() {
    // Main function logic
}
```

Step 3: Running the Web Server

```go
go run main.go
```

Open your web browser and visit [http://localhost:8080](http://localhost:8080/) to see your web server in action!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696269968698/1e0d07e9-ca70-484f-8ea8-1eaa4fee3b7b.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696269971231/158e14a4-391c-4b87-9338-55671d9863a7.png align="left")

### Key Components of the Code 🧩

Let’s break down the crucial components of the code:

1\. Importing Packages: We import necessary packages like `fmt` for formatted I/O, `log` for logging, and `net/http` for building HTTP servers and handling HTTP requests and responses.

2\. Handlers: We define two handler functions:

* `helloHandler`: Handles requests to the "/hello" route.
    
* `formHandler`: Handles POST requests to the "/form" route.
    

3\. Route Handling: We use `http.HandleFunc` to associate our handler functions with specific routes, such as /hello and /form.

4\. Serving Static Files: We create an HTTP file server to serve static files from the “static” directory using `http.FileServer`.

5\. Listening and Serving: We use `http.ListenAndServe` to start the web server on port 8080.

### Conclusion 🎉

Congratulations! You’ve successfully built a simple web server using the Go programming language. This project lays the foundation for more advanced web applications and APIs. Remember, practice and experimentation are key.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696269973602/58affd20-9c3d-4276-be54-2616897393af.png align="left")

Explore the code, add new features, and refer to the [Go documentation](https://go.dev/doc/) to enhance your web development skills. Happy coding! 🚀

#### Connect with Me on social media 📲

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on Dev.to: [devangtomar](https://dev.to/devangtomar)