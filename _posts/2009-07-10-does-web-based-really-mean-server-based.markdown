---
author: admin
comments: true
date: 2009-07-10 16:31:53+00:00
layout: post
link: http://blog.sproutcore.com/does-web-based-really-mean-server-based/
slug: does-web-based-really-mean-server-based
title: Does Web-based really mean Server-based?
wordpress_id: 144
post_format:
- Aside
---

Daring Fireball posted a great [analysis](http://daringfireball.net/2009/07/chrome_os_context) of the new Chrome OS.  However, he demonstrates one of the common misconceptions about modern web platforms.  Money quote:




<blockquote>Web apps largely consist of server-side code, with a relatively thin layer of JavaScript that runs on the client. Data, too, mostly resides on the network, not the client machine.</blockquote>




This is exactly the misconception [What is a Cloud Application](http://wiki.sproutcore.com/What-is-a-Cloud-Application) on our wiki tries to address.




![](http://img.skitch.com/20090625-jyus9ardg2ismw87w8dpqye7ab.png)




John's statement is true for most deployed web apps today, but only for historical reasons.  There is not (anymore) any technical limitation to building full client-side apps in the browser.*  With HTML5 ApplicationCache and offline storage, its entirely possibly to create a web app that "installs" itself onto a local machine and can run anytime. The capability is there; we just need developer tools and developer knowledge to catch up.





* As in most things these days, this does not apply to IE.  But I'm talking only about the browsers that would be used on a "web-only" device.
