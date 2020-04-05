---
layout: post
title: Adding Chapters to Your Videos
description: >-
  Chapters can help your viewers quickly navigate through longer form videos.
date: '2020-04-03T20:52:40.563Z'
categories: []
keywords: []
slug: /@api.video/restful-api-explained-e28c0e157c23
---


## Video Chapters

When uploading a long video, it can be hard for your viewers to scan to the area of the video they are interested in.  Rather than chop your video into smaller segments (and breaking up the continuity of the entire video), you can use chapters to denote placeholders in your video so that your viewers can ‘skip ahead’ or ‘skip back’ to pertinent sections that they want to watch again.

As an example for this post, I’m going to share a video my daughter made for her astronomy class.  In order to show the distance from the sun to the various planets in the Solar System, she used her GPS and walked through our neighborhood placing the planets.  The distance between each planet was scaled based on the size of the sun in her model.  It is a good study of logarithmic distances:

![Image of the solar system](https://apivideo.github.io/images/chapters_planets.png)

### The video was 35 minutes long. 
We knew that her teacher would not watch this, so we edited the video so that all of the walking bits were 3x faster than when she was standing at each planet.  It was still 13 minutes long.  This seemed like a prime example of a video suited for chapters, since it was hard to know when a planet was being placed. 

Chapters!

Chapters are markers that appear in the video timeline, and help the viewer see different sections of your video.

![Screenshot of a video with chapters](https://apivideo.github.io/images/chapters_videoscreenshot.png)

In this screenshot, we can see that we are at the “Saturn” section in the video, both from the content on the screen, but also by the annotation on the playback bar. We can also guess that the next chapters are for Uranus, and the last chapter is marking Neptune. (The chapters for the closer-in planets are under the playback bar)

How do we add chapters?  With api.video, we simply create a VTT file  (the same format that is used for [captions](https://apivideo.github.io/2020/03/06/@api.video-how-to-add-captions-to-your-videos-19eba225a4f8.html) with time markers and names for each chapter.  In my daughters video, we only named the sections near the planets and left the time traveling space blank:

![Image of a VTT file](https://apivideo.github.io/images/chapters_vtt.png)

I ran the VTT file through a [VTT validator](https://quuz.org/webvtt/) to ensure all the formatting was correct, and then  uploaded to api.video using the api command:

```bash
curl -X POST https://ws.api.video/videos/vi16NDdXmGxk5QSggW54qw0v/chapters/en  -H 'Authorization: Bearer {access_token}' -F file=@/path/to/planets.vtt
```
AFter the /video/ path in the URL os the videoId that the captions are associated with, and the en and the end means that they are in english.  I used my access token [read about how to get your api.video access token](https://docs.api.video/5.1/videos-and-streaming/Authentication-tutorial), and then finally the path the to planets.vtt file on my local computer.  

That’s it!  Frankly, the chapter markers on the playback timeline show the logarithmic nature of the distances in the solar system almost as well as my daughter’s video

<iframe src="https://embed.api.video/vod/vi16NDdXmGxk5QSggW54qw0v" width="100%" height="100%" frameborder="0" scrolling="no" allowfullscreen=""></iframe>

Conclusion:

For longer videos, your viewers might be interested in skipping to different sections of the video. Providing chapter markers makes this easier for them. What are your experiences with adding or using chapters in videos?  Leave us a note in our [developer community](community.api.video) to let us know!
