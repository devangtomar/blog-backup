---
title: "Monitoring Made Fun: A Beginner’s Guide to Prometheus 👀"
datePublished: Fri Apr 07 2023 07:11:28 GMT+0000 (Coordinated Universal Time)
cuid: clg69c7xb0281uonv310dhbvr
slug: monitoring-made-fun-a-beginners-guide-to-prometheus-184e6b7a3eb4
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680854444258/b6a6eb92-a02a-44d4-9318-a0743340383d.jpeg

---

#### 👨‍💻🔧 Prometheus: The Fire-Starter of Monitoring Tools

If you’re familiar with the Greek myth of Prometheus, you know that he was the Titan who stole fire from the gods and gave it to humans. But did you know that there’s also a monitoring tool named after him? 🤔 That’s right, Prometheus is a popular open-source system for collecting and analyzing metrics from your applications and infrastructure.

Now, I know what you’re thinking: “Great, another monitoring tool. Just what I need.” But trust me, Prometheus is different. Not only is it powerful and flexible, but it’s also surprisingly easy to use. And best of all, it’s got a cool name! 😎

So, what exactly is Prometheus, and why should you care? Let’s find out. 🤔

### 🔥 Prometheus: The Fire-Starter

Prometheus was created by SoundCloud in 2012 and released as an open-source project in 2015. Since then, it’s become one of the most popular monitoring tools out there, used by companies like Airbnb, Digital Ocean, and Google. 🔥

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680854434851/0f8ea9d4-bbb3-474e-87c3-b4ac75e71c4f.png align="left")

So, what makes Prometheus so special? For starters, it’s designed to be highly scalable and fault-tolerant. It’s also built on a time-series database that can store and query massive amounts of data with ease. And it’s got a powerful query language that lets you slice and dice your metrics in all sorts of interesting ways.

But perhaps the most unique thing about Prometheus is its “pull” model. Unlike some other monitoring tools that use a “push” model, where agents send data to a central server, Prometheus works the other way around. It has a central server that “pulls” data from your applications and infrastructure at regular intervals. This means that you don’t need to worry about setting up agents or managing firewalls, and it also makes Prometheus more resilient to network failures.

### 👨‍💻 Prometheus: The Tool for Developers

So, who is Prometheus for, exactly? Well, in short, anyone who wants to monitor their applications and infrastructure. But Prometheus is especially well-suited for developers, who often need to debug performance issues and optimize their code.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680854436673/a91e54d1-de29-48ea-a2f5-c29905b0f269.jpeg align="left")

With Prometheus, you can easily track metrics like CPU usage, memory usage, request latency, and error rates. You can also set up alerts to notify you when something goes wrong. And thanks to its flexible query language, you can create custom dashboards that show exactly the information you need.

But perhaps the best thing about Prometheus is that it’s highly extensible. There are dozens of third-party exporters that you can use to collect metrics from popular tools like MySQL, nginx, and Redis. And if you can’t find an exporter for your favorite tool, you can always write your own.

### 🔥 👨‍💻 Getting Started with Prometheus

