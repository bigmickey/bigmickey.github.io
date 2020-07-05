---
title: "Continuing the Web-Scraping Article"
date: 2020-06-29
category: Journal
---

Scraping the Current Bitcoin Price using Javascript with Cheerio

## Introduction
This article will take you step-by-step through scraping the bitcoin price using Javascript on node.js and a clever HTTP-processing module called Cheerio. If you haven't yet installed node or Cheerio please see the links at the end of the article for details on how to do that.

... body of artcle ...

We will take the current bitcoin price from the webpage located at cryptowat.ch and the first thing we must be able to do is grab that page so that we can scrape it. Fortunately, Cheerio makes this a piece of cake. Before we do anything else, we tell node.js about the modules that we want to use - one that is in-built called Request and, of course, Cheerio:

    let request = require('request');
    let cheerio = require('cheerio');

do the last two lines look like code?


## Installing Node.js and Cheerio

Node is runtime environment that allows you to execute Javascript code. It is based on the Javascript engine from the Google Chrome browser. Installation instructions can be found [here](https://nodejs.org/en/download/)

You can test your installation by running

node -v

which will display the version of node that has been installed. Node also comes with its own package manager, npm. Check which version of this has been installed by running 

npm -v

Cheerio is a Node module for handling HTTP requests and responses. You will npm to install it as described [here](https://www.npmjs.com/package/cheerio)
