---
author: admin
comments: true
date: 2009-09-05 18:10:00+00:00
layout: post
link: http://blog.sproutcore.com/what-server-does-sproutcore-run-on/
slug: what-server-does-sproutcore-run-on
title: What server does SproutCore run on?
wordpress_id: 107
post_format:
- Aside
---

Ha ha! Trick question! SproutCore is a **client-side** application framework only.




**No part of SproutCore “runs” on the server, and SproutCore contains no “server-side” libraries.** A web server (Apache, for example) is only used to deliver plain old HTML, CSS, and JavaScript to the browser. Once those initial files have been served, a SproutCore-based application runs entirely in the browser (and can easily be run “offline”, with no network access at all).




Any server that can receive HTTP requests (which is all of them) can interact with a running SproutCore application, via XHR calls. Here's some example languages and servers you could use to interact with a SproutCore application at runtime: CGI scripts, Java, .Net, PHP, Perl, Python, Django, Ruby, Rails/Merb/Rack, WebObjects, WebDav and countless others.




During _development_, SproutCore's own HTML, CSS, and JavaScript and any custom HTML, JavaScript and CSS you write can be easily served to the browser using a trivial Ruby/Rack-based server included with the SproutCore buildtools and launched with the `sc-server` command. The `sc-server` command and SproutCore buildtools are _not_ used once your SproutCore application is deployed to users; they are merely a development aid.




When you are ready to deploy, SproutCore's buildtools provide an `sc-build` command—used to generate a static directory of HTML, CSS, and JavaScript that you would then upload to a production-quality web server such as Apache or lighttpd. `sc-build` will combine, pack, and minify the HTML, CSS, and JavaScript—and generate cache-friendly URLs. The same directory structure you used with `sc-server` during development is accepted by `sc-build` for deployment, making this an easy, one-step process.




Note: _SproutCore_ (HTML, CSS, and JavaScript) and SproutCore's _buildtools_ (Ruby, Rack) are [separate](http://github.com/sproutit/sproutcore/tree/master) [projects](http://github.com/sproutit/sproutcore-abbot/tree/master) and can be used independently. For example, [this website](http://www.sproutcore.com) is built using SproutCore's buildtools, but not SproutCore itself (it is a website after all, not an application).




_Hat tip to __[Jacob Kaplan-Moss](http://jacobian.org/)__ for noticing that we hadn't moved the docs for this aspect of SproutCore prominently to the new SproutCore 1.0 website._




_ _
