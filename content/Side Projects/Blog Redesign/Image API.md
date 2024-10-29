---
title: Image API
tags:
  - Blog
---

# Multer

Multer is a middleware that allows a file to be downloaded by the server side of an application and stored locally then uploaded to a cloud service like AWS S3. Unfortunately because I am using Remix there is no way to run a middleware or an Express server because Remix itself is an express server. Not being able to use Multer made things quite challenging and I ended up needing to upload everything to S3 directly. Additionally because I was having issues with 64 bit filestreams, I ended up creating a Netlify function that generates a unique upload link that I can use from the frontend to directly upload the file. This ended up being extremely useful and worked flawlessly.

# Notes on Remix

You need express so you can setup Multer which is a connect middleware, you can’t use it inside an action because they don’t have the request and response objects of Node/Connect/Express.