The first step in using Prometheus is to download and install it on your system. You can find installation instructions on the official [Prometheus website](https://prometheus.io/).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680854438209/0fb82224-419a-49ca-995f-1fec30732050.jpeg align="left")

Once you have Prometheus installed, you’ll need to configure it to collect metrics from your system. This involves two main steps:

* Instrument your code to emit metrics
    
* Configure Prometheus to scrape those metrics
    

#### 🔧 Instrumenting Your Code

To start collecting metrics, you’ll need to instrument your code to emit metrics that Prometheus can scrape. Prometheus uses a pull-based model to collect metrics, which means that it periodically sends HTTP requests to your application’s endpoints to collect metrics.

To make your application’s metrics available to Prometheus, you’ll need to use a client library that is compatible with your programming language. Prometheus provides a list of client libraries for popular languages like Java, Python, and Go on its website.

For example, if you’re using the Python Flask web framework, you can use the `prometheus-flask-exporter` library to instrument your code. Here’s an example of how to use it:

```python
from prometheus_flask_exporter import PrometheusMetrics
app = Flask(__name__)

# Create a PrometheusMetrics object
metrics = PrometheusMetrics(app)

# Instrument a Flask route
@app.route('/')
def hello_world():
return 'Hello, World!'

# Increment a counter metric
metrics.counter('requests_total', 'Total number of requests')
```

In this example, we create a `PrometheusMetrics` object and use it to instrument a Flask route. We also create a counter metric called `requests_total` to track the total number of requests.

#### 🔧 Configuring Prometheus to Scrape Metrics

Once you’ve instrumented your code, you’ll need to configure Prometheus to scrape your metrics. This involves adding a `scrape_config` section to the `prometheus.yml` configuration file.

Here’s an example `prometheus.yml` file that scrapes metrics from a Flask application running on `localhost:5000`:

```yaml
global:scrape_interval: 15s
scrape_configs:
- job_name: 'flask'
scrape_interval: 5s
metrics_path: '/metrics'
static_configs:
- targets: ['localhost:5000']
```

In this example, we set the global `scrape_interval` to 15 seconds and define a `scrape_config` for our Flask application. The `job_name` is set to `'flask'`, and the `metrics_path` is set to `'/metrics'`, which is the endpoint that the prometheus-flask-exporter library uses to expose metrics.

We also define a `static_configs` section that specifies the targets we want to scrape. In this case, we're scraping the `localhost:5000` endpoint where our Flask application is running.

Once you’ve added your `scrape_config` to `prometheus.yml`, you can start Prometheus by running the `prometheus` command in your terminal. Prometheus will then start scraping metrics from your application and storing them in its time-series database.

### 📈 Analyzing Metrics with Prometheus

Now that you’ve collected metrics with Prometheus, it’s time to start analyzing them. Prometheus provides a powerful query language called PromQL that you can use to query and aggregate metrics.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680854440017/04811d57-afa2-4375-8ebc-7f9c88847f2f.png align="left")

Here’s an example of how to use PromQL to calculate the average request latency over the last 5 minutes:

```scss
rate(http_request_duration_seconds_sum[5m]) / rate(http_request_duration_seconds_count[5m])
```

In this example, we use the `rate()` function to calculate the per-second rate of request duration and divide the sum of those durations by the count of requests to get the average request latency.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680854441661/90c70a25-fa7f-402d-9b93-5e9041fe671b.jpeg align="left")

PromQL also provides a wide range of functions for aggregating, filtering, and transforming metrics. You can find a full list of PromQL functions in the Prometheus documentation.

### 👍 Why Choose Prometheus?

So why should you choose Prometheus as your monitoring tool? Here are just a few reasons:

1. 🔍 **Powerful Query Language**: PromQL provides a flexible and expressive language for querying and aggregating metrics.
    
2. 📈 **Real-Time Visualization**: Prometheus includes a built-in web UI that allows you to visualize and explore your metrics in real-time.
    
3. 💪 **Easy to Scale**: Prometheus is designed to be easy to scale horizontally, allowing you to handle large volumes of metrics with ease.
    
4. 🕰️ **High Availability**: Prometheus is designed to be highly available, with built-in support for redundant storage and alerting.
    
5. 🧰 **Extensible**: Prometheus is built to be extensible, with support for a wide range of exporters, client libraries, and integrations.
    

### 👋 Wrapping Up

Prometheus is a powerful and flexible monitoring tool that can help you collect and analyze metrics from a wide range of sources. With its powerful query language and real-time visualization, Prometheus can help you gain insights into your system’s performance and improve your application’s reliability.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680854442932/96a81807-ea1d-4f6a-b8ec-9d0f30e7d738.jpeg align="left")

So why not give Prometheus a try? With its easy-to-use client libraries, simple configuration, and powerful features, it’s never been easier to get started with monitoring.

#### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on Dev.to: [devangtomar](https://dev.to/devangtomar)