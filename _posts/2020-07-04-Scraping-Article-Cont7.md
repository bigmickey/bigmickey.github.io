---
layout: post
title: "Continuing the Web-Scraping Article"
date: 2020-07-04
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

```js
    request({
      method: 'GET',
      url: 'https://cryptowat.ch/'
    }, (err, res, body) => {
      if (err) return console.error(err);
```

Within the request method, we now have Document Object Model (DOM) representing the whole page in our variable called body. So what can we do with that? To make it useful, we ask Cheerio to process it for us:
```js
      let $ = cheerio.load(body);
```
So far, so good but what will cheerio do for us? One of its most useful features is to make a (apparently jQuery-like) search to return useful parts of the DOM. Let's do a quick example:
```js
      let title = $('title');
      console.log(title.text));
    });
```
Note that now that we have something remotely useful, I have closed the request function so that we can execute or code. Add all the code so far to a file called scrapeBTCPrice.js and in the same directory, execute using node like this:

    node scrapeBTCPrice

If everything goes as planned, you should see 'Cryptowatch \| Your Trading Terminal' printed on the console.

### Getting to the Price
The bitcoin price we want to scrape is shown in the screenshot below.
![Bitcoin price on cryptowatch]({{site.url}}/assets/images/BitcoinPriceOnCryptowatch.png){:class="img-responsive"}

To figure out how to pull the price out of the webpage, we need to take a closer look at it. To do this, navigate to [cryptowat.ch](https://cryptowat.ch) and pull up your browser's developer tools. I am using the Brave browser and I do this by clicking on the menu at symbol (three horizontal bars) at the top right and selecting More Tools --> Developer Tools. This will bring up a new pane showing all the underlying HTML used to create the page. What's more, in Brave, as you mouse-over different HTML elements, the corresponding part of the webpage is highlighted which makes picking out the HTML we need really easy as you can see in this screenshot:

![Picking out the price HTML]({{site.url}}/assets/images/ShowingHTMLBreakdown.png){:class='img-responsive"}

If you drill down to where the price is located in the page you will see that it is contained in this link:

```html
<a class="_1roDdymkPS2zplXEDcBm0L _3z3AqahoD2pN2R7vFue-0o pointer" title="Bitcoin" href="/assets/btc" data-testid="list-row">
  <div class="text-center _2yv_NtK1R_FBVWqrvRdgcN _2jRRJJvarKXJGP9oRP-Bv0 _2eU06SRnF8jtz1L2K41BsV">2</div>
  <div class="text-left _2yv_NtK1R_FBVWqrvRdgcN _2jRRJJvarKXJGP9oRP-Bv0 _1TuQ_Cac70IaRi6hBmwL9">
    <i class="crypton sym-default-s sym-btc-s _3fjTNyT8S3oN5Xib_Ru5mn"></i>BTC</div>
  <div class="text-left _2yv_NtK1R_FBVWqrvRdgcN _2jRRJJvarKXJGP9oRP-Bv0 _2eU06SRnF8jtz1L2K41BsV">
    <i class="crypton sym-default-s sym-btc-s"></i>Bitcoin</div>
  <div class="text-right _2yv_NtK1R_FBVWqrvRdgcN _2jRRJJvarKXJGP9oRP-Bv0 _1TuQ_Cac70IaRi6hBmwL9">
    <span class="price">9082.93</span>
  </div>
  <div class="text-right _2yv_NtK1R_FBVWqrvRdgcN _2jRRJJvarKXJGP9oRP-Bv0 _1TuQ_Cac70IaRi6hBmwL9">2.727B</div>

  ...

</a>
```

### Installing Node.js and Cheerio

Node is runtime environment that allows you to execute Javascript code. It is based on the Javascript engine from the Google Chrome browser. Installation instructions can be found [here](https://nodejs.org/en/download/)

You can test your installation by running

node -v

which will display the version of node that has been installed. Node also comes with its own package manager, npm. Check which version of this has been installed by running 

npm -v

Cheerio is a Node module for handling HTTP requests and responses. You will npm to install it as described [here](https://www.npmjs.com/package/cheerio)
