---
layout: post
title: RESTful API Explained
description: >-
  We’re pretty familiar with the REST standard, and feel fairly confident
  answering this question. Our product, api.video was developed on…
author:
  name: "Doug Sillars"
  url: "https://twitter.com/dougsillars"
twitter:
  username: dougsillars  
date: '2018-05-21T20:52:40.563Z'
categories: []
keywords: []
slug: /@api.video/restful-api-explained-e28c0e157c23
---

We’re pretty familiar with the REST standard, and feel fairly confident answering this question. Our product, [api.video](http://api.video) was developed on the REST standard, chosen so that our API can scale rapidly and utilize the cloud to facilitate immediate playback no matter the device or platform. So, what exactly is a RESTful API and why are they so popular?

A RESTful API is a standard approach to creating a web service communication protocol. REST stands for Representational State Transfer, but just what exactly does that mean? What are we transferring and what is being represented? In this scenario we are using a representation of a resource to transfer a resource state living on a server to an application state on the client slide. To put it even more simply, RESTful APIs work by accessing data when requesting services, a function that makes them perfect fit for a public facing API operating on the Internet, and why over 70% of public APIs were developed using the REST architectural style.

Now that we understand what a RESTful API, let’s dive a little deeper. Just how exactly does a RESTful API work? Luckily for you and for us, REST web service instructions operate under the hypertext transfer protocol, also known as HTTP. Very briefly, HTTP serves as the foundation of communication on our internet. It functions as a request-response protocol in the client-server computing model, i.e a client (web browser, web crawler, mobile apps, software) submits a request message to the server (site, service, computer), and the service responds in return with a response message or resource. Sound familiar? Well it should, since that’s exactly how RESTful APIs operate!

Even better for the lazy or perhaps enterprising developer, is that RESTful APIs use the same instructions as HTTP. This means less learning and more coding. As mentioned in other answers, these instructions and their corresponding operations include:

**POST** - Create

**GET** - Read

**PUT** - Update/Replace

**PATCH** - Update/Modify

**DELETE** - Delete

One more thing to keep in mind: As per the RE**S**T (Representational **State** Transfer) architecture, the server does not store any sate about the client session and vice-versa. This means that the operations function on a stateless protocol, meaning that when the sender (client) transmits a packet to the receiver (server), the sender does not expect an acknowledgement of receipt, in other words, the system doesn’t maintain information about the session during its life. Due to their stateless nature, REST APIs have proven to be highly adaptive in cloud based applications.

**In summary,** RESTful APIs are an architectural standard for developing a web service. They operate using the same instructions as HTTP and are inherently well suited for the Cloud. These characteristics are the reason why RESTful APIs make up over 70% of all public APIs on the internet.