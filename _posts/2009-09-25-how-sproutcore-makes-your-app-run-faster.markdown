---
author: admin
comments: true
date: 2009-09-25 23:28:00+00:00
layout: post
link: http://blog.sproutcore.com/how-sproutcore-makes-your-app-run-faster/
slug: how-sproutcore-makes-your-app-run-faster
title: How SproutCore Makes Your App Run Faster
wordpress_id: 100
post_format:
- Aside
---

If SproutCore 1.0 had a theme it would be "performance".  We've spent a lot of time - almost a year in fact - trying to make SproutCore applications the fastest web apps on the planet.  I think we've done a pretty good job overall.




For example, we took [Steve Souders](http://stevesouders.com/) excellent book on [High Performance Websites](http://oreilly.com/catalog/9780596529307) and built his 14 rules right into our platform.  We also discovered a few other rules along the way and built those in as well.




That means simply by adopting SproutCore for your web apps [and following our [deployment recommendations](http://wiki.sproutcore.com/Deployment-Introduction)], you will get best performance practices out of the box.  No black-magic required.




So what did we do specifically to make SproutCore apps faster?  Lots of things but here's how we stack up against Steve's recommendations:




## Rule 1: Make Fewer HTTP Requests.




When you build your app in SproutCore, it takes all of your JavaScript and CSS files and generates "packed" files that include all your code in one file.  Most SproutCore apps only need to load two stylesheets and two JS files when you go to production.  Although its not automatic, the built-in SproutCore theme ([Ace](http://wiki.sproutcore.com/Ace-Introduction)) is also [sprited](http://developer.yahoo.net/blog/archives/2007/04/rule_1_make_few.html), keeping the number of image files down to 5-6.




## Rule 2: Use a Content Delivery Network.




OK, we can't bundle a CDN with our tools [yet], but all SproutCore resources have versioning built into the URLs.  To add a CDN like Amazon's CloudFront, just turn it on.  Your entire SproutCore app will literally live on the CDN nodes, near your users instead of in your data center.  Major perf gain.  I can't understate the importance of using a CDN to speed up your app.




## Rule 3: Add an Expires Header.




Again, we can't configure  your web server for you, but when you build your SproutCore app, all of your assets will be packaged under a single directory with versioning.  All you need to do is add the Expires header to your Apache config and your entire SC app will be cached in the users browser.  Be careful though!  Only set your expiration to a max of 1-year.  Any longer and some proxies will actually ignore your header and turn off caching entirely.


<!-- more -->


## Rule 4: Gzip Components




This is documented in our [Deployment Docs](http://wiki.sproutcore.com/Deployment-Introduction).  SproutCore's JavaScript is already combined for you; but it is intended for you to Gzip it as well.  Turning on Gzipping in your web browser can shave up to 500msec from your load time.




## Rule 5: Put Stylesheets at the Top




Done. SproutCore generates an index.html that does this for you automatically.




## Rule 6: Put Scripts at the Bottom




Also done.  The index.html loads all your scripts last.




Although you can add scripts so they load at the top of your index.html if you jump through a few hoops, we have intentionally made designed the system to put scripts at the bottom whenever possible.




## Rule 7: Avoid CSS Expressions




Actually, this is a more special cased version of a general rule that we use which is:




_Don't use complicated CSS layout_.




Even though CSS will let you specify a rule to style the 3rd child of a 2nd cousin's aunt's grandmother, that doesn't mean you should do it.  Browsers have to invalidate and repaint larger portions of your screen to handle these kinds of crazy rules.




SproutCore is designed to encourage you to use simple absolute positioning for most app-like views.  You can use regular "flow" layouts, but it should be restricted to actual document-like content such as help files and messages.




Absolute positioning is actually a lot more flexible than most people realize; it can even resize automatically with the browser.  It is just a simpler, more easily predicted model for layout that is relatively inexpensive for the browser as long as you use it everywhere.  It also encourages you to keep your CSS rules simple, which makes the browser faster.




And for the love of all things that are good, don't use CSS expressions - the IE-only way to embed JavaScript into CSS.  It is not only proprietary; it is also terrible for performance.




## Rule 8: Make JavaScript and CSS External




Done.  All SproutCore JS and CSS is saved as external files, ready for caching and CDN hosting as I mentioned earlier.




## Rule 9: Reduce DNS Lookups




So, finally a rule where SproutCore really can't really help you. For the record, the A records, not CNAMES, whenever possible.




## Rule 10: Minify JavaScript




Done.




In fact if you ever wonder why an sc-build is taking so long to finish, it is probably the YUI minifier working on all of your JS and CSS to pack it down.  There are faster solutions out there, but the YUI minifier did the best overall job of packing down your code into the smallest size possible in our tests, so its the preferred choice for the moment.




## Rule 11: Avoid Redirects




Done.




Since SproutCore apps are single-page applications, the user rarely will need to wait on a page to load, let alone a redirect.  The one exception to this is when you need to handle login.  Sometimes best practice will require you to redirect over to a domain under HTTPS to handle login.  This should be a rare occurrence.




## Rule 12: Remove Duplicate Scripts




Done.




SproutCore's build tools will detect when your various frameworks depend on other frameworks and then  build a single dependency chain so that each script is loaded only once and in the proper order.




It is possible to get around this of course, but you  would have to work at it.  That's the point; make it easiest to do things in a performant way.




## Rule 13: Configure ETags




We can't do this in the SproutCore itself but the built files are ETag ready.  Our deployment guide also includes this in the checklist of recommendations.




## Rule 14: Make Ajax Cacheable




This rule mostly applies to your dynamic requests, but when you do load resources from SproutCore dynamically, they are setup to follow the standard caching rules so they can load quickly.




## Other Rules




I said we came up with a few more rules of our own.  Most of these relate to building heavy client-side applications, but they matter nonetheless.  Here's a short list of things that make SproutCore apps fast:




## Rule 15: Don't Do More Work Than Necessary




SproutCore apps do very little work before they get your app up and running.  For example, the entire view layer of your application may be loaded right away but no views will be constructed until you actually try to bring them onto screen.




We also added support for something called a RunLoop, which allows you to defer actions until just before you are finished running your JavaScript.  For example, if you make a view visible, then not visible, then visible again, SproutCore won't actually update the DOM until just before the event handler returns.




By following this principle, your app will generally load and launch very quickly and will have more even performance over the long run.




## Rule 16: Avoid Touching the DOM




Even though the DOM is available to you in JavaScript, underneath the covers it is actually implemented in straight C.  All browsers have some kind of bridge you need to cross every time you access the DOM to get from the JavaScript world to the C world.




This means you pay a performance cost for every DOM access; even for something as simple as reading the "id" from an element. (i.e. var foo = element.id).  In Internet Explorer this effect is especially pronounced since the COM model that wraps mshtml leaves 10 or more layers of code between the JS and the DOM.




To work around this, SproutCore's entire view layer has been specially designed to minimize the number of times we touch the DOM at all.  The first time you generate your UI for example, SproutCore will generate one large HTML string and put it on screen using "innerHTML".




Compare this to frameworks like Cappuccino, jQuery plugins that work mostly by constructing like DOM elements, or even SproutCore before 1.0, and you'll see sometimes a 100x performance improvement.  It's huge.




Of course, once you've generated your UI for the first time, SproutCore will need to work more directly with the DOM so we don't get as much of an improvement all the time.  Overall, however, SproutCore 1.0 improved our view layer performance by 10x over the 0.9 version (which was pretty fast to begin with).




## Rule 17: Don't Load More Than Necessary




If you build a very large application, you will often end up with lots of UI that may not be needed right away - or possibly ever - during a typical session.  Even though SproutCore avoids doing more work than necessary on page load, you can still shorten your load time even further by not downloading the code for this UI at all.




SproutCore 1.0 sports a new "dynamic framework" model that allows you to lazily load frameworks only when they are needed instead of all up front.  Some apps have been built with dozens of such frameworks, cutting their load time by almost 30%.




## And More...




There are more enhancements we've made here and there - such as tightly controlling memory usage and managing change propogation in the app.  There are more improvement we will make over time as well, but I think you get the idea.




The #1 reason I hear people say they can't build client-side web apps is because they are worried about performance.




Their concerns are not totally unfounded.  It has traditionally been very hard to build large JavaScript applications that perform well.  The reason, though, is not because the browsers can't handle it.  It's just because most of us didn't know all the black magic needed to do it right.




My hope is that SproutCore 1.0 will lay this concern to rest for good.  You still have to think about performance, but SproutCore takes care of the most important stuff for you.  Apps can have lots of features and still perform very well, thank you very much.




There are a lot of cool features we could have focused on for 1.0 - more controls for example or a nice visual UI builder.  We are actually working on these [especially the view builder], but none of it really matters of your app performance sucks.  You have to get that right first.




Great web performance.  Built-in.  Now _that's_ a feature.
