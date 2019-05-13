---
author: admin
comments: true
date: 2009-07-18 22:55:00+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-website-built-with-sproutcore/
slug: sproutcore-website-built-with-sproutcore
title: SproutCore Website Built With SproutCore
wordpress_id: 140
post_format:
- Aside
---

The coding portion of SproutCore 1.0 is nearly complete, so it's time to start work on some of the non-code parts of the SproutCore project.




Today I just push a brand new version of the SproutCore website.  The design is very simple, but unifies the wiki, blog, and main site so that they finally feel like they belong together.




We still have a lot more to do with the site before 1.0.  (More on that later)  But, the really interesting thing about the site is how it was built.




First, the new website uses SproutCore's build tools.  Over the last few years these tools have been honed to generate highly optimized, cache friendly apps in multiple languages.  It turns out, you can use the same tools to create highly optimized, cache friendly** web pages** in multiple languages too.  The new site is really zippy in part because we let these tools work their magic.




Second, the new website is built in HTML5*.  SproutCore is an HTML5 application framework.  Although the "section" and "article" tags don't have much to do with applications, we want to eat our own dogfood; so, there you go.




Third, and most important, the new website, like the rest of SproutCore, is open source.  You can get at the source HTML for the site by visiting the [Github repository](http://github.com/sproutit/sproutcore-website). Although this isn't really "software", Git makes it easy for people to clone the website, make changes, and contribute them back.  Now anyone can contribute.




I've also put up a project page on the wiki where we can track the plans for the new website.  The code name is "[Boulevard](http://wiki.sproutcore.com/Boulevard-Introduction)".




**Left Overs**




OK, so what's left to do?




It would be nice to localize it, for one thing.  We also need to add additonal "marketing" content - including demos - that help explain SproutCore's place in the world to new visitors.  There is also a lot of polish we can put into the site itself and it probably needs a few tweaks on IE.




But, hey, its an improvement.  And it's really great to finally be at a place where we can spend some cycles on this kind of thing because the code is largely complete.




**UPDATE:** If you're having trouble with the "screencasts" link, it's probably because the DNS change is still propagating.  It should be visible in the next 12 hours.





* The site doesn't validate HTML5 just yet.  But its a moving standard and we're working on this so take this as a statement of intent.
