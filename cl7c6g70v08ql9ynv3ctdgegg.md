---
title: "Bun: A brand-new, lightning-quick JavaScript runtime"
datePublished: Sat Aug 20 2022 17:35:28 GMT+0000 (Coordinated Universal Time)
cuid: cl7c6g70v08ql9ynv3ctdgegg
slug: bun-a-brand-new-lightning-quick-javascript-runtime-e42119a306ca
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1661621346907/QK3LNPdUK.jpeg

---

![Bun logo](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621323955/pL0QJn-BT.png align="left")

### What is Bun? 🤔

Bun is built on Zig and has the ability to transpile, set up, and run TypeScript and JavaScript projects. It is a full utility since it also functions as a package manager. That’s why it’s referred to as all-in-bun. This has been made possible via the usage of Zig, a dated programming language that was initially created for video games.

Notably, a bun produces another ***bun.lockb*** file, which is not comparable to a standard typical *yarn.lock* or *package-lock.json* file. The lock file that goes along with it is produced in binary. Exactly why? due to performance-related factors. This can make it difficult to track changes in common PRs.

### Performance 🏃‍♂️

People now refer to it as blazingly fast instead of just fast.

What could be better than a detailed examination of some of its benchmarks in comparison to NodeJs and Deno:

#### Comparison of React’s server-side rendering *:*

![SSR render comparison](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621325953/r_s3xd3iy.png align="left")

In SSR of React, Bun is unquestionably more than **3 times faster** 🚀 in handling http requests.

#### Comparison in terms of Hashing :

![Hashing render comparison](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621327664/SsQbDtlsr.png align="left")

Bun has a staggering **6.3 times higher average** 😮 query throughput than deno and nodeJs, respectively.

### Support ⛷️

Numerous Node.js and Web APIs, such as fs, path, Buffer, and others, are natively supported by Bun. This means that many npm packages already in use will be run by bun.

![Bun Node Deno meme](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621329518/jXPSOfbqq.jpeg align="left")

Through improved, more user-friendly tooling, Bun wants to run the majority of JavaScript outside of browsers, increasing infrastructure complexity and speed.

* **TypeScript with JSX?** It will work. (even .tsconfig support).
    
* Bun **loads.env files** for you automatically.
    
* **Node modules?** No issue.
    
* There are built-in web APIs like **fetch** and **WebSocket**
    
* **Run a test?** We possess it. It’s also quick.
    
* **Package manager?** It soars.
    

### Getting started 🎬

Run this [install script](https://bun.sh/install) in your terminal to install Bun. From GitHub, Bun is downloaded.

```yaml
curl https://bun.sh/install | bash
```

![Bun install](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621331234/Bl-q-ehwe.png align="left")

### Create a react app 🔨

Run the command below to create a react app right away.

```yaml
bun create react bun-app
```

![react app bun](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621333236/QzVPjdhrg.png align="left")

It will create a new directory with the name of your app. To start the app run the following command

```yaml
cd your-app-name  
bun dev
```

![bun dir](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621334942/mg6wjJpgN.png align="left")

![bun dev](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621336649/kkxEK6qBj.png align="left")

### Build production bundle for react app 🏗️

React-scripts is not included by default with Bun, therefore you must first install it.

```yaml
bun a react-scripts -d
```

It is set up in this place as a dev dependency.  
Run the subsequent command to create the production bundle after that.

```yaml
bun react-scripts build
```

![bun react app](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621338985/qGuKw3ZiLu.png align="left")

The production bundle will be created when you issue the aforementioned command, and it will be saved in the `build` directory.

### Adding `scripts` to your package.json 📜

The scripts listed below can be included in our package.json file.

```yaml
{  
  "scripts": {  
    "start": "bun dev",  
    "build": "react-scripts build"  
  }  
}
```

To launch the app, issue the following command.

```yaml
bun start
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621340759/eSQgcawm8.png align="left")

And to create the production bundle, we may issue the following command.

```yaml
bun run build
```

### App ✨

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621342989/EtgJzNtDB.png align="left")

### Bonus 💰

> Bun builds react apps by default with javascript, however typescript can be used by simply changing the file extension from .jsx to .tsx.

### Conclusion 💭

It’s admirable that Bun.js has lofty goals for the future. Although it is currently too early to declare that it will replace Node.js, that is its intended replacement. Although Bun.js performs insanely, it tries to replace a lot of tools at once, which puts a heavy pressure on the Bun.js developers. Additionally, Zig is not a very well-known programming language, making it difficult, in my opinion, to find a contributor.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1661621344818/i6CX33wrS.jpeg align="left")

It will take years for Bun.js to mature and become a technology that we can use in production applications because it is still too new and immature. Even so, it has a lot of potential.

### Github URL for the app 💻

[**GitHub - devangtomar/bun-app**  
\*Contribute to devangtomar/bun-app development by creating an account on GitHub.\*github.com](https://github.com/devangtomar/bun-app)

### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on [Dev.to](http://Dev.to): [devangtomar](https://dev.to/devangtomar)