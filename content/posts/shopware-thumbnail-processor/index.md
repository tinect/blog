---
title: "Shopware 6 + ThumbnailProcessor"
author: tinect
date: 2021-08-17
tags: ["shopware","cdn","thumbnail","pagespeed"]
draft: true
---

> No one needs thumbnails on disk!

If you have no idea, why it is a great idea to use dynamic thumbnail and images, instead of creating WebP images, please 
[read this]({{< ref "../you-might-not-need-thumbnails-or-modern-image-format/index.md" >}})

## Goal

I will show you how to install ThumbnailProcessor.

Just imagine you can get suitable thumbnails and webp images without waiting for generation.
This is why there is a plugin named ThumbnailProcessor.

I hate it to wait for any file to be generated, `webp` or `avif` f.e.
Additionally, we exaggerated with cms-elements and different viewports, so we added 15 more thumbnail-sizes onto album CMS.

These were a few reasons for the plugin ThumbnailProcessor. In the end the plugin just tells the shop not to get the url of the shop, but translating url of any service to be used in shopware.

You might know services like cloudinary, cloudimage or selfhosted imgproxy. If not, I will show you one.

So, let us start to deliver images as webp.  
We will install the Processor with Bunny.net which is an suitable content delivery network with the option to deliver images on-the-fly.

>! Please note: while we want to install just the ThumbnailProcessor, we won't take care of storage at bunnycdn. See dedicated post about the storage.

- Register at bunny.net
- 