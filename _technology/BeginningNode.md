---
title: "Beginning Node"
date: 2021-06-05
category: technology
headline: "Exploring the book Beginning Node.js, Express and MongoDB Development"
---

Initial Explorations with Beginning Node.js

### Introduction
Next up on my journey to find easy ways to build websites is the book Beginning Node.js, Express and MongoDB Development. Each chapter in the book includes an exercise to use a new aspect of the technology and builds to a usable blogging website. I just started so this post focuses on what I learned in chapter 1.

### First Shock
This isn't the very first time I have looked at Node so I wasn't surprised that the first execise is to use the Node http package to create and run a webserver. If you are interested, the code is succinct:

```js
    const http = require('http')
    const server = http.createServer((req, res) =>{
      console.log(req.url)
      res.end('Hello Node.js')
})

    server.listen(3000)
```

This creates a webserve which can be started by executing

    node index.js

in the directory where the index.js file is located. You can then navigate to http://localhost:3000 to see the website thus created saying Hello Node.js. The URL is echoed on the command line. It was when observing this that I noticed another resource was silently being requested - /favicon.ico. Where did this come from?

A quick search reveals that many modern browsers automatically make a request for /favicon.ico which, if supplied, will be displayed in the URL bar to the left of the current URL. Armed with this new knowledge I found [a site](https://favicon.io/favicon-generator/) that will turn text into a favicon.ico file. I downloaded my .ico file and placed it in the same directory as index.js then re-started the websever hoping that it would automatically serve the file but no joy. I guess I need to change the code to server the icon when requested but that exceeds my JS knowledge at the moment so I will just continue with the book for now.

Thanks for reading!

