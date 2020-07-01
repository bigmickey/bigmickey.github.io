---
layout: post
title: "Continuing the Web-Scraping Article"
date: 2020-07-01
category: Journal
---

Scraping the Current Bitcoin Price using Javascript with Cheerio

### Introduction
This article will take you step-by-step through scraping the bitcoin price using Javascript on node.js and a clever HTTP-processing module called Cheerio. If you haven't yet installed node or Cheerio please see the links at the end of the article for details on how to do that.

### Approach
We will scrape the current bitcoin price from the webpage located at cryptowat.ch. The first thing we must be able to do is grab that page so that we can scrape it. Fortunately, Cheerio makes this a piece of cake. Before we do anything else, we tell node.js about the modules that we want to use - one that is in-built called Request and, of course, Cheerio:

    let request = require('request');
    let cheerio = require('cheerio');

With the request library now available, we can use its functionality to pull the HTTP response from cryptowat.ch like this:

```
    request({
      method: 'GET',
      url: 'https://cryptowat.ch/'
    }, (err, res, body) => {
      if (err) return console.error(err);
```

Within the request method, we now have Document Object Model (DOM) representing the whole page in our variable called body. So what can we do with that? To make it useful, we ask Cheerio to process it for us:

      let $ = cheerio.load(body);

So far, so good but what will cheerio do for us? One of its most useful features is to make a (apparently jQuery-like) search to return useful parts of the DOM. Let's do a quick example:

      let title = $('title');
      console.log(title.text));
    });

Note that now that we have something remotely useful, I have closed the request function so that we can execute or code. Add all the code so far to a file called scrapeBTCPrice.js and in the same directory, execute using node like this:

    node scrapeBTCPrice

If everything goes as planned, you should see 'Cryptowatch \| Your Trading Terminal' printed on the console.

### Getting to the Price
The bitcoin price we want to scrape is shown in the screenshot below.





### Installing Node.js and Cheerio

Node is runtime environment that allows you to execute Javascript code. It is based on the Javascript engine from the Google Chrome browser. Installation instructions can be found [here](https://nodejs.org/en/download/)

You can test your installation by running

node -v

which will display the version of node that has been installed. Node also comes with its own package manager, npm. Check which version of this has been installed by running 

npm -v

Cheerio is a Node module for handling HTTP requests and responses. You will npm to install it as described [here](https://www.npmjs.com/package/cheerio)
