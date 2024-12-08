---
title: "How Facebook Keeps Millions of Servers Synced 🕰️⏰"
datePublished: Fri Jan 26 2024 05:31:44 GMT+0000 (Coordinated Universal Time)
cuid: clrvmwfke000809i8g1pk222k
slug: how-facebook-keeps-millions-of-servers-synced-efb88f-6d6ebd519963
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706333484124/cbb9bc19-c6ba-4c04-b66b-47e62b5ac4b9.jpeg
tags: software-development, facebook, system-architecture, software-engineering, system-design, synchronous, facebookads

---

If you’re running a distributed system, it’s *incredibly* important to keep the system clocks of the machines synchronized. If the machines are off by a few seconds, this will cause a huge variety of different issues.

You can probably imagine why unsynchronized clocks would be a big issue, but just to beat a dead horse…

Today, let’s dive into the intricate world of time synchronization at Meta. Buckle up, it’s not just about ticking clocks; it’s about the heartbeat of millions of servers! 💻🌐

#### ⏳ Why Sync Matters

Running a distributed system? Syncing system clocks is crucial! 🔄 Unsynchronized clocks? Brace yourself for data inconsistency, log chaos, security issues, and more! Facebook knows this too well.

#### 🌐 Meet NTP and PTP

NTP: Old but gold. Syncs computers within milliseconds. How? Clients talk to NTP servers, adjusting internal time based on roundtrip delays.

PTP: The shiny new kid. Precision to nanoseconds or even picoseconds! It tackles network delays with hardware timestamping. But, watch out for the load it places on network hardware! 💽⚙️

#### 🌟 Facebook’s Sync Symphony

NTP Days: Facebook danced with Ntpd and Chrony. Chrony brought nanoseconds to the party, but the story doesn’t end there.

PTP Era: In 2022, Facebook waved goodbye to NTP, embracing Precision Time Protocol for superior precision and scalability. Say hello to nanosecond accuracy! 🚀

Absolutely, let’s break down the details of Meta’s pursuit of nanosecond accuracy using Precision Time Protocol (PTP) and the key components involved:

#### 🏹 Aim: Nanoseconds! 🎯

Meta’s shift to PTP comes with the ambitious goal of achieving nanosecond-level accuracy in time synchronization. This precision is crucial in the fast-paced world of distributed systems where every second matters.

### 🌐 Components Leading the Charge

#### PTP Rack

The PTP Rack is the nerve center, housing the hardware and software responsible for serving time to clients. Here’s what makes it tick:

\- **GNSS Antenna**: This critical component communicates with the Global Navigation Satellite System (GNSS). It ensures that the PTP system is in sync with the global positioning signals, enhancing accuracy.  
  
\- **Time Appliance:** A dedicated piece of hardware residing in the PTP Rack. It combines a GNSS receiver and a miniaturized atomic clock. This combination ensures that even in scenarios where GNSS connectivity is lost, the Time Appliance can maintain accurate timekeeping independently.

The PTP Rack, with its GNSS synchronization and atomic clock precision, sets the stage for achieving the nanosecond goal.

#### The Network

The network plays a pivotal role in transmitting PTP messages from the PTP Rack to clients. Meta employs unicast transmission, a communication method where information flows from one sender (PTP Rack) to a single recipient (PTP Client). This choice simplifies network design and enhances scalability.

Unicast transmission ensures that each client receives the necessary time synchronization information directly from the PTP Rack, reducing the complexity that could arise in a multicast setup.

#### PTP Client

Running on individual machines, the PTP Client is the endpoint that actively communicates with the PTP network. Meta uses an open-source PTP client called ptp4l for this purpose. However, the implementation wasn’t without its challenges, especially when dealing with edge cases.

\- **Open Source Client:** Ptp4l is an open-source implementation, reflecting Meta’s commitment to transparency and community collaboration. It’s a tool that facilitates communication between the PTP Rack and individual servers, allowing them to synchronize their clocks with nanosecond precision.

\- **Challenges with Edge Cases:** While ptp4l is a robust tool, Meta acknowledges challenges faced in specific scenarios or with certain types of network cards. These edge cases required additional attention to ensure the seamless functioning of the PTP system.

