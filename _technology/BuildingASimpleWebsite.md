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

When the deploy was complete Firebase reported that I could view my simple website here: https://simple-website-1.web.app - as of the time of writing it is still viewable. Go ahead and take a look (fair warning it is very underwhelming!)

The article continues to show how to tie your own domain name to the website but that is an adventure for another day. Thanks for reading.

