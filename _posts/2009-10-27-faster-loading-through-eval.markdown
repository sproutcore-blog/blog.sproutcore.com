---
author: admin
comments: true
date: 2009-10-27 21:46:00+00:00
layout: post
link: http://blog.sproutcore.com/faster-loading-through-eval/
slug: faster-loading-through-eval
title: Faster Loading Through Eval()
wordpress_id: 89
post_format:
- Aside
tags:
- Performance
---

_Note: Unfortunately, the images that accompanied this post were stored in an individual's private share and have been lost. Because this post is very old, it will not be updated. However, the results of this work did make its way into SproutCore as [`SC.Module`](http://docs.sproutcore.com/#doc=SC.Module&src=false)._

When you want to reduce the load time of a JavaScript-heavy web page (like any SproutCore application), you inevitably spend a lot of time thinking about how to reduce the time consumed by the JavaScript itself on page load.  This is particularly true when working on mobile devices, as the [Gmail or Mobile team recently pointed out](http://googlecode.blogspot.com/2009/09/gmail-for-mobile-html5-series-reducing.html).



The Gmail team used an interesting technique to reduce their load time on the iPhone by loading scripts as comment which they later regexed and eval'd on demand.  I wanted to see if I could make something like this totally automatic in the next version of SproutCore, so I've been doing some research.  This post documents some of my findings.





## Anatomy of a Script Load





Whenever your browser loads a script, it essentially has to go through three steps:





  1. Download the script from the server (if needed) or load it from cache


  2. Parse the script


  3. Execute the actual code in the script



Now, I should point out that usually 80% of your performance problem lie in step 3.  You can often cut the script-portion of your page load time the most by simply redesigning your code to do less work up front.



This is mostly what we focused on for SproutCore 1.0 and it yielded some big improvements.  One app, for example, had it's worst case load time on IE drop from 10 seconds to 2 seconds just by using our new API that defers execution whenever possible.



After you stop doing more work than necessary, often the next biggest bottleneck is step 1.  You can get around this by packaging your scripts into as few files as possible, using a CDN, and using caching.  Again, SproutCore 1.0 makes almost all of this totally automatic.  So we've got you covered there.


<!-- more -->



## Faster Parsing Through Eval()





Once you've beat these first two bottlenecks, the next thing we need to address is JavaScript parse time.  Believe it or not, your browser can actually spend a significant amount of time just parsing your code; especially if you have a lot of it.



You can get around this with some trickery, it turns out, by downloading your JavaScript, not as actual script, but as something else.  The Gmail team wrapped their scripts in comments.  I'm trying to simply download my scripts as strings.



Since strings and comments both don't involve constructing actual code, the browser is able to process this code much faster on initial download.  Only later, when you actually need the code, do you need to eval() the code to get it ready.



So how much exactly can you cut your page load time if you download strings/comments instead of actual code?  Well, I ran a few tests to find out.





## The Tests





In these tests, I eval()'d a 50K function directly.  Then I tried wrapping the same function inside of a comment and eval()'d that.  This roughly reproduces the technique described by the Gmail team.



Using comments to defer parsing is clever but it requires some hacks involving an iframe and it won't work across domains, so I also tried wrapping the 50K function inside of a string as well.  Theoretically, passing your code as a string and processing it later should get us most of the benefits of comments without the limitations.



Here are the results of parsing in all the major web browsers on the desktop (times are avg/eval in msec):



![](http://idisk.me.com/charlesjolley/Public/Pictures/Skitch/quick_test_data-20091027-145104.png)



I also tried the various methods on an iPhone 3G (not 3GS).  I am including a separate chart here because the raw times are so different I didn't want to throw off the chart scale:



![](http://idisk.me.com/charlesjolley/Public/Pictures/Skitch/quick_test_data_-_iphone-20091027-142630.png)





## The Results





Overall, wrapping code as a large comment is faster than wrapping the code as a string on all browsers.  (Most of them required less than half the time to parse a comment over a string.)



However, on all browsers, even using the string approach was **3x-20x ****faster** than loading the function directly.  That is a huge win if parsing time is your primary bottleneck. [Again - it usually is not.]



Overall, even though using comments is technically faster than strings, I think we are still going to go the strings approach for now.  The marginal gain is not large enough to counter the drawbacks of the technique in my book.





## The Caveats





So, looks like perhaps we've found a nice way to further improve the load times on SproutCore apps.  I'm going to build this in at some point in SproutCore 1.1 or later.



That said, if you are thinking about using this technique on your own site, there is an important limitation you should consider.



This technique works by loading your code as a string or comment _first_. What is did not show in the graphs above is the added time required to convert this string or comment into usable code.  When you include this time, the actual time required to get your code into a usable form for either technique is actually four times **slower** than simply loading your code.  Not good!



Because of this, I would recommend using this method only if the following are true:





  1. You have already made your code do as little as possible on page load and packed your JS into the minimum number of files and you defer loading JS whenever possible.


  2. You need to reduce your initial page load time to an absolute minimum.


  3. You have a lot of code to load, but during any one session you may execute only a portion of it.  [In this case, be sure you can eval your code in bits and pieces]



Finally, if you are working on a mobile device, note that the gain here will be far more important as the time differential will be noticeable to a user.  This is the primary reason why we are adding it to SproutCore in fact.





## Where's the Code?





So nice technique.  How will this make it into SproutCore?  Turns out, there is already a prototype out there.



SproutCore 1.1 or later will adopt the new CommonJS SecurableModule standard for packaging JavaScript.  When we do this, our loader will be able to accept strings of module code as well as functions.  You can find our prototype of this code in our new loader, [code-named Tiki](http://github.com/sproutit/sproutcore-tiki), on Github.
