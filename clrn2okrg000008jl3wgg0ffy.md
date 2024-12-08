---
title: "How Cloudflare Achieved 55 Million Requests per Second with Just 15 PostgreSQL Clusters! 💻"
datePublished: Fri Jan 19 2024 05:32:15 GMT+0000 (Coordinated Universal Time)
cuid: clrn2okrg000008jl3wgg0ffy
slug: how-cloudflare-achieved-55-million-requests-per-second-with-just-15-postgresql-clusters-2d8a28ffd100
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705815795579/711faec2-4493-4d62-98e0-b51a91ae0d07.jpeg
tags: cloudflare, postgresql, system-architecture, system-design, devops-articles

---

In the vast landscape of the internet, Cloudflare emerged in July 2009, founded by a group of visionaries with the goal of making the internet faster and more reliable. The challenges they faced were immense, but their growth was nothing short of spectacular. Fast forward to today, and Cloudflare serves a whopping 20% of the internet’s traffic, handling a staggering 55 million HTTP requests per second. The most incredible part? They achieved this feat with only 15 PostgreSQL clusters. Let’s dive into the magic behind this impressive system design!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705815780808/9ccdc664-8351-433c-a14d-05f298cd47db.jpeg align="center")

### PostgreSQL Scalability: The Core 🚀

#### Resource Usage Optimization with PgBouncer 🔄

Handling Postgres connections efficiently is crucial, and Cloudflare uses PgBouncer as a TCP proxy to manage a pool of connections to Postgres.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705815782364/f8939662-5362-43ac-8d61-a9ca0dc99e5e.jpeg align="left")

This not only prevents connection starvation but also tackles the challenge of diverse workloads from different tenants within a cluster.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705815783954/562fa571-27c1-4509-b329-af0bc6a05d77.png align="center")

#### Thundering Herd Problem Solved! 🐘

The infamous Thundering Herd Problem, where many clients query a server concurrently, was addressed by Cloudflare using PgBouncer. It smartly throttles the number of Postgres connections created by a specific tenant, preventing degradation of database performance during high traffic.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705815785847/c3b0c450-1155-4751-b7f1-92ac301bd756.jpeg align="center")

#### Performance Boost with Bare Metal Servers and HAProxy ⚙️

Cloudflare opts for bare metal servers without virtualization, ensuring high performance. They leverage HAProxy as an L4 load balancer, distributing traffic across primary and secondary database read replicas, providing a robust solution for performance enhancement.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705815787098/63a0e739-2b9a-4ffd-90b8-e00c947e8464.jpeg align="center")

#### Congestion Avoidance Algorithm for Concurrency 🚧

To manage concurrent queries and avoid performance degradation, Cloudflare employs the TCP Vegas congestion avoidance algorithm.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705815788380/360ee687-27fb-4bb5-ade9-e661cc7d42f5.png align="center")

This algorithm samples each tenant’s transaction round-trip time to Postgres, dynamically adjusting the connection pool size to throttle traffic before resource starvation occurs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705815789952/22c812c3-a772-4e2b-a55a-0785d840b3ce.jpeg align="center")

#### Ordering Queries Strategically with Priority Queues 📊

Cloudflare tackles query latency by ranking queries at the PgBouncer layer using queues based on historical resource consumption.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705815791437/6f77b408-27bf-4f7a-8cc0-ecd49985fc2e.jpeg align="center")

Enabling priority queuing only during peak traffic ensures that queries needing more resources are handled efficiently without causing resource starvation.

#### High Availability with Stolon Cluster Manager 🌐

Ensuring high availability is a top priority for Cloudflare. They employ the Stolon cluster manager, replicating data across Postgres instances, and performing failovers seamlessly in peak traffic. With data replication across regions and proactive network testing, Cloudflare ensures a robust and resilient system.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705815792842/1781a96a-6a8d-49d9-8318-97a20b8d12c8.jpeg align="center")

#### Conclusion 🌈

Cloudflare’s journey to handling 55 million requests per second with just 15 PostgreSQL clusters is a testament to their ingenious system design. From smart connection pooling to tackling concurrency and ensuring high availability, they’ve navigated the complexities of scaling with finesse. Subscribe to our newsletter for more simplified case studies and unravel the secrets behind the tech giants’ success! 🚀🔍

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705815794188/8b0a6207-6a26-4c84-910e-7af1923a40d1.jpeg align="center")

#### Connect with Me on social media 📲

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on Dev.to: [devangtomar](https://dev.to/devangtomar)