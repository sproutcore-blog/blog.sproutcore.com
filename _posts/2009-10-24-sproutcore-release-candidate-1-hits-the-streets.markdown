---
author: admin
comments: true
date: 2009-10-24 10:54:18+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-release-candidate-1-hits-the-streets/
slug: sproutcore-release-candidate-1-hits-the-streets
title: SproutCore Release Candidate 1 Hits the Streets
wordpress_id: 92
post_format:
- Aside
tags:
- Release
---

Last night I merged the final set of changes for the first release candidate of SproutCore 1.0.  I also published a new gem (build 1.0.1008) so you can get the official release quite easily.  Just open your terminal [on Mac or Linux] and type:




<blockquote>`sudo gem install sproutcore`</blockquote>




Then enjoy!




If you just want a taste of what the release candidate can do, check out the demos at:




<blockquote>

> 
> [http://demo.sproutcore.com](http://demo.sproutcore.com)
> 
> 
</blockquote>




Especially try the [SampleControls](http://demo.sproutcore.com/sample_controls) app, where you can see an example of over 300 views rendered on a single page (in the Controls tab).




**What's In the Box?**




In case you haven't heard, SproutCore 1.0 is a major revision of the entire SproutCore platform. New build tools, new data store, new view layer, massively upgraded bindings and property observing and more.  Our primary goals for this release were performance and stability.  I'm happy to report we achieved both in spades.




**Fast, Fast, Fast!  Make it fast!**




I created SproutCore in the first place was because I wanted to build fast applications on the web.  I believe the web is the ultimate application platform, but it will only be so when we can build apps that are just as fast and fluid as their native cousins.




While the 0.9 code I think proved this concept; we hadn't really achieved parity yet.  Our goal with 1.0 was to make sure SproutCore apps could load on any desktop browser in under 3 seconds, even if the app is big and complex and has a large data set.




We passed this goal actually; by 50%.  Most SproutCore apps can load in under 1.5 second with the proper deployment.  You results may vary; but if they do it is unlikely SproutCore will be the bottleneck.


<!-- more -->


Here are just a few of the big enhancements we added to make this possible:




  * The build tools can now automatically combine your JavaScript and CSS to minimize the number of assets you have to download.  Usually, you'll only need to get 2 scripts and 2 stylesheets that's it.


  * Output apps are also designed for caching.  If you follow our deployment guide, your app will be able to essentially "live" in your user's browser cache; eliminating network latency issues for the SproutCore part entirely [after first load].


  * We also made it possible to break your application into loadable bundles that can be deferred until you actually need them.  This means if you have a large app you an write portions of it so they only load when they are actually needed; keeping your initial page weight down to a minimum.


  * On the framework level, our view layer was rewritten specifically around the major performance bottlenecks in IE.  Our new layer can render 300 views client side in IE in about 100msec (on my Mac Book Air).  It's even faster in the other browsers.


  * Once rendered, all views on the page are now displayed using absolute positioning.  This not only virtually eliminates cross browser issues for display - it also makes the browser actually render your content faster.


  * We also rewrote the datastore layer to "lazy evaluate" queries and data changes.  This means you can easily shove a large number of records into the data store - some people have been using 50,000 or more records each time their app loads - and we'll handle it just fine.  You can load those records often in just a few hundred msec.


  * Finally, the code property observing and bindings layer that underpins all of SproutCore was massively optimized.  Notifications are sent less often, use less memory, and they are generally 3x faster than the 0.9 code.



All of these improvements essentially mean you can make just about any SproutCore app load and run in just a few seconds.  The only piece of your infrastructure we can't control is the part of your server that delivers actual data.  If you can make that component blazing fast as well, your web app will knock the socks off of a native app any day.




If you want an example of this performance, just [visit the Tasks](http://tasks-sc.appspot.com/) app (running 1.0 Beta code on top of Google App Engine) and login as "guest".  You can also checkout the new [SproutCore demos](http://demo.sproutcore.com) linked below.




**No More Changes!**




SproutCore is a large framework.  It has over 25,000 lines of code.  We wanted to make SproutCore stable - meaning both the API we published would not change underneath you (or at least it would change in a controlled way) and that features we added would continue to work; even as we introduced new code.




We started on this goal by adding nearly 5,500 unit tests across the entire platform.  It's a lot of unit tests.  Currently, on Safari 4 and Firefox at least, every single one of these unit tests pass green.  IE7 and IE8 each file 18 tests due to issues with the tests themselves rather than the code they test; we aim to have these tests fixed by the time 1.0 is final as well.




We also massively reworked the entire API, scrubbing it for consistency and cleaning up areas that were confusing or made it too easy to do things wrong or too hard to do things right.




This API review led to a lot of church and instability, ironically, during development which was an endless source of frustration for those few brave souls who were building on 1.0 before it was finished.  It was worth the pain, however.  The new API is easy to use and generally works well.




We will always want to polish bits of the API here and there, but I'm convinced that we have a clear path to evolve our code now without breaking your existing code in major ways again.




**What's Next?**




The release candidate is out.  This means we are "done" with the development of SproutCore 1.0.  Please test it out if you can and send us feedback.  If you find a bug or want a change in, please still submit it.  We can take changes up till just before we release thanks to our unit tests.




The core team will be working on finishing documentation on the wiki, validating example applications, and updating the website for our final release.  We would also like to have a party in San Francisco for the release.




When these things are ready,  SproutCore 1.0 will be fast, stable, and easy to learn (thanks to the new docs and tutorials).  Then, finally - after a year of effort - we will be done.




**Thanks!**




Finally, I want to say a word of thanks to all of those who have contributed to the development of SproutCore over the last year.  I went back through the commit logs and its actually a pretty big list.  I can name 30 contributors and that doesn't include the folks who send me patches now and then via email.




But I just want to call out those I can.  If I missed you, please forgive me.  But your contribution is really appreciated:




  * Billy Kakes


  * Brian Cully


  * Charles Jolley


  * Chris Hyle


  * Colin Campbell


  * Cortlan Klien


  * Erich Ocean


  * Evin Grano


  * Geoffrey Donaldson


  * James Austin


  * Jason Ketterman


  * Jonathan Lewis


  * Joshua Dickens


  * Juan Pinzon


  * Majd Taby


  * Martin Ottenwaelter 


  * Maurits Lamers


  * Mike Ball


  * Mike Subelsky


  * Mohammed Ashik


  * Onar Vikingstad


  * Peter Bergstrom


  * Peter Wagenet


  * Ray Bodenhorn 


  * Santosh Shanboque


  * Sudarshan Bhat


  * Tanner Donovan


  * Teresa Tsui


  * Thomas Langemann


  * Tom Dale


  * Trek Glowacki



Most of us get into the software industry to try to build something that is really, truly, great.  Like-magic kind of great.  It turns out it is really hard to do this.  We can turn out good software, but the really great stuff doesn't come easy or often.




SproutCore 1.0 is really truly great.  It's the best piece of code I've never been involved with and it's thanks to the contributions of the folks above, as well as those who've been testing, providing feedback, and brave enough to try to build actual products on our code while it was still in development.




So thank you!  I can't say it enough.




**What's Next Next?**




Finally, I can't leave this post on 1.0 without pointing you who are interested to some of the cool things we are already starting work on for [SproutCore 1.1](http://wiki.sproutcore.com/Quilmes-Introduction) (code named [Quilmes](http://en.wikipedia.org/wiki/Cerveza_Quilmes)).  Now that 1.0 is looking really solid, we get to spend some time on really fun things including:




  * An awesome new animation layer (already working in alpha form).


  * A FormView that can automatically generate an editor or browser UI from model objects


  * A UI builder - like Interface Builder or Atlas.  The engine is already finished; we're just putting together the editor UI.


  * A new JS loader based on [CommonJS SecurableModules](http://wiki.commonjs.org/wiki/Modules/1.1).  This will make SproutCore usable in server-side code as well as making it easier to suck in external libraries for your own use.



Development is being [tracked on the wiki](http://wiki.sproutcore.com/Quilmes-Introduction) so head on over to take a look.




The Tasks app I linked to earlier is also coming along nicely.  The team there has a few more changes lined up, but we will soon be able to use it as our default bug tracker and planning tool for SproutCore.




![](http://l3-1.kiva.org/r17693/images/logoLeafy3.gif)




Last of all, I want to give a shout out to the team at Kiva.org who has been working with us on a new [Kiva Loan Browser](http://github.com/skylar/Kiva-Loan-Browser).  Kiva, you might know, is a non-profit that makes microloans to entrepreneurs in developing countries.  Microloans are one of the most effective ways to address poverty and Kiva is one of the best.




SproutCore needs a good end-to-end example application and so we've partnered with them to build a new Loan Browser - and perhaps more in the long run.  I hope that once SproutCore 1.0, you will help us build this app into a really great way for Kiva to find and share loans.




Help others while you learn!




--




So this post has turned into a minor book.  Sorry for the length.  1.0 is a big milestone.  I can't wait to see what you build with it.




-Charles


 
