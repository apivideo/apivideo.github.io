---
layout: post
title: Live Streaming a video using just the browser
description: >-
 You don't need Zoom or any fancy software to stream live video - just Chrome or Firefox!
date: '2020-04-06T20:52:40.563Z'
categories: []
keywords: []
slug: 
---


## Live Streaming a video using just the browser

The tech world has been pivoting to being ‘video-first’ for several years, with many companies being 100% remote,and everyone communicating digitally.  This spring, the rest of the world was involuntarily thrown into not just “video-first” but “video-only.”  Schools, universities, and millions of companies are being forced to quickly embrace video as their primary means of communication.

While there are many tools that can be used for video streaming - wouldn’t it be great if we could just use our browser?  We at [api.video](https://api.video) wanted to show that it was possible!  In this post, we will walk you through the steps to start streaming right form your browser!

## Hosting the video

We’ll be using  [api.video](https://api.video) to host the video (big surprise there, right?). The first step is to create a free account account.  Head over to [api.video](https://api.video) and press “Start” in the upper right corner to create your account.

Once you have created your account, you will be redirected to the dashboard.  In this walkthrough, we are creating a livestream, and we could use our API to do this (here’s a [tutorial how](https://docs.api.video/5.1/videos-and-streaming/livestream-tutorial), but today we’ll just push the big gray button at the top of the page:
![Screenshot of the api.video dashboard](https://apivideo.github.io/images/livestream_dashboard.png)

This will create a livestream, and let you name it.  This will create a new livestream. Click the image of your livestream, and scroll to the bottom of the page:

![Screenshot of the api.video livstream](https://apivideo.github.io/images/livestream_livestreamdetails.png)

In the image above I’ve highlighted a few regions.  In the red box are several options:
Enable recording: saves each of your live streams to be watched on demand later. (we’ve built a [demo tool](https://glitch.com/edit/#!/twilight-decorous-mail?path=README.md:1:0) to help you organize your streams and recordings here).  
Thumbnail: Upload an image to replace the placeholder background image.

The orange box is highlighting is the url of the video.  If you share this (or the iframe url just offscreen), your viewers can watch your live stream.

Finally, in purple is the RTMP stream.  You need this to tell the browser where to send your video for broadcasting (we’ll use this in a second).  

Congratulations! You’ve finished the hardest part in setting up your stream!


## Streaming!


Open  [https://livestream.streamclarity.com](https://livestream.streamclarity.com) in your browser.  This page is where you will stream from. We need to update the form:

![Screenshot of the live browser stream page](https://apivideo.github.io/images/livestream_form.png) 

Size: the width and height of the video you will be broadcasting (start small - we’ll discuss why in a moment). 
Frame rate: frames per second captured by your webcam.
RTMP destination:  Paste in the url in the purple box.
That’s it!  Now we are set to stream:

Click “Connect Server”, then “Start Streaming.”  You’ll see your video appear on the page, and a bunch of text running through the text window.  You’re streaming - and in about 20s, your live stream will begin playing for your viewers on the playback link.  

When you are done - press Stop Streaming, and the stream will stop.  Pretty easy, right?

Dimensions
 Why are the initial dimensions so small?  Each pixel you send is uploaded to the server and processed in real time.  The more pixels you send - the better your internet connection needs to be.  If there is a delay in video delivery - the stream could fail - ending your live stream.

If you know you have a fast connection, by all means, increase the size of the video you send.  

The next issue to think about is the tool processing your video.  The video is transcoded by FFMPEG, and since we want to keep the video as close to live as possible, we need the transcoder to be running faster than the video is coming in.  In the window at the bottom of the screen, you can see the output from the video encoder, and the speed value needs to be over 1.0. 

![Screenshot of the ffmpeg output](https://apivideo.github.io/images/livestream_ffmpeg.png) 

![gif of fast conveyer belt](https://giphy.com/gifs/cheezburger-chocolate-candy-bSJB8Ju3063qU)

Conclusion
And that’s it!  We CAN livestream from the browser.  The code running the website is available on [GitHub](https://github.com/dougsillars/browserLiveStream), so feel free to fork the code and build your own livestreaming website!  Have fun streaming video across the web with no added software!  If you have any questions or concerns, please reach out via our [online community](https://community.api.video)
