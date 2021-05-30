---
title: "Building A Simple Website"
date: 2021-05-29
category: technology
headline: "Building A Simple Website"
---

Building A Simple Website

### Introduction
I want to explore ways to build and publish websites. I will take a look at some services like Webflow and Carrd but I came across [this approach](https://tinyprojects.dev/guides/tiny_website) recently and decided to give it a try first.

### Going Through The Process
The first part is simple enough - just creating a file called index.html in a directory called public - so far, so familiar. The next step was new to me however - creating a project in Google Firebase. A little Googling revealed that this is a backend framework for building apps. I figured Google wouldn't be the only one in this space and quickly discovered Amazon's competing product, AWS Amplify. Ingtriguing. However since these are primarily app-related products I will save more research on these for another day.

This was enough to warrant starting to write this post and it was then that I learned that Github are deprecating their username / password access from the command line. Now I need to use a Personal Access Token. Another diversion from my little project - but you can find the details [here](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token) if this affects you.

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

Now we know where our price is embedded but how to we grab it? The answer is that Cheerio has a fantastic mechanism for pulling HTML elements out of the DOM. It is modeled after jQuery but as I know nothing about jQuery that doesn't really help me much! Nevertheless, it isn't difficult to grasp how it works. It is best explained with an example.

Remember that in the code above we loaded the entire DOM into a variable called $ using Cheerio's load function. We apply a search function to $ simply by giving it a *selector* to match against. There is a specified set of selectors to use (you can see a list used in jQuery [here](https://www.elated.com/jquery-selectors/)). The result can be empty, a single element or an array of elements depending on what the selector matches within the DOM. We know that the bitcoin price we want is embedded in the link shown above so let's start by pulling the links out of the DOM using the appropriate selector like this: 

```js
    const allLinks = $("a");

    console.log("number of links in DOM = " + allLinks.length);
``` 

If you add those lines to scrapeBTCPrice.js and run it with node your output should look something like this:

```
    Cryptowatch | Your Trading Terminal
    number of links in DOM = 125
```

This is great and we could start looping through our list of links looking for the price but Cheerio can do even better than this. Instead of querying for all links we can note that the particular link of interest has an attribute called title which has the value Bitcoin. Let's use this attribute to pull just our link out of the DOM:

```js
    const bitcoinPriceLink = $("a[title='Bitcoin']");
```

This tells Cheerio exactly which link we want. From here, we can pull the actual price out by noting that it lives in a span element with a css class called price. This is how we use Cheerio and these characteristics to get the price:

```js
    console.log("the current bitcoin price is: " + $(".price", $(bitcoinPriceLink)).text());
```

This needs a little bit of unpacking. ".price" is the selector and tells Cheerio to search for a CSS class with this name however this time we are not applying the selector to the whole DOM. Instead we tell it only to search within bitcoinPriceLink. Once Cheerio has pulled out the HTML element with that CSS class we simply pull out the text of the element which is the current bitcoin price. Hey presto! We successfully scraped the price!

If you enjoyed this, you can find me on Twitter at the handle below. You can also find the code used in this article in [this repository](https://github.com/bigmickey/CheerioWebScrapeExample)
### Installing Node.js and Cheerio

Node is runtime environment that allows you to execute Javascript code. It is based on the Javascript engine from the Google Chrome browser. Installation instructions can be found [here](https://nodejs.org/en/download/)

You can test your installation by running

node -v

which will display the version of node that has been installed. Node also comes with its own package manager, npm. Check which version of this has been installed by running 

npm -v

Cheerio is a Node module for handling HTTP requests and responses. You will npm to install it as described [here](https://www.npmjs.com/package/cheerio)
