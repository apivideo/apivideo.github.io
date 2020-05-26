---

twitter:
  username: codegician
layout: post
title: Creating Unique Video Dashboards for Individual Users Is Easier than You Would Imagine... If You Are Using Api.video😉
tagline: One of the primary sources of frustration for teachers and parents stems from the need for teachers and students to adopt new technology with which they are unfamiliar.
image: /images/teacher.jpg
author:
  name: "Yitzi G"
  url: "https://twitter.com/codegician"
  
---

<picture style=""><img style="" alt="" src="https://images.storychief.com/account_21166/design-desk-display-eyewear-313690_4c94524b088e9f195cac811221aa4664_1000.jpg"></picture>
<br>
If you have kids or know anybody that has kids, then you’ve probably been exposed to the frustration surrounding the rapid and non-optional transition from a classroom learning environment to a remote one.

One of the primary sources of frustration for teachers and parents stems from the need for teachers and students to adopt new technology with which they are unfamiliar.

> Imagine that you are a developer in the booming field of e-learning. Since you are smart, one of your primary goals is to make the interface as self-explanatory and straightforward as possible for teachers and students.

To accomplish that, you may decide that each student or teacher who logs in should, by default, see only videos relevant to them on their dashboard.

Implementing such customization may seem like a herculean task. After all, you’ve got hundreds of teachers and students and thousands of videos.

Don’t fret. It’s quite easy with api.video’s API.

Let’s dive in!

## A Bird’s Eye View

Before looking at any code, let’s restate the problem. I’ll begin with the teacher's use case.

**Problem:** We have many teachers uploading videos, and we want each teacher to see only their videos on their dashboard.

**Solution:** We make use of api.video’s **tagging** feature on our backend.

There are two reasons for this:

- We want to make this as simple as possible. This implementation is entirely invisible to the teachers and requires no action from them, not even a checkbox.
- Having implemented a login on our backend means that we are holding a unique identifier (i.e., username, id) for our logged-in user. That makes tagging and accurate retrieval a breeze.

## Upload

For simplicities sake, let’s assume that students and teachers share a table in our database that looks like this:

```sql
CREATE TABLE users (
    id            SERIAL PRIMARY KEY,
    username      TEXT UNIQUE NOT NULL,
    email_address TEXT,
    password_hash TEXT
);
```

   When a teacher logs in, we query this table to authenticate them. It’s trivial to grab the unique username at the same time.

   Every time the logged-in teacher uploads a video, we include their “username/tag” in the ‘Create video’ request we make to the api.video API.

   When [creating the video](https://docs.api.video/5.1/videos/create-video), you can include tags in the request body like so:

 ```json
 {
  "title": "Maths video",
  "description": "An amazing video explaining the string theory",
  "tags": [
  "einstein"
  ]
 }
 ```

We can take this a step further, allowing the teacher to select which course they are uploading the video to and adding a tag for that as well.

## Retrieving the Users Video’s

Every video is now associated with the unique identifier of the uploader. When a teacher logs into his video dashboard, all we need to do on the backend is to add their unique identifier to the query string when requesting the video list from api.video’s API.

For example, if the teacher's unique tag is “einstein,” our request would look like so:

```shell
curl --request GET \
--url 'https://ws.api.video/videos?tags=einstein' \
--header 'authorization: dgsgsdgsdgsdg' \
--data '{}'
```

Our backend would get a response from api.video’s API that looks like this:

```json
{
  "data": [
    {
      "assets": {
        "hls": "https://cdn.api.video/stream/89-9f9-8ae/hls/manifest.m3u8",
        "iframe": "<iframe src='//embed.api.video/58-3403-46?token=89-9f9-8ae' width='100%' height='100%' frameborder='0' scrolling='no' allowfullscreen=''></iframe>",
        "mp4": "https://cdn.api.video/vod/dRAEjQ/token/443-d9f0-45/mp4/720/source.mp4",
        "player": "https://embed.api.video/58-3403-46?token=89-9f9-8ae",
        "thumbnail": "https://cdn.api.video/stream/89-9f9-8ae/thumbnail.jpg"
      },
      "description": "An amazing video explaining the string theory",
      "mp4Support": true,
      "panoramic": false,
      "playerId": "pl45KFKdlddgk654dspkze",
      "public": false,
      "publishedAt": "2019-12-16T08:25:51+00:00",
      "source": {
        "uri": "/videos/58-3403-46/source"
      },
      "tags": [
        "einstein",
        "maths",
        "string theory",
        "video"
      ],
      "title": "Maths video",
      "updateddAt": "2019-12-16T08:48:49+00:00",
      "videoId": "58-3403-46"
    },
    {
      ...
    },
    {
      ...
    }
  ],
  "pagination": {
    "currentPage": 1,
    "currentPageItems": 3,
    "itemsTotal": 3,
    "links": [
      {
        "rel": "self",
        "uri": "https://ws.api.video/videos?currentPage=1"
      },
      {
        "rel": "first",
        "uri": "https://ws.api.video/videos?currentPage=1"
      },
      {
        "rel": "last",
        "uri": "https://ws.api.video/videos?currentPage=1"
      }
    ],
    "pageSize": 25,
    "pagesTotal": 1
  }
}
```

We can then handle that response however we’d like, passing on to the client app whichever properties we choose, confident that this user uploaded these videos.

## What about the Students?

Applying the above technique to provide each student with a video dashboard tailored to them is simple.

Let’s say we have a table for courses that lists all the essential info for each course.

```sql
CREATE TABLE courses (
    id   SERIAL PRIMARY KEY,
    name TEXT UNIQUE NOT NULL, 
    .
    .
    .
);
```

Our lookup table could look like this:

```sql
CREATE TABLE student_course_lookup (
    user_id   INTEGER NOT NULL REFERENCES users ON DELETE CASCADE,
    course_id INTEGER NOT NULL REFERENCES courses ON DELETE CASCADE,
    UNIQUE (user_id, course_id)
);
```

When a student logs in, it's a simple query to get the tags of all their courses:

```sql
SELECT name
FROM courses c
         JOIN student_course_lookup s ON s.course_id = id
WHERE user_id = :id;
```

With this information, we can display a friendly UI allowing the student to choose which course they would like to see from a personalized course list.

<picture style=""><img style="" alt="" src="https://images.storychief.com/account_21166/Capture_8f8e9b0ec7b4ce5a7993857e8a282e35_1000.PNG"></picture><figcaption>Screenshot from Udacity for illustration only.</figcaption>

Based on their selection, we’ll request their videos from our backend with the appropriate tag attached.

```shell
    curl --request GET \
    --url 'https://ws.api.video/videos?tags=html-intro' \
    --header 'authorization: dgsgsdgsdgsdg' \
    --data '{}'
```

We can then pass the required fields from the response back to the client UI

<picture style=""><img style="" alt="" src="https://images.storychief.com/account_21166/Capture2_743fde0dfc0474d49cad8541305cca8a_800.PNG"></picture><figcaption>Screenshot from Udacity for illustration only.<br></figcaption>

That’s all folks!

I hope you’ve got the picture. Remember, our community is here for you at [community.api.video](http://community.api.video), and you can always reach out to me directly at yitzi@api.video.

Thanks for reading!
<script>
    if (window.strchfSettings === undefined) window.strchfSettings = {};
    window.strchfSettings.stats = {
        url: "https://api-video.storychief.io/creating-unique-video-dashboards-for-individual-users-is-easier-than-you-would-imagine-if-you-are-using-api-video?id=1727905228&type=27",
        title: "Creating Unique Video Dashboards for Individual Users Is Easier than You Would Imagine... If You Are Using Api.video😉",
        id: "4d243e33-fa51-4214-b7d7-78371ef08d5e"
    };
    (function (d, s, id) {
        var js, sjs = d.getElementsByTagName(s)[0];
        if (d.getElementById(id)) {
            window.strchf.update();
            return;
        }
        js = d.createElement(s);
        js.id = id;
        js.src = "https://d37oebn0w9ir6a.cloudfront.net/scripts/v0/strchf.js";
        js.async = true;
        sjs.parentNode.insertBefore(js, sjs);
    }(document, 'script', 'storychief-jssdk'))
</script>
<!-- End strchf script -->