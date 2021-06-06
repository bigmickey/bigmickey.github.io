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
This isn't the very first time I have looked in Node so I wasn't surprised that the first execise is to use the Node http package to create and run a webserver. If you are interested, the code is succinct:


This was enough to warrant starting to write this post and it was then that I learned that Github are deprecating their username / password access from the command line. Now I need to use a Personal Access Token. Another diversion from my little project - but you can find the details [here](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token) if this affects you.

### Firebase Setup Issues
The next snag I encountered was trying to run 

    firebase init

after a few moments I received this error message:

    Error: Failed to authenticate, have you run firebase login?

I returned to the Firebase project page and I noticed that it had detected my Google account and I was automatically logged in. So I did as instructed and ran firebase init. This resulted in a request to allow Google to collect information from Firebase CLI (Command Line Interface) which I agreed to. I was then redirected to a webpage warning about the permissions that Firebase CLI was asking for. Once I agreed to these I was successfully logged into Firebase under my Google account. Now I resumed the process with

    firebase init

This time I was presented with:

         ######## #### ########  ######## ########     ###     ######  ########
         ##        ##  ##     ## ##       ##     ##  ##   ##  ##       ##
         ######    ##  ########  ######   ########  #########  ######  ######
         ##        ##  ##    ##  ##       ##     ## ##     ##       ## ##
         ##       #### ##     ## ######## ########  ##     ##  ######  ########

    You're about to initialize a Firebase project in this directory:

      /Users/SimpleWebsite

    ? Which Firebase CLI features do you want to set up for this folder? Press Space to select features, then Enter to confirm your choices. (Press
      <space> to select, <a> to toggle all, <i> to invert selection)
    ❯◯ Database: Configure Firebase Realtime Database and deploy rules
     ◯ Firestore: Deploy rules and create indexes for Firestore
     ◯ Functions: Configure and deploy Cloud Functions
     ◯ Hosting: Configure and deploy Firebase Hosting sites
     ◯ Storage: Deploy Cloud Storage security rules
     ◯ Emulators: Set up local emulators for Firebase features
     ◯ Remote Config: Get, deploy, and rollback configurations for Remote Config

As per the instructions I selected Hosting: Configure and deploy Firebase Hosting sites. The rest of the steps were straightforward with the exception of one additional question to answer that didn't appear in the article:

    ? Set up automatic builds and deploys with GitHub? No

Once complete I executed the final command

    firebase deploy

When the deploy was complete Firebase reported that I could view my simple website here: [https://simple-website-1.web.app](https://simple-website-1.web.app) - as of the time of writing it is still viewable. Go ahead and take a look (fair warning it is very underwhelming!)

The article continues to show how to tie your own domain name to the website but that is an adventure for another day. Thanks for reading.

