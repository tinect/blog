---
title: "You might not need modern file formats or need thumbnails"
author: tinect
date: 2024-01-30
tags: ["cdn","thumbnail","pagespeed"]
---

## Goal

I would like to show you, how you can make Google love your images without saving any new format.

## Imagine

- Google loves your images.
- You can obtain suitable thumbnails and WebP images without waiting for generation.
- Every visitor gets modern file formats with best quality and small sizes.
- You don't need to generate a new file or have plugins do this on your server.
- You can upload your image to the CMS or commerce platform like Shopware without waiting images to be generated.
- You don't need HTML picture tags to announce `image/webp` or `image/avif`.
- `<img src="myimage.jpg"/>` will automatically deliver WebP or AVIF, if the browser supports it.

You like to achieve all these things... quite simply?

## Background

### Picture tags with types
```html
<picture>
  <!-- avif, if supported -->
  <source srcset="img/image.avif" type="image/avif">
  <!-- webp, if supported -->
  <source srcset="img/image.webp" type="image/webp">
  <!-- failover -->
  <img src="img/image.jpg" alt="Really nice content!" loading="lazy">
</picture>
```
Cons: 
- need to save more files (original JPEG, WebP and/or AVIF)
- your CPU wasted
- your servers storage wasted
- HTML is larger

So, what about just this?
```html
<img src="img/image.jpg" alt="Really nice content!">
```

### Responsive picture tags
```html
<picture>
  <!-- avif, if supported -->
  <source type="image/avif" srcset=" img/image_100px.avif 100w, img/image_200px.avif 200w, ..."
    sizes="(max-width: 768px), (max-width: 1376px), 500px">
  <!-- webp, if supported. paste the above and replace avif with webp or imagine here are more lines following -->
  <!-- ... -->
  <!-- ... -->
  <!-- failover -->
  <img
    srcset="img/image_100px.jpg 100w, img/image_200px.jpg 200w, ..."
    sizes="(max-width: 768px), (max-width: 1376px), 500px" src="img/image.jpg"
    alt="Really nice content!">
</picture>
```
Cons: 
- need to save more and more files (original JPEG, WebP and/or AVIF - each in different sizes)
- your CPU is more wasted
- your servers storage is more wasted
- HTML is even larger

So, what about just this?
```html
<img
    srcset="img/image_100px.jpg 100w, img/image_200px.jpg 200w, ..."
    sizes="(max-width: 768px), (max-width: 1376px), 500px" src="img/image.jpg"
    alt="Really nice content!">
```

## How can this work?

There are services out there you can use to give the visitor images in best quality, format and size you like to have. You just need to upload the known JPEG, PNG or whatever.

### What these service take

- Money: Sure, everyone wants to keep their service up and economically, but there are free plans out there.
- Your data: Yes, you might need to register. Mainly they need to know, where your (original) images are accessible. So they can just pick and transform it - your shop or maybe CDN.

#### How does the code look like
Preparation:
- `https://www.tinect.de/img/image.jpg` is your original image.
- You point the service to your domain `https://www.tinect.de`.
- You might be able to set a own subdomain like `https://img.tinect.de` for the service.

Responsive example:
```html
<img
    srcset="https://img.tinect.de/img/image.jpg?width=100 100w, https://img.tinect.de/img/image.jpg?width=200 200w, ..."
    sizes="(max-width: 768px), (max-width: 1376px), 500px" src="https://img.tinect.de/img/image.jpg"
    alt="Really nice content!">
```

That's it.

### What service you can use?
There are some service I tried for one of my plugins for Shopware 6. You might know services like cloudinary, cloudimage, bunny.net or selfhosted imgproxy.
So you can check the [discussion in GitHub](https://github.com/FriendsOfShopware/FroshPlatformThumbnailProcessor/discussions/categories/patterns). There are some listed with personal opinions.

You can find selfhosted ones there too. But keep in mind, you need to manage caching on your proxy of your own servers.

### Plugin for Shopware 6

See [GitHub](https://github.com/FriendsOfShopware/FroshPlatformThumbnailProcessor) or [Shopware Store](https://store.shopware.com/en/frosh69611263569f/thumbnailprocessor-incl.-webp-support.html).  
Dedicated blog post is incomming.