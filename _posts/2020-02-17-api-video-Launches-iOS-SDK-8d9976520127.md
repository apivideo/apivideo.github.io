---
title: api.video Launches iOS SDK
description: >-
  api.video removes the complexity from streaming video. Last year, we announced
  our Android SDK, now we are happy to introduce the iOS SDK.
date: '2020-02-17T15:19:35.723Z'
categories: []
keywords: []
slug: /@api.video/api-video-launches-ios-sdk-8d9976520127
---

![iPhone development image [https://www.flickr.com/photos/ramotion/5189385602](https://www.flickr.com/photos/ramotion/5189385602)](https://cdn-images-1.medium.com/max/800/1*ZYvRjWjK-DvvAz_Ww7Nx-A.jpeg)
iPhone development image [https://www.flickr.com/photos/ramotion/5189385602](https://www.flickr.com/photos/ramotion/5189385602)

[api.video](https://api.video) removes the complexity from streaming video. Our simple to use APIs allow you to focus on creating your content, and leaving the video streaming details to us.

Since launching api.video, one of the most common questions we are asked is “do you have mobile SDKs?” Today, we can answer that with a “yes!”

Late last year, we announced our [Android SDK](https://github.com/apivideo/android-sdk), and today we are happy to announce the release of our [iOS SDK](https://github.com/apivideo/ios-sdk). If you have used api.video in the past, you’ll see that all of the features that are available in our APIs are now available as native iOS calls.

If you have never used api.video, imagine a simple API interface to upload, modify, and delete video streams, create custom players, add captions or chapters, and even live stream video — all from the native app. That is the power that api.video (and all of our [SDKs](https://docs.api.video/5.1/sdk-and-tools)) can give you. To get started, read the documentation on [GitHub](https://github.com/apivideo/ios-sdk), and check out the [demo application code](https://github.com/apivideo/ios-demo) (launching this week).

The quick start guide (pulled from GitHub):

### Installation

### Cocoapod

1.  Add the following entry to your Podfile:

> pod ‘sdkApiVideo’

2\. Then run pod install

3\. Don’t forget to import sdkApiVideo in every file you’d like to use api.video sdk

### Quick Start

### 1\. In the AppDelegate.swift instantiate a new Client

> let authClient = Client()

### 2\. In the didFinishLaunchingWithOptions func add the following code

*   If you want to use the production environment, use createProduction method
*   If you want to use the sandbox environment , use createSandbox method

> authClient.createSandbox(key: « YOUR\_SANDBOX\_API\_KEY »){ (created, reponse) in

> }

### 3\. In your ViewController.swift file import the sdk

> import sdkApiVideo

### 4\. Create Variable

> let appDelegate = UIApplication.shared.delegate as! AppDelegate

### 5\. In viewDidLoad func

> self.videoApi = appDelegate.authClient.videoApi

### 6\. Create and upload a video file

> self.videoApi.create(title: «title», description: «description», fileName: «filename», filePath: «filePath», url: «url»){ (uploaded, resp) in

> if(resp != nil){

> print(“error : \\((resp?.statusCode)!) -> \\((resp?.message)!)”)

> }else{

> if(uploaded){

> //Do whatever you want

> }else{

> // Do whatever you want

> }

> }

> }

And that’s all there is to it!

Now you can use all your favourite api.video calls in your mobile app, simplifying the delivery of your videos with one API to apps, browsers and billions of devices around the world.

If you have questions, file an [issue](https://github.com/apivideo/ios-sdk/issues), or reach out to us on [chat](https://api.video).