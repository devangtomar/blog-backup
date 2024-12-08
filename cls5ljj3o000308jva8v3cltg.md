---
title: "How one line of code caused a $60 million loss 📉😓"
datePublished: Tue Jan 30 2024 18:32:43 GMT+0000 (Coordinated Universal Time)
cuid: cls5ljj3o000308jva8v3cltg
slug: how-one-line-of-code-caused-a-60-million-loss-6cab28f863c4
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706935863893/8758352d-d0ae-46cf-8546-4bdaf100645a.jpeg
tags: programming-blogs, coding, horror, bad-code, cost-of-bad-code, coding-code-review

---

60,000 people lost full phone service, half of AT&T’s network was down, and 500 airline flights were delayed

On January 15th, 1990, AT&T’s New Jersey operations center detected a widespread system malfunction, shown by a plethora of red warnings on their network use display.

**Despite attempts to rectify the situation, the network remained compromised for 9 hours, leading to a 50% failure rate in call connections.**

AT&T lost over **$60 million** as a result with **over 60,000 of Americans left with fully disconnected phones**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706935855811/b8ddd066-9573-4334-a2ef-977b37b2ce4a.png align="center")

Furthermore, **500 airline flights were delayed, affecting 85,000 people.**

AT&T’s long-distance network was supposedly a paragon of efficiency, handling a substantial portion of the nation’s calls with its advanced electronic switches and signaling system. This system usually completed call routing within seconds.

However, on this day, a fault originating in a New York switch cascaded through the network. **This was due to a software bug in a recent update that contained a critical bug affecting the network’s 114 switches.** When the New York switch reset itself and sent out signals, this bug caused a domino effect, leading to widespread network disruption.

**This software patch had already gone through layers of testing without being caught. This incident was especially surprising because AT&T was known for their rigorous testing.**

### The Problem 😓

The root cause was traced back to a coding error in a software update implemented across the network’s switches.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706935857691/d0c23dd7-16be-45d6-8b5b-20b244ddafd2.jpeg align="left")

The error, within a C program, involved a misplaced *break* statement within nested conditional statements, leading to data overwrites and system resets.

The pseudocode :

```python
while (ring receive buffer not empty 
          and side buffer not empty):

  Initialize pointer to first message in side buffer
       or ring receive buffer
  
  get copy of buffer
  
  switch (message):
  
    case (incoming_message):
    
      if (sending switch is out of service):
      
        if (ring write buffer is empty):
      
          send "in service" to status map
      
        else:
      
          break // The error was here!
    
        END IF
  
      process incoming message, set up pointers to
               optional parameters
  
      break
    END SWITCH
  
  
do optional parameter work
```

The problem:

* If the *ring write buffer is NOT empty*, then the \`if\` statement on line 7 is skipped and the *break* statement on line 10 is hit instead.
    
* However, for the program to function properly, line 11 should have been hit instead.
    
* When the *break* statement is hit instead of the incoming message being processed and pointers being set up to optional parameters, then data (the pointers that should’ve been held) is overwritten
    
* The error correction software identified the data overwrite and initiated a shutdown of the switch for a reset. This issue was compounded because this flawed software was present in all switches across the network, leading to a chain reaction of resets that ultimately crippled the entire network system.
    

Despite having a network designed for resilience, **one line of code was able to bring down half the country’s main line of communication.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706935859038/d3967688-bb61-4c8d-824e-c346d2021a3c.jpeg align="center")

### The Fix 🔨

It took engineers 9 hours to get AT&T’s system fully back online. They did so mostly by rolling back the switches to a previous, working version of code.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706935860518/b44d2c91-c065-481c-b4c5-e12c8610aaba.jpeg align="center")

It actually took software engineers two weeks of rigorous code reading, testing, and replication to actually understand where the bug was.

### Conclusion 💭

For AT&T, unfortunately, this wasn’t even their biggest system crash of the 90s. They encountered many more issues later in the decade.

**In reality, it wasn’t one line of code that brought down a system**. It was a failure in processes.

Today’s companies have even better processes in place, and even then, bugs slip through. Google wrote a great retrospective on [20 years of Site Reliability Engineering](https://sre.google/resources/practices-and-processes/twenty-years-of-sre-lessons-learned/), where they reflect on YouTube’s first global outage in 2016.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706935862141/efa35110-ee79-4e30-8405-8480a68e4eed.jpeg align="left")

The scale of an outage for companies is huge and there are lessons to be learned from each outage. For most, however, outages come down to human error and gaps in processes.

### Connect with Me on social media 📲

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on Dev.to: [devangtomar](https://dev.to/devangtomar)