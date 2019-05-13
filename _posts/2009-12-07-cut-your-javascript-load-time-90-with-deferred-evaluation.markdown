---
author: admin
comments: true
date: 2009-12-07 06:24:00+00:00
layout: post
link: http://blog.sproutcore.com/cut-your-javascript-load-time-90-with-deferred-evaluation/
slug: cut-your-javascript-load-time-90-with-deferred-evaluation
title: Cut Your JavaScript Load Time 90% with Deferred Evaluation
wordpress_id: 73
post_format:
- Aside
---

_Note: Unfortunately, the images that accompanied this post were stored in an individual's private share and have been lost. Because this post is very old, it will not be updated. However, the results of this work did make its way into SproutCore as [`SC.Module`](http://docs.sproutcore.com/#doc=SC.Module&src=false)._

In [Faster Loading Throug eval()](http://blog.sproutcore.com/post/225219087/faster-loading-through-eval) a introduced a new technique for improving load time of JavaScript applications called **deferred evaluation**.  As a follow up to the micro-benchmarks I performed in that test, I wanted to see how much deferred evaluation could improve load time in a full end-to-end test.





## Background





In case you didn't read the other post, deferred evaluation is a technique that can be used to reduce the load time of a web page when you need to fetch a large amount of JavaScript.



Traditionally, when you include a script tag in your page, the browser will stop processing the page while it downloads, evaluates, and executes your script.  Even if your code doesn't do much but define classes and other standards, simply parsing and executing such a large quantity of code can have a noticeable effect.  This is especially true on mobile devices like the iPhone.



With deferred evaluation, instead of sending your JavaScript as regular code, you wrap it in  something else - as a string or a comment for example.  This way the browser will download your code but not attempt to parse or execute it.  Later, when you actually need to use the code, you can eval() it.



My first tests were micro-benchmarks focused on the different types of deferred evaluation.  They seemed to indicate that using this technique should reduce the JS portion of your page load 3x-10x.  Comments vs strings don't seem to make a difference, so I'm focusing on strings because it is easier to process later.



Those were micro-benchmarks.  Next I wanted to see how this would play out with a real page.





## The Test





The tests, if you want to try them on your own browser are [here](http://www.sproutcore.com/trial/baseline), [here](http://www.sproutcore.com/trial/closure), and [here](http://www.sproutcore.com/trial/string).  You should load each test once, then click "Run Again" to get real results.  [The first run will cache the files.]



Each test does the same basic thing: it loads jQuery then generates a report with the timing results.  Here are how the tests differ:





  * **Baseline** - load jQuery like normal via script tag.  jQuery is parsed and executed immediately on load. 


  * **Closure** - load jQuery in a closure but don't actually execute the closure until after the onload event fires.  This essentially means the jQuery code will be parsed but not executed until later.


  * **String** - load jQuery as a giant string.  After the onload event fires, eval() the string to actually make jQuery ready for use.



The test measures two times: load and setup.  The load time is the time that elapsed from the start of the page load to when the onload event fired.  setup is the time that elapsed from the start of the page load until jQuery was fully loaded and ready to use.

 <!-- more -->

For the baseline test, the load and setup times are always the same (since jQuery is setup while it loads).  The closure and string tests both have to do some extra work after onload fires to prepare jQuery, so their setup times will differ.



The test code, by the way, is setup to repeat five times before it generates a report.  If you ran the test, you would see it reload the page several times.  This is why.





## The Results





So how did it do?  As expected, deferred evaluation cut load time significantly - sometimes by up to 90%.  Surprisingly, in all browsers except for Chrome, the total time required to get jQuery setup and ready to use was roughly the same.  This means that the overall cost of using deferred evaluation to load your code is not nearly as bad as my earlier microbenchmarks implied.



Here are the relevant diagrams.  All numbers are relative to the time required to load the baseline for each browser.  This makes it easier to see the difference:



![](http://idisk.me.com/charlesjolley/Public/Pictures/Skitch/String_Eval_Trial_Results-20091206-221019.png)



[I don't have access to IE this weekend.  I will add a chart for IE soon.]



So what's going on with this Chrome business?  Apparently Chrome is almost 4x slower at eval()'ing code than it is as loading the exact same code from a script tag.



That said, Chrome is ridiculously fast at loading scripts.  In absolute time, Chrome took an average of 12 milliseconds to load jQuery in the baseline test.  The next closest was WebKit with 36 milliseconds.  In the "string" test, Chrome takes about 50 msec compared to WebKit's 45 msec.



In other words, Chrome appears to have a fast path for loading scripts from a script tag that is triggered by my test.  When using other techniques it is "only" as fast as WebKit - which beats pretty much everyone else by a country mile so I wouldn't worry too much about it.





## Recommendations





Based on my tests, I think deferred evaluation should have a place in just about every JavaScript developer's tool belt if you are building large scale applications.  Simply having the ability to preload your JS without pausing the browser while it is parsed is a huge win.



Generally, you should consider using deferred evaluation when you want to load a large amount of JavaScript that you may or may not use (say - depending on user action).  This way your code will be available when needed but doesn't cost much to fetch in the first place.



You should not use deferred evaluation to load all of your code, especially any code you know you will need on page load anyway.  Since you will eval() the code in the end, there is no win.



For SproutCore, we already have support for deferred evaluation built in.  It will be included in the main branch for SproutCore 1.1 sometime in early 2010.  You can try it today by using the "tiki" branches of both the build tools and sproutcore itself.




**UPDATE:** I had a chance to test IE8 today as well.  Here are the results (IE7 had a similar profile):



![](http://idisk.me.com/charlesjolley/Public/Pictures/Skitch/String_Eval_Trial_Results-20091207-162738.png)



Basically, the net of this chart means that the string approach won't actually save you as much time with IE.  As you can see the base load time is about the same for both methods.  When you add in the extra eval(), the string method is actually about 13% slower than just executing your code outright.



That said, there are some confounding factors to keep in mind here:





  1. IE had much more variability in its results than all the other browsers.  In some cases, the baseline was slower than the string - in other cases it was faster by a wide margin.  Overall I would rate these as about equal in performance.


  2. If you don't actually use the code you are loading, the string method is still no worse than baseline loading.



In summary, my original advice still stands.  Deferred evaluation can be very useful if you need to load a lot of code that you may or may not use.  This is especially true for mobile devices.  With IE you will receive fewer benefits however.  If your audience is primarily IE it might not be worth the effort.
