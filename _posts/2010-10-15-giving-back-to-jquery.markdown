---
author: ykatz
comments: true
date: 2010-10-15 16:03:12+00:00
layout: post
link: http://blog.sproutcore.com/giving-back-to-jquery/
slug: giving-back-to-jquery
title: Giving Back to jQuery
wordpress_id: 28
post_format:
- Aside
tags:
- Community
---

For the first several years of SproutCore's life, we shipped a fast, minimal jQuery clone that powered our view layer. As of SproutCore 1.4, we integrated jQuery proper into SproutCore's view layer. I thought it might be worth taking a few minutes to explain why we made this change and what it means for our project.




## Why?




In the past, we tried to stay relatively DOM library agnostic.  You could use Prototype, jQuery, MooTools, or whatever else you wanted.  SproutCore would do its best not to depend on any of these so you didn't have to pay the cost of loading a library you didn't own.




Since we made that decision, things have changed somewhat on the web.  jQuery adoption, in particular, has skyrocketed.  Not that these other libraries aren't used, but today it's common to find most sites using jQuery alongside them for one or two things.




In short, we believe jQuery has become a nearly standard library of the web. In many ways, it is no longer just about one project but really belongs to the web as a whole.




Because of its degree of use on the web, it is by far the best way to work with the APIs exposed by the web browser. And while it was once somewhat sluggish compared with hand-rolled code, jQuery is now usually *faster* than the code you wrote yourself. The jQuery team has spent years building features with and an expert-level understanding of the browser environment and API.




Here's one example: did you know that when you use `$("<div id='test'></div>")`, jQuery caches a document fragment that it reuses every time you use the same String value? (Did you know there was such a thing as a document fragment?). To avoid memory bloat, jQuery applies heuristics to the String based on real-world usage. The widespread use of jQuery and the team's focus on real use cases has afforded the library a careful balance between all of the factors that go into using the browser efficiently.




Having spent almost half a decade pushing the limits of the browser, we're familiar with a lot of these tradeoffs. In many cases, jQuery 1.4.3 will be faster and more efficient than our code. In some cases, because of the ways that SproutCore has been used, our techniques are more efficient. Starting with SproutCore 1.4, we're going to be contributing time and resources to jQuery, which is crucial to our own success.


<!-- more -->


## SproutCore for the Rest of Us




While we are integrating jQuery further into SproutCore, we thought we might take this opportunity to make SproutCore more accessible to regular jQuery developers as well.




SproutCore has always been built as a modular framework. We've always wanted people to be able to use SproutCore's runtime library and data store as standalone JavaScript libraries. Unfortunately, we didn't put in the effort to ship them as separate libraries. 




In the weeks ahead, I'll put in the bit of work necessary to make them releasable as standalone libraries. While I'm at it, I'll reduce duplication with jQuery's own utilities, which should make the SproutCore Runtime and SproutCore DataStore libraries fit in nicely in the jQuery ecosystem.




The goal is to make it easy to use the parts of the SproutCore libraries that you want without having to jump head-first into the full SproutCore experience. SproutCore's binding system, batched DOM changes, and data store are battle-tested libraries that can significantly improve the structure of your applications.




I also plan to create jQuery plugins for these components so that you can use the SproutCore binding system as a normal jQuery method. The SproutCore team has spent some time on extending jQuery to allow DOM manipulations to be batched up and persisted all at once, and I'm working with John to make it easier for us to release a well-behaved jQuery plugin that won't break as new versions of jQuery are released.




If you're interested, it will probably work something like:



    
      var $ = batchedjQuery;
      $("#item")
        .addClass("active")
        .addClass("selected")
        .css("color", "blue")
        .flush();




This becomes increasingly useful when paired with the SproutCore run loop, which allows you to make these changes in various functions, and trigger the batch manipulation at an appropriate time. This technique is baked into the way SproutCore works, and it's partially responsible for the performance of large SproutCore applications like MobileMe. Why shouldn't you be able to get the same benefits in traditional jQuery applications?




And when you're ready to jump in and do a fast, native-style application, the full SproutCore framework will be ready for you.




This won't change the direction of the SproutCore framework itself or its API. It will simply make SproutCore's tools more accessible to a wider audience of jQuery developers who are not yet ready to jump on the SproutCore train.




## Closing




Like I said, jQuery belongs to the web. Contributing to the health and success of the jQuery library helps all web developers by giving us a shared place to work on innovative ways to use the tools that the web browsers give us. As browsers continue to improve those tools, the web community increasingly needs a place to share the work to make new features accessible, and there's no better place than jQuery.




_Post by Yehuda Katz_