#### 🌟 Benefits of the PTP System

\- **Higher Precision and Accuracy:** The PTP system allows Meta to achieve precision within nanoseconds, a significant leap from the millisecond-level synchronization provided by traditional methods like NTP.

\- **Better Scalability:** Unicast transmission reduces the frequency of check-ins required for synchronization, enabling smoother network operation as the system scales. A single source of truth for timing enhances overall scalability.

\- **Mitigation of Network Delays and Errors:** PTP’s focus on hardware timestamping and transparent clocks helps reduce the impact of network delays and errors, contributing to a more robust and reliable synchronization process.

In essence, the PTP trio — PTP Rack, The Network, and PTP Client — embodies Meta’s commitment to precision, scalability, and overcoming challenges in the pursuit of nanosecond-level accuracy in time synchronization.

### 🌐 Network Time Strata Explained:

NTP organizes computers into hierarchical layers called “strata” based on their proximity to highly accurate time sources, typically atomic clocks or GPS receivers. Each stratum represents a level in the hierarchy, and the lower the stratum number, the closer a device is to the primary time source.

**1\. Stratum 0: Atomic Clock or GPS Receiver:**

* At the top of the hierarchy are devices with direct access to incredibly precise timekeeping mechanisms, such as atomic clocks or GPS receivers.
    
* Stratum 0 devices serve as the primary time source for the entire synchronization network.
    

**2\. Stratum 1: Directly Synced with Stratum 0:**

* Stratum 1 devices are directly synchronized with Stratum 0 devices. These could be servers or systems that have a direct connection to the primary time source.
    
* Stratum 1 devices act as secondary time sources for the next level of devices in the hierarchy.
    

**3\. Stratum 2: Syncs with Stratum 1:**

* Stratum 2 devices synchronize their clocks with Stratum 1 devices. These devices are one step further away from the primary time source.
    
* Stratum 2 devices act as time sources for devices in the subsequent stratum.
    

**4. … and so on, until Stratum 15: Indicating Unsynced Devices:**

* The strata continue in a cascading manner, with each stratum representing a level of hierarchy further away from the primary time source.
    
* As the stratum number increases, the accuracy of time synchronization decreases.
    

**5\. Stratum 16: Unsynced Devices:**

* Stratum 16 is a special designation used to indicate devices that are not synchronized with any source. It represents the highest stratum number and signifies unsynchronization.
    

#### 🔄 How Synchronization Works

* Computers in lower strata synchronize their clocks with devices in higher strata. For example, Stratum 2 devices synchronize with Stratum 1 devices, and so on.
    
* Multiple devices in the same stratum can be synchronized with different devices in a higher stratum, introducing redundancy and fault tolerance.
    

#### 🔍 Why the Hierarchy Matters

* The hierarchical structure ensures that not every device needs to directly synchronize with the most accurate time source. This arrangement prevents overloading a single time server with numerous synchronization requests.
    
* The hierarchy allows for redundancy and fault tolerance. If a device in a lower stratum loses synchronization, it can quickly switch to another source in the same stratum or a higher one.
    

#### 🌟 Benefits

* Efficient Synchronization: Devices in lower strata benefit from the accuracy of those in higher strata, optimizing the synchronization process.
    
* Scalability: The hierarchical structure scales well, allowing for the expansion of the synchronization network without overwhelming primary time sources.
    

Understanding Network Time Strata provides insights into how NTP organizes and maintains time synchronization across a distributed system, ensuring accuracy and efficiency in timekeeping.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706333482023/877df832-6bf7-4648-b972-7dfc0ce5befc.jpeg align="center")

#### 🚀 Conclusion

Syncing clocks isn’t just about ticking seconds; it’s the heartbeat of a well-functioning system. Facebook’s journey from NTP to PTP showcases the relentless pursuit of precision and scalability. Time, after all, waits for no server! ⏰💡

What are your thoughts on Meta’s clockwork precision? Share your views! 👇

Happy Syncing! 🌐🚀

#### Connect with Me on social media 📲

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on Dev.to: [devangtomar](https://dev.to/devangtomar)