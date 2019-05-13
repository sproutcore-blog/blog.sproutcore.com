---
author: admin
comments: true
date: 2010-04-18 12:49:00+00:00
layout: post
link: http://blog.sproutcore.com/introducing-sproutcore-touch/
slug: introducing-sproutcore-touch
title: Introducing SproutCore Touch
wordpress_id: 50
post_format:
- Aside
tags:
- News
---

_This guest post was contributed by Mike Ball.  Mike presented SproutCore today at jsconf along with Evin Grano._




There are two officially supported platforms for developing apps on touch devices like the iPad: native and HTML5.   A lot of people don't know this or don't care because conventional wisdom states that you can't build a really great HTML5 experience on touch devices.




Guess what?  Conventional wisdom got it wrong.  Ever since the early iPhones Safari has had great touch-specific features and the problem is, as is common in the web, few people know how to use them.




Today all of that changes.  At jsconf this morning Evin and I, representing the SproutCore project, got to show for the first time SproutCore Touch.




![Hedwig on iPad](http://idisk.me.com/charlesjolley/Public/Pictures/Skitch/iPhone_Simulator-20100418-144225.png)




SproutCore Touch is the first edition of SproutCore that includes complete support for touch events and hardware acceleration on the iPad and iPhone. 


<!-- more -->


So in addition to supporting low-level browser features SproutCore also integrates touch into our high-level views.  For example SC.ScrollView supports hardware optimized scrolling which some people said was impossible!  We also have a bad-ass SC.MasterDetailView that automatically reconfigures your UI to show a sidebar in landscape mode and hides it under a picker in portrait mode.




Since all of our views provide touch support automatically, this means that you can actually use SproutCore Touch to build apps that run both on the iPad and desktop computers.  In fact, we've found that usually its easier to build our apps for the iPad first and then desktop next - since things usually just work when you transition.




Touch is the most important innovation we've seen in computing in 15 years.  It is completely changing the way people interact with their content.  As developers, we have a chance to really up the experience on our own apps thanks to this new technology.  




Now if your app makes more sense on the web than as a native app, you have a viable way to build something using the only other officially supported platform on touch: HTML5.




If you want to try SproutCore Touch yourself check out our slick new documentation app:




http://touch.sproutcore.com/hedwig




It currently runs on both the desktop (well WebKit, Chrome and Firefox - we are still fixing minor bugs on IE) and the iPad.  




If you want to start building SproutCore Touch apps yourself, first go to the SproutCore Home page, install SproutCore, and then switch to the latest master branch.  All the code is available there today.




The developers who worked on this for the last few months are also hanging on the IRC channel at #sproutcore if you need some help.




Finally, I'd like to give a shout out to all of the developers from Apple and around the world who have worked so hard on getting SproutCore Touch ready.  This new technology has truly been a community effort. We were humbled to get to present all of your amazing work today.




So, please check out SproutCore Touch today.  We can't wait to see the native-like apps that get built with SproutCore touch.




PS. I should add that SproutCore Touch is only possible thanks to the hard work put in by developers over the last few years to give SproutCore 1.0 it's incredible performance and speed.  Touch devices run fast web browsers on slower hardware.  Without that baseline performance, we never could have built this experience in such a short time.
