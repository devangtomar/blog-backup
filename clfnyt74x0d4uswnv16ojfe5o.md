---
title: "Building a Rotten Tomatoes Web Scraper using Node.js 🕸🍅"
datePublished: Sat Mar 25 2023 10:18:57 GMT+0000 (Coordinated Universal Time)
cuid: clfnyt74x0d4uswnv16ojfe5o
slug: building-a-rotten-tomatoes-web-scraper-using-node-js-26807c48bb8e
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679748369013/8c1bebf7-75f7-4527-af00-104c1ad368e6.png
tags: web-scraping, nodejs-developer, node-js-development, webscrapingservices

---

### **Introduction 💁🏻‍♀️**

Are you tired of scrolling through endless movie reviews on Rotten Tomatoes? Do you wish there was a faster way to find out which movies are worth watching and which ones are better off being skipped? Well, have no fear because we’re about to take a deep dive into the world of web scraping with Node.js, and build our very own Rotten Tomatoes web scraper!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679748356160/e3a8241b-ae4f-4b4e-8132-97e8c5916ab8.jpeg align="left")

These days, I’m learning about web scrapers. So I decided to create a simple cli tool that crawls a small section of the website “[Rotten Tomatoes](https://www.rottentomatoes.com/)” and chooses all of the movie cards on the page, iterating over them and choosing the movie title and score for each one.

If you’re unfamiliar with [Rotten Tomatoes](https://www.rottentomatoes.com/), it’s a website that offers rating and information about movies, TV series, and celebrities. It is a very popular website with a massive information database. As a result, it is a wonderful location to begin learning about web scraping.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679748358873/2223566d-aa7d-4d0a-b446-3e0c133188e6.jpeg align="left")

As you may be aware, creating a web scraper consists of four major steps:

* **Crawling** : Crawling is the process of discovering all of the links on a website and adding them to a queue.
    
* **Scraping :** Scraping is the process of obtaining data from a website.
    
* **Parsing** : The process of transforming raw data into a structured representation is known as parsing.
    
* **Storing** : Storing is the process of storing data in a file or database.
    

And we’ll go through all of them in detail step by step, so buckle up and let’s get started.

### Prerequisites 👩🏻‍🏫

* [**NodeJS**](https://nodejs.org/en/)
    
* [**NPM**](https://www.npmjs.com/)
    

> And also you should have basic knowledge of crawlers and scrapers in general. [Learn here](https://oxylabs.io/blog/crawling-vs-scraping)

### Let us begin then ⚡️

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679748361049/52199dbb-1f15-42c9-84ce-124158f175ce.jpeg align="left")

First things first, you’re going to need to install Node.js if you haven’t already. I recommend doing this while wearing a clown nose and juggling three oranges. It’s important to maintain a sense of humor when doing anything with Node.js, otherwise you might start to take yourself too seriously.

Once you’ve got Node.js installed, you’re going to want to install a few packages using npm. Now, you might be wondering what npm stands for. Does it stand for “Node Package Manager”? Or maybe “Notoriously Painful Middleware”? Honestly, nobody knows. It’s just one of those things that’s best not to question.

So, let’s get down to business. Open up your terminal and navigate to the directory where you want to create your project. Then type:

```javascript
npm init
```

This will create a new Node.js project and generate a package.json file. This file contains information about your project, such as its name, version, and dependencies. You’ll want to make sure to fill out all of the information in this file while wearing a silly hat. It’s important to keep things light-hearted.

Now, let’s install a few packages. Type the following commands in your terminal:

```javascript
npm install request
npm install cheerio
npm install fs
```

The request package is used to make HTTP requests, and the cheerio package is used to parse HTML. Think of it like a really fancy, high-tech blender that turns HTML into data smoothies.

With those packages installed, let’s get to the fun part. We’re going to write some code!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679748363319/db3fd3c0-e045-434b-a875-238c4c594e04.jpeg align="left")

Open up your favorite code editor and create a new file called scraper.js. Now, let’s write some code to scrape Rotten Tomatoes. Copy and paste the following code into your scraper.js file :

```javascript
const request = require('request');
const cheerio = require('cheerio');
const fs = require('fs');

const URL = 'https://www.rottentomatoes.com/';

request(URL, function (error, response, html) {
if (! error && response.statusCode === 200) {
const $ = cheerio.load(html);

// Example: Get the title and rating of the first movie on the homepage
const firstMovieTitle = $('.mb-movie:nth-of-type(1) h3 a').text();
const firstMovieRating = $('.mb-movie:nth-of-type(1) .tMeterScore').text();

console.log(`Title: ${firstMovieTitle}`);
console.log(`Rating: ${firstMovieRating}\n`);

// Example: Get the titles and ratings of all movies on the homepage
const movieTitles = [];
const movieRatings = [];

$('.mb-movie h3 a').each(function (i, elem) {
movieTitles[i] = $(this).text();
});

$('.mb-movie .tMeterScore').each(function (i, elem) {
movieRatings[i] = $(this).text();
});

for (let i = 0; i < movieTitles.length; i++) {
console.log(`Title: ${
movieTitles[i]
}`);
console.log(`Rating: ${
movieRatings[i]
}\n`);
}

// Example: Save the titles and ratings of all movies on the homepage to a file
const data = [];

$('.mb-movie').each(function (i, elem) {
const title = $(this).find('h3 a').text();
const rating = $(this).find('.tMeterScore').text();

data.push({title, rating});
});

fs.writeFile('movies.json', JSON.stringify(data), function (err) {
if (err)
throw err;

console.log('Data saved to file.');
});
}
});
```

This script uses the `request` module to make an HTTP GET request to the Rotten Tomatoes homepage, and then loads the HTML response into a Cheerio instance using `cheerio.load()`. From there, it uses CSS selectors to extract data from the page, such as the title and rating of the first movie, the titles and ratings of all movies on the homepage, and saves the titles and ratings of all movies on the homepage to a JSON file.

You can modify the script to scrape other pages on Rotten Tomatoes or extract different pieces of data by changing the CSS selectors and modifying the data handling logic

Now, let’s run our code. In your terminal, type :

```javascript
node scraper.js
```

If all goes well, you should see the title of the Rotten Tomatoes homepage printed to the console. Congratulations, you just scraped a website using Node.js!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679748364876/bb251517-4a5d-4ac7-ab36-e44d10608e53.png align="left")

Of course, this is just the beginning. There's so much more you can do with web scraping and Node.js. You could scrape reviews for a specific movie, or even build a web app that displays the latest Rotten Tomatoes scores for all the movies currently in theaters. The possibilities are endless.

Just remember to keep things fun and lighthearted. Node.js can be a serious business, but it’s important to not take yourself too seriously. After all, we’re just a bunch of silly humans trying to make sense of a chaotic digital world. So put on your clown nose, juggle those oranges, and let’s build something amazing!

### Conclusion 💭

So there you have it, folks. Building a Rotten Tomatoes web scraper using Node.js. It’s easy, it’s fun, and it’s a great way to learn how to use Node.js to automate web tasks. And if you’re lucky, you might even have a feline coding partner to help you out.

### Warning ⚠️

But before you go off and start building your own web scraper, there are a few things you should keep in mind. First of all, make sure you’re not violating any terms of service or copyright laws. Scraping websites without permission can get you into legal trouble, so be sure to check the website’s policies before you start scraping.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679748366245/9dd031df-57a5-4c17-923e-29718144fac0.jpeg align="left")

Additionally, web scraping can put a lot of strain on a website’s servers. If you’re making too many requests too quickly, you could cause the website to crash or slow down. Make sure you’re being respectful of the website’s resources and following best practices for web scraping.

Finally, remember that web scraping is not foolproof. Websites can change their HTML structure or add anti-scraping measures at any time, which could break your scraper. Make sure you’re keeping an eye on your scraper and updating it as needed to keep up with any changes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679748367522/13e44ccb-1738-4536-87bb-4cc0b13e9618.jpeg align="left")

In conclusion, building a Rotten Tomatoes web scraper using Node.js can be a fun and educational experience. Just be sure to follow best practices, respect the website’s policies, and don’t let your cat take over your coding too often. Happy scraping!

### GitHub repo for the article 💻

%[https://github.com/devangtomar/nodejs-scrapper] 

### Connect with Me on Social Media

🐦 Follow me on Twitter: [devangtomar7](https://twitter.com/devangtomar7)  
🔗 Connect with me on LinkedIn: [devangtomar](https://www.linkedin.com/in/devangtomar)  
📷 Check out my Instagram: [be\_ayushmann](https://instagram.com/be_ayushmann)  
Ⓜ️ Checkout my blogs on Medium: [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)  
**#️⃣** Checkout my blogs on Hashnode: [devangtomar](https://devangtomar.hashnode.dev/)  
**🧑‍💻** Checkout my blogs on [Dev.to](http://Dev.to): [devangtomar](https://dev.to/devangtomar)