---
title: "Using GitHub Pages and GitHub Actions to Deploy a React App ✨"
datePublished: Sat Dec 10 2022 14:36:47 GMT+0000 (Coordinated Universal Time)
cuid: clbj0cw0102kxj9nv2lqycgvf
slug: using-github-pages-and-github-actions-to-deploy-a-react-app-9f679b5e256b
canonical: https://medium.com/@devangtomar/using-github-pages-and-github-actions-to-deploy-a-react-app-9f679b5e256b
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1670741507265/A15hYPevW.png
tags: github, react, reactjs, github-actions, githubpages

---

#### A straightforward method to hosting your single-page application.

### Getting started 📰

Let’s begin with a common ground. To begin, we’ll use the Create React App feature to create a React app and then add the code to a GitHub repository. To create this sample React app, I used the following command.

npx create-react-app --template typescript

At this time, your project directory should resemble the image below. I haven’t changed or added anything — these are the files and directories that are created by default when we run the `npx` command. I just tested it locally by using the command `npm run start` and that is it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670741497664/pWTvC5b8D.png align="left")

### Deploying to GitHub pages ⚓

Create React App places the production files in the build directory when we run the command `npm run build`. However, if you examine the`.gitignore` file, you’ll notice that the `build` directory has been added to this list, prohibiting you from committing the contents of this folder to GitHub. So, how do we get our app out there?

### GitHub Actions 🎬

Let [GitHub Actions](https://docs.github.com/en/actions) come to our aid! Every time we commit code, we need to create our app, which is where GitHub Actions comes in. Create a YAML file called `build-deploy.yml` in your app’s `.github/workflows` directory. Copy and paste the following into this YAML file.

Here’s the `build-deploy.yml` :

This YAML file defines the GitHub Actions workflow. When a change is made to the main branch or a pull request is created to merge changes to the main branch, this workflow will build the React app and deploy the contents of the `build` directory to the `gh-pages` branch.

A little word on `${{ secrets.GITHUB_TOKEN }}` — GitHub generates a `GITHUB_TOKEN` secret for you to utilize in your workflow. It includes write access to the repository, allowing you to update the `gh-pages` branch. The whole list of permissions can be found [here](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#permissions-for-the-github_token).

Commit this file to your repository if you’re following along. You’ll see right away that GitHub Pages is now building based on what’s in your workflow file. If you go to the GitHub Actions tab, you’ll see your workflow being executed and, hopefully, recognized as successful after some time. Feel free to explore this section of your GitHub repository by clicking around in the UI.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670741499126/as9kS0ucPL.png align="left")

Given the successful status, this procedure would have also generated a new branch called `gh-pages` and deployed the production-ready code there.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670741500692/1GiGa_mN-.png align="left")

Isn’t it simple? 🐣

### GitHub Pages 📃

Now that we’ve moved our build files to a new branch, let’s enable GitHub Pages. Scroll down to the GitHub Pages section after selecting Settings from the menu.

We’ll configure the location of our website’s contents here. Because our build files are pushed to the `gh-pages` branch, select it from the menu. Save the file by clicking the Save button. The website will refresh, and when you return to this part, you will see a URL. To view the website, go to that URL.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670741502199/nioSF-Wgk.png align="left")

What exactly happened? Can you view the output of the React app?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670741503614/qZ06_KhqN.png align="left")

You may notice an empty screen and a slew of errors if you open the console.

> **Tip :** If you don’t see an empty screen and instead see a 404 error from GitHub, please wait a few minutes, try a different browser, and then clear the cache. Because this is your first visit to the site, it is possible that things in the background have not yet been updated.

### Setting the homepage value ⚙️

Open up the source code for this app, and in the `package.json` file, add this key-value pair. Replace the parts in the URL below as appropriate.

"homepage": "https://.github.io//",

In my instance, this is what I had to add:

"homepage": "https://devangtomar.github.io/gh-pages-react-app/",

Give it a minute or two, then return to the website. Your React app should now be operational. You can visit the one I hosted [here](https://github.com/devangtomar/gh-pages-react-app).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670741505748/-adWb45zd.png align="left")

> Hooray! 🥳🍾

### GitHub repo for this article 💻

[**GitHub - devangtomar/gh-pages-react-app: Using GitHub Pages and GitHub Actions to Deploy a React…**  
\*This project was bootstrapped with Create React App. In the project directory, you can run: Runs the app in the…\*github.com](https://github.com/devangtomar/gh-pages-react-app)

### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on [Dev.to](http://Dev.to): [devangtomar](https://dev.to/devangtomar)