---
author: admin
comments: true
date: 2009-11-13 17:21:18+00:00
layout: post
link: http://blog.sproutcore.com/scresponse-and-json/
slug: scresponse-and-json
title: SC.Response and JSON
wordpress_id: 81
post_format:
- Aside
---

[martinottenwaelter](http://martinottenwaelter.fr/post/242665340/sc-response-and-json):




<blockquote>

> 
> SproutCore’s `SC.Response` was [recently rewritten](http://github.com/sproutit/sproutcore/commit/3ac172b2559e85a0a7c8a260fcf5f1dab2de9773) and I [patched](http://github.com/sproutit/sproutcore/commit/d380ed008e0cd42b6b05e21a179a4de390550c1d) it to avoid an exception to be thrown when a malformed JSON string was parsed. The standard way to write you data source `didFetch` method is now:
> 
> 

>     
>     <code>didFetch: function(response, params) {
>       var results; 
>       if (SC.ok(response) && SC.ok(results = response.get('body'))) {
>         ...
>       } else {
>         store.dataSourceDidErrorQuery(query);
>       }
>     }
>     </code>
> 
> 
</blockquote>


 
