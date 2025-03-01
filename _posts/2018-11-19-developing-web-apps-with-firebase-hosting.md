---
id: 2003
title: 'Developing Web Apps With Firebase Hosting'
date: '2018-11-19T18:26:09+00:00'
permalink: /developing-web-apps-with-firebase-hosting/
image: /wp-content/uploads/2018/11/QoYLmO5.png
categories:
    - 'Web Dev'
tags:
    - Cloudflare
    - Firebase
    - Hosting
---

Firebase hosting provides an extremely simple way to deploy JavaScript web apps. Whilst it lacks almost all of the advanced features other hosts have, it does have the major advantage of being free for low-traffic usage. This tutorial will cover creating a basic site, as well as utilising a custom subdomain with Cloudflare.

This post is part of [The Complete Guide to Firebase](/search/?q=firebase/). Throughout this tutorial, you'll need access to the [Firebase Hosting dashboard](https://console.firebase.google.com/u/0/project/_/hosting/main), and the [official documentation](https://firebase.google.com/docs/hosting/) may be useful too.

## Implementation

As always, the entire [Firebase Reference Project is open source](https://github.com/JakeSteam/FirebaseReference), and the hosted code is [available as a repository](https://github.com/JakeSteam/FirebaseHosting). There is also [a pull request](https://github.com/JakeSteam/FirebaseReference/pull/7) for the very minor changes made to the Android reference app.

### Setting up Firebase Hosting environment

1. First [install npm &amp; node.js](https://www.npmjs.com/get-npm), used to handle the Firebase installation process.
2. Next, open a Command Prompt and enter `npm install -g firebase-tools`, after a few minutes you should see something similar to the following image:[![](/wp-content/uploads/2018/11/2.png)](/wp-content/uploads/2018/11/2.png)
3. Next, login to your Firebase account using `firebase login`. This will open a browser with a login request. Once logged in, the Command Prompt will report success.[![](/wp-content/uploads/2018/11/yZ61qY0.png)](/wp-content/uploads/2018/11/yZ61qY0.png)
4. Next, navigate to the directory you want to deploy code from.
5. Enter `firebase init` to initialise a local Firebase project. You will be prompted to choose a service (choose "Hosting"), and a Firebase project to use.
6. Finally, pick a folder to use for your public files (default is "public"), and whether you want a single page web app (this can be changed later).[![](/wp-content/uploads/2018/11/NA55Gff.png)](/wp-content/uploads/2018/11/NA55Gff.png)

### Deploying Firebase Hosting site

Deploying your site is very easy, just enter `firebase deploy` and within a few seconds the updated files are published. That's it! The same process is used for the initial deployment as well as all subsequent deployments.

[![](/wp-content/uploads/2018/11/deploy.png)](/wp-content/uploads/2018/11/deploy.png)

### Setting up a custom subdomain with Cloudflare

By default, your project will have a URL like `https://fir-referenceproject.firebaseapp.com/`. However, custom domains / subdomains can be added within a minute or two by following the simple steps displayed when "Connect domain" is pressed.

#### Define custom URL

First, enter your custom URL. I'll be using `https://firebasehosting.jakelee.co.uk`.

#### Verify domain ownership

Next, you need to prove you own the URL. This is done by adding a `TXT` record in your domain's DNS, accessible under the "DNS" tab in Cloudflare.

[![](/wp-content/uploads/2018/11/step2.png)](/wp-content/uploads/2018/11/step2.png) [![](/wp-content/uploads/2018/11/step2b.png)](/wp-content/uploads/2018/11/step2b.png)

#### Add `A` records

Finally, you now need to add the actual `A` records that will allow Firebase to serve content for your URL. This is done by adding 2 entries, each with your target subdomain as the "Name", and the specified IPs as the "IPv4 Address".

[![](/wp-content/uploads/2018/11/step3.png)](/wp-content/uploads/2018/11/step3.png) [![](/wp-content/uploads/2018/11/step3b.png)](/wp-content/uploads/2018/11/step3b.png)

## Web interface

Firebase Hosting's very limited function set is easily seen when accessing the web interface. Each tab provides the bare essentials, and sometimes not even that!

### Dashboard

The dashboard displays a list of all connected custom domains, and a list of all releases. Previous releases can be easily rolled back to or deleted, but no information is available about them. As such, an external source code manager like Git will still be essential for development.

[![](/wp-content/uploads/2018/11/dashboard-2.png)](/wp-content/uploads/2018/11/dashboard-2.png)

### Usage

The usage tab shows 2 simple graphs; your storage space used over time, and your data transfer size over time. The free "Spark" plan has a limit of 1GB of storage space, and 10GB/month of data transfer.

[![](/wp-content/uploads/2018/11/usage.png)](/wp-content/uploads/2018/11/usage.png)

## Conclusion

Before judging Firebase Hosting too harshly, it's important to remember that this isn't meant to replace traditional web hosts. Instead, it is intended as an extremely quick &amp; simple way to have a web app live on the internet, with CDN + HTTPS + custom domain, for free. Whilst it absolutely can be used for production-level apps, the lack of any controls may make even the most cutting-edge web developer a little bit hesitant.

Considering the amazingly easy to use deployment process, and the industry standard features offered for free, Firebase Hosting is definitely a contender for quick site prototypes. It can also hook into [Firebase Cloud Functions](/developing-android-apps-with-firebase-cloud-functions/) to handle server / database communication or data transfer with other systems.

I personally will most likely use it next time a simple idea needs testing, and eagerly await being up and running within a minute or two!

Previous: [Developing Android Apps With Firebase Cloud Storage](/developing-android-apps-with-firebase-cloud-storage)