---
author: TomHuda
comments: true
date: 2011-03-01 20:37:00+00:00
layout: post
link: http://blog.sproutcore.com/introducing-sctemplateview-now-with-tutorial/
slug: introducing-sctemplateview-now-with-tutorial
title: Introducing SC.TemplateView - Now With Tutorial
wordpress_id: 12
post_format:
- Aside
tags:
- Tutorial
---

Yesterday, we released an updated version of the SproutCore 1.5 prerelease gem that contains our preliminary work on Amber and SC.TemplateView.




To us, Amber means significantly reducing the cognitive overhead of picking up SproutCore for the first time. A big part of that is leveraging technology that web developers already know: HTML and CSS. We've heard from developers in the past who said they loved SproutCore's observers and bindings but were intimidated by the complexity of its view layer.




Part of easing developers into SproutCore means having the best documentation on the planet. Over the past month, contributors have done a kick-ass job of populating the SproutCore Guides site with up-to-date and easy-to-follow material. We wanted to provide a similar experience for SC.TemplateView, so we've written a hands-on guide to using it to build a simple (but still fully-featured) todo application.




You can find the guide at [http://guides.sproutcore.com/html_based.html](http://guides.sproutcore.com/html_based.html). It takes you through the process of initializing a new project, defining your models, designing your views, and then tying them all together with controllers and bindings. You can also check out the finished product at [https://github.com/sproutcore/Todos-Example](https://github.com/sproutcore/Todos-Example).




We think that describing the flow of data in your application, then allowing the framework to put the pieces together for you, leads to robust, maintainable applications. In fact, we think this declarative structure is the only way to build web applications that truly scale beyond simplistic demos like this one. We plan to create a second iteration of this app that really shows off how well the declarative model allows you to manage increasing complexity. But for now, we think you'll be blown away at how features begin to emerge, almost like magic. By paying a small upfront cost, you begin to get functionality for free.

<!-- more -->


Because SproutCore does all of the heavy lifting, your app code remains small, and you don't have to worry about introducing errors in your glue code. Other frameworks like to talk about their small size, and we think they are a good fit for simple apps, but their small size does you no good if you end up writing many of the features of SproutCore yourself.




While we're not there yet, we are on track to have Amber ship at under 50k after gzip and minification. As examples like New Twitter show, apps of any sophistication end up dwarfing the frameworks upon which they are based precisely because they eventually have to implement their own abstractions. We've thought a lot about how client-side web applications can scale, and we think you'll agree that SproutCore can ease growing pains as the client side gets ever more complex.




[@tomdale](http://twitter.com/tomdale) & [@wycats](http://twitter.com/wycats)




**NOTE: **If you installed SproutCore 1.5.pre.4 yesterday, please make sure to update to SproutCore 1.5.pre.4.1 (gem install sproutcore --pre). There are some important bugfixes that are necessary in order for the tutorial.
