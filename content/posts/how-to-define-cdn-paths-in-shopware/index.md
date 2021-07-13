---
title: "How to setup CDN Urls in Shopware 6"
author: "tinectaaa"
date: 2021-07-14
lastmod: 2021-07-14
tags: ["shopware","cdn"]
---

Edit the `shopware.yml` file in the `config/packages` subfolder of the shop.

### Change the urls leaving the filesystem on your shop:

This is mainly used to connect CDN Pull zones.

```yaml
shopware:
  filesystem:
    public:
      type: "local"
      url: "https://mycdn.example.net"
      config:
        root: "%kernel.project_dir%/public"
    sitemap:
      type: "local"
      url: "https://mycdn.example.net"
      config:
        root: "%kernel.project_dir%/public"
    theme:
      type: "local"
      url: "https://mycdn.example.net"
      config:
        root: "%kernel.project_dir%/public"
    asset:
      type: "local"
      url: "https://mycdn.example.net"
      config:
        root: "%kernel.project_dir%/public"
```

### Changing the filesystem with new urls:

In the following examples we are just adjusting the filesystem public (which are your media) and the sitemaps.
Therefore we keep theme and asset on the shops storage due to performance issues.

```yaml
shopware:
  filesystem:
    public: &bunnycdn
      type: "bunnycdn"
      url: "https://example.b-cdn.net"
      config:
        apiUrl: "https://storage.bunnycdn.com/example/"
        apiKey: "secret-ftp-password"
    sitemap:
      <<: *bunnycdn
    theme:
      type: "local"
      url: "https://pullzone.b-cdn.net"
      config:
        root: "%kernel.project_dir%/public"
    asset:
      type: "local"
      url: "https://pullzone.b-cdn.net"
      config:
        root: "%kernel.project_dir%/public"
```