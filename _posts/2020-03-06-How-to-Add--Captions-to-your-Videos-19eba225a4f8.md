---
title: How to Add  Captions to your Videos
layout: post
author:
  name: "Doug Sillars"
  url: "https://twitter.com/dougsillars"
twitter:
  username: dougsillars
description: >-
  Videos are a compelling way to share experiences with your customers. The
  combination of speech, sounds, images and movement allow us to…
date: '2020-03-06T22:25:35.689Z'
categories: []
keywords: []
slug: /@api.video/how-to-add-captions-to-your-videos-19eba225a4f8
---

<!--more-->

![](https://cdn-images-1.medium.com/max/800/1*rvPreCBsGA-po5W6JOZGuw.png)

Videos are a compelling way to share experiences with your customers. The combination of speech, sounds, images and movement allow us to share a more enriching experience.

However, on the web a video can only be autoplayed when it is muted. As a consumer with small children, this is often a blessing: the last thing I want is a website to wake up a sleeping baby. But as a developer, I want everyone to experience everything my videos have to offer, so I want to work around this issue (but of course, while still letting everyone’s babies nap!)

One solution is to add captions. Users can still engage with your video and follow along with the dialogue. Facebook finds that [videos with captions are watched 12%](https://instapage.com/blog/closed-captioning-mute-videos) longer than videos without captions (85% of Facebook videos are watched without audio). Longer video watch time increases [your search rank](https://www.3playmedia.com/2018/12/10/7-ways-video-transcripts-captions-improve-seo/), and the presence of a captions file even improves your site SEO! With all of these advantages, the accessibility improvements of your website almost come as an afterthought.

No matter the reason you choose to add captions to your videos — you are probably wondering how it is done!

### The VTT File

Closed captioning is typically done with a VTT (Video Text Track) file. They=se are text files that simply list the text that should appear over a specified period:

> WEBVTT

> 1

> 00:00:15.000 → 00:00:17.951

> At the left we can see…

> 2

> 00:00:18.166 → 00:00:20.083

> At the right we can see the…

In the example above, from 15–17.9 seconds, the text “At the left we can see” will appear on the screen, followed a split second later by “at the right we can see.” It is really a pretty straightforward format. But other than manually transcribing your video, how can you create a VTT file?

Let’s walk through 2 ways:

### VTT Creator

[VTT Creator](https://www.vtt-creator.com/) is a web based tool. You simply upload your video, and as it plays the video back, it creates captions for you.

![](https://cdn-images-1.medium.com/max/800/0*0EV4F_2lV2epjlaB)

The website uploads your video and begins the analysis, and the pane on the left fills with the subtitles

![](https://cdn-images-1.medium.com/max/800/0*XTOA3ZQoSjDk3InB)

You can download the VTT, and you’re good to go!

### Google Speech to Text

Google Cloud, Azure and AWS all have a speech to text tool. I chose Google’s for this demo, but they all operate in much the same way.

Google has a helpful [QuickStart](https://cloud.google.com/speech-to-text/docs/quickstart-client-libraries#client-libraries-install-nodejs) guide to set up your Google Cloud account for Speech to Text. The first step is to use ffmpeg to strip the audio track (there is no need to upload the video track when doing audio analysis).

I used their Node.js code example with a few changes (Code available on [GitHub](https://github.com/dougsillars/subtitles)). The video I was transcribing was over 1 minute long, so I had to host it on a Google Cloud instance. Rather than using:

> // The name of the audio file to transcribe

> const fileName = ‘./resources/audio.raw’;

> // The audio file’s encoding, sample rate in hertz, and BCP-47 language code

> const audio = {

> content: audioBytes,

> };

> …

> const request = {

> audio: audio,

> config: config,

> };

I used:

> const gcsUri = ‘gs://video-text-files/sample.mp3’;

> const audio = {

> uri: gcsUri,

> };

There is no need to transcode the video to base64 (as described in the tutorial) if it is hosted on Google Cloud. The sample code from Google writes the transcript into the console:

![](https://cdn-images-1.medium.com/max/800/0*PHDqyWCU_PCA4nR8)

This is super cool, but we want more than a transcription — we need those time stamps. The raw JSON file has an entry for each word with the start and end time for each word:

![](https://cdn-images-1.medium.com/max/800/0*jxIPZw0Mr2CFOVLA)

So I created a function that groups words, using the first word’s start time,and the end time of the last word. The length of the phrase can be varied — in the sample code it is set to 10 words. The script outputs a VTT file to the console.

### Adding Captions to your Video

### HTML5

Adding the VTT file to your video is easy. If you are using HTML5 video, you can add a track attribute pointing to the VTT file.

```html
<video autoplay muted controls>
    <source src=”myvideo.webm”>
    <source src=”myvideo.mp4">
    <track default lang=”en” kind=”captions” src=”myvideo.vtt”>
    <track lang=”es” kind=”captions” src=”muvideo-es.vtt”>
</video>
```
### Video Streaming

If you want to add captions to your [api.video](https://api.video) video, you can use the Captions API.

1.  First you must [authenticate](https://docs.api.video/5.1/videos-and-streaming/Authentication-tutorial) your session to gain an access token.
2.  Determine the videoID of the video you’d like to add the caption to. In this example, I have created captions to [Elephant’s Dream](https://orange.blender.org/) (an Open Source video project). The video ID is: vi5UNyaStzuuj0xTAGp7qtjf

[**api.video**  
_Video Player by api.video_embed.api.video](https://embed.api.video/vod/vi5UNyaStzuuj0xTAGp7qtjf "https://embed.api.video/vod/vi5UNyaStzuuj0xTAGp7qtjf")[](https://embed.api.video/vod/vi5UNyaStzuuj0xTAGp7qtjf)

3\. Make a call to add the caption. Using curl, the request looks like:

> curl [https://ws.api.video/videos/vi5UNyaStzuuj0xTAGp7qtjf/captions/en-US](https://ws.api.video/videos/vi5UNyaStzuuj0xTAGp7qtjf/captions/en-US) -H ‘Authorization: Bearer {access\_token}’ -F file=@/path/to/google.vtt

And we receive a response:

> {“uri”:”/videos/vi5UNyaStzuuj0xTAGp7qtjf/captions/en”,”src”:”https://cdn.api.video/vod/vi5UNyaStzuuj0xTAGp7qtjf/captions/en.vtt","srclang":"en","default":false}

Note that captions are off by default. This is easily resolved by patching the video, setting the default to true. Using curl, this looks like:

> curl -X PATCH [https://ws.api.video/videos/vi5UNyaStzuuj0xTAGp7qtjf/captions/en](https://ws.api.video/videos/vi5UNyaStzuuj0xTAGp7qtjf/captions/e) -H ‘Authorization: Bearer {access\_token}’ -d ‘{“default”: true}’

And we receive a response:

> {“uri”:”/videos/vi5UNyaStzuuj0xTAGp7qtjf/captions/en”,”src”:”https://cdn.api.video/vod/vi5UNyaStzuuj0xTAGp7qtjf/captions/en.vtt","srclang":"en","default":true}

And watching the movie: success! the captions are turned on by default. To autoplay a video with api.video, simply add #autoplay to the end of the url, and we have an autoplaying video with captions.

Now we can rest assured that our videos will likely have more traction, be watched longer, and shared more often. And, we are making our content more accessible to users who cannot hear.

### Conclusion

Video captions not only make your content accessible, but research shows videos with captions are watched longer, and shared more often. And searchable transcriptions actually increase the SEO of your site!

Often there is reluctance to add captions due to the added work, but with just a few clicks of a button, captions can be generated automatically and uploaded for immediate playback.

Give it a try, and share your caption successes in the [api.video community](https://community.api.video/)