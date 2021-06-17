---
title: "Beginning Node Chapter 3"
date: 2021-06-13
category: technology
headline: "Bug fix for Chapter 3 of Exploring the book Beginning Node.js, Express and MongoDB Development"
---

A Bug Fix for Chapter 3 of Beginning Node.js, Express and MongoDB Development

### Introduction
I am really enjoying working through the examples in the book but I thought I'd share a small bug I found whilst reading chapter 3.

### The Bug
Towards the end of the chapter, we use the Express app to define some routes for GET requests from the browser which serve htmlpages which we have taken from a Bootstrap template and placed in a directory called pages. To accommodate this we are also told to edit index.html which previously had links pointing directly to html pages it expects to be in the root directory. Thus

```js
    <li><a...href="index.html">Home</a></li>
    <li><a...href="about.html">About</a></li>
    <li><a...href="post.html">Sample Post</a></li>
    <li><a...href="contact.html">Contact</a></li>

```
becomes
```js
    <li><a...href="/">Home</a></li>
    <li><a...href="/about">About</a></li>
    <li><a...href="/post">Sample Post</a></li>
    <li><a...href="/contact">Contact</a></li>
```

Clicking on one of the links from the home page will bring you to the correct page but thereafter none of the links work. I realised this is because the html above is repeated in each of the pages that are served (about.html, post.html and contact.html). In order for it to work correctly, you have to make the same edit in each of the .html files. 

Thanks for reading :)

PS I just finished reading Chapter 3 and this 'bug' is pointed out in the closing paragraphs LOL! Still better to have solved it myself - now I think I will appreciate chapter 4 more ...

