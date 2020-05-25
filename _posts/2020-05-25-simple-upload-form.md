---
layout: post
title: Magic Video Upload URL's
tagline: A simple upload form generator that allows you to collect video submissions organized by source.
---
Often it's useful to be able to provide others with a quick upload link to your video host (i.e., Vimeo, YouTube, [api.video](http://api.video) 😉).
<!--more-->
<br/>
<br/>
- Customer service reps who would like the customer to record and upload the issue with their phone.
- Schools that want to provide teachers with a way to upload lectures to their LMS (Learning Management System)
- Grandparents who want to be proactive instead of waiting until their kids "get around" to sending videos of the grandkids.

<br/>
However, It would not be enough to simply provide a third-party upload link. In each of these cases (except, perhaps the last), we need a way to organize the videos based on their upload source. For example, the school will want to be able to filter (either programmatically or with a UI) the videos based on the teacher who uploaded them.

Similarly, the customer service rep will need a way to identify which customer-uploaded which videos.

Here's my solution (also available at [this link](https://enigmatic-harbor-87060.herokuapp.com/)). You will need a free [api.video](http://api.video) account. It takes less than a minute to sign up if you don't yet have an account.
<br><br>

---

<br>
<div style="background-color: #0066cc; padding:10px;">

<div style="position: relative; display: flex; justify-content: center; width: 100%; min-height: 100px; height: 930px;"><div style="position: absolute; left: 0px; top: 0px; width: 100%; height: 100%; border-radius: 1px;"><div style="height: 100%; width: 100%;"><iframe src="https://enigmatic-harbor-87060.herokuapp.com/" frameborder="0" sandbox="allow-scripts allow-popups allow-top-navigation-by-user-activation allow-forms allow-same-origin" allowfullscreen="" loading="lazy" style="position: absolute; left: 0px; top: 0px; width: 100%; height: 100%; border-radius: 1px; pointer-events: auto; "></iframe></div></div></div>

</div>
<br>

---

<br>
After hitting submit you will get a URL that looks something like this:
<br><br>
<div style="background-color: #ff9900; padding:10px;">

<img src="/images/Untitled.png" alt="">

</div>
<br>
Anyone visiting that URL will see the following form:
<br>
<br>

---


<br>
<div style="background-color:#ccccff; padding:10px">

<div style="position: relative; display: flex; justify-content: center; width: 100%; min-height: 100px; height: 800px; "><div style="position: absolute; left: 0px; top: 0px; width: 100%; height: 100%; border-radius: 1px;"><div style="height: 100%; width: 100%; "><iframe src="https://enigmatic-harbor-87060.herokuapp.com/upload/d6832ghoef9p9p91tatujqu99e" frameborder="0" sandbox="allow-scripts allow-popups allow-top-navigation-by-user-activation allow-forms allow-same-origin" allowfullscreen="" loading="lazy" style="position: absolute; left: 0px; top: 0px; width: 100%; height: 100%; border-radius: 1px; pointer-events: auto; "></iframe></div></div></div>

</div>
<br>
By clicking "Choose File," users can choose a video on their file system or take one on the spot if they are on a mobile device.

Any videos uploaded using this form will show up in your account, tagged with the tag you chose when creating the upload link. 

Guess what? I created this form with the tag `source: blog post`, so any videos uploaded here will show up in my account tagged accordingly. I know I'm asking for trolling here. 😐 Go easy.

You can filter your videos by tag using the web UI at [go.api.video](http://go.api.video) or via the API at the /videos endpoint by setting the `tags` parameter. See the docs [here](https://docs.api.video/5.1/videos/list-videos).

For example, over here, I am taking a look to see which videos were uploaded from each source where I shared this article. I want to know which platform has the most trolls.
<br>
<br>

---


<br>
**This post**
<br>
<br>
<div style="background-color: #9999ff; padding:10px;">
<img src="/images/Screenshot_2020-05-20_at_4.34.11_PM.png" alt="A%20simple%20upload%20form%20generator%20that%20allows%20you%20to%20%20e12901ecdf35411aba1daf2e591e34a3/Screenshot_2020-05-20_at_4.34.11_PM.png">
</div>
<br>

---

<br>
**Hacker Mews**
<br>
<br>

<figure class="aligncenter" style="background-color: #003399; padding:10px; ">
<img src="/images/Screenshot_2020-05-20_at_4.37.28_PM.png" alt="A%20simple%20upload%20form%20generator%20that%20allows%20you%20to%20%20e12901ecdf35411aba1daf2e591e34a3/Screenshot_2020-05-20_at_4.37.28_PM.png" style="width: 100%;">
</figure>
<br>

---

<br>
**Product Hunt**
<br>
<br>
<div style="background-color: #ff9900; padding:10px;">
<img src="/images/Screenshot_2020-05-20_at_4.38.05_PM.png" alt="A%20simple%20upload%20form%20generator%20that%20allows%20you%20to%20%20e12901ecdf35411aba1daf2e591e34a3/Screenshot_2020-05-20_at_4.38.05_PM.png">
</div>

<br>

---

<br>
You can embed the generated form on any website using an embed service such as Embedly. 

In this case, I am using notions built-in video embed service. 

You can also share the link with as many people as you want. It can be reused indefinitely. If this becomes an issue, you need only refresh your API key on your [api.video](http://api.video) dashboard, and videos will no longer be uploaded to your account.


---

<br>
That's all, folks! I hope you enjoyed reading this half as much as I enjoyed writing it.

If you have any questions or comments, hit me up on [twitter](https://twitter.com/codegician) or shoot me an [email](mailto:yitzi@api.video).

See you next time!

Yitzi G.
