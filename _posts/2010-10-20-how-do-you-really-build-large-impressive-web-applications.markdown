---
author: egrano
comments: true
date: 2010-10-20 14:20:00+00:00
layout: post
link: http://blog.sproutcore.com/how-do-you-really-build-large-impressive-web-applications/
slug: how-do-you-really-build-large-impressive-web-applications
title: How do you really build large impressive web applications?
wordpress_id: 26
post_format:
- Aside
tags:
- Tutorials
---

There have been enormous leaps in browser technology and computers that have made rich internet apps and cloud applications no longer a figment of someone's utopian dream, but a reality that can be acted on today.  I want to take you on a journey how my company, [Eloqua](http://www.eloqua.com), did just that, take an utopian dream of the best web application and made it a reality, with SproutCore.



## How do you decide what technology to use?



Well, the journey started about a couple of years ago, even before I came to Eloqua.  Eloqua was the market leader and really the inventor of the [marketing automation](http://www.eloqua.com/topics/marketing-automation.html) space.  This space is where the marketing teams and the sales team work to get the right information to the right people at the right time.  In order to grow your business, timing is crucial.  Eloqua had built an application from the ground up over the last 10 years.  It had all the successes and failures that come with inventing a space. Now that they succeeded in inventing the space, it was time to start the revolution all over again.  Eloqua now needed to change the game because the space was starting to get crowded and we all know that unless you are innovating and catching the next wave, soon the market leader can become yesterday's technology footnote in Wikipedia. This is when Mike Ball and I came onto the project and it was called [Eloqua 10](http://www.eloqua.com/eloqua10)...

We were looking for the next greatest thing in web technology and we started to see this resurgence in an age old idea: returning to fat clients with business logic and thin servers, but all with a new significant twist. <!-- more --> These apps were done with more native code for the browser like JavaScript and plugins and made the web more like native desktop applications.  So which technologies are we to use to to do this?  How do you make a great user experience across the web?  Well, first you need to see if people have done it before.  So we started to look around the internet for web applications that do what we wanted to do.  We found a couple of examples of really cool applications that are pushing the envelope of what is possible.  Applications like:

  - [280 Slides](http://280slides.com/) from the guys at 280 North
  - [Photoshop Express Editor](http://www.photoshop.com/tools?wf=editor)
  - [Squarespace](http://www.squarespace.com/)
  - [Mobile Me](http://www.me.com)
  
So these applications represent technologies like the following: Cappuccino, Flash/Flex, SproutCore, jQuery, ExtJS and others. But, what if you want to make a more sophisticated application than these?  What if you want to push the envelope further?  You have to choose the right technology and make it do a little more than what you have seen before.  That is how you become a thought leader and that is how you innovate and stay on top of your game as a technology company.  So how do these technologies stack up?

We worked and studied every one.  We made sample applications with each when available and through this trial effort and working with people we came out with a clear winner...



## ...SproutCore



SproutCore was a new technology, but was moving in the right direction and at the right time.  We had a list of features that were required by the framework that we were to use:
  
- **Required!** Must have a quick load time.
    - *Answer:* Only SproutCore has bundling to get load times down.
    - *Answer:* SproutCore makes is easy to do things like [deferred evaluation](http://blog.sproutcore.com/post/272853740/cut-your-javascript-load-time-90-with-deferred).
- **Required!** We had a legacy system so we needed a good solution for gathering data from an established system.
    - *Answer:* Only SproutCore had a fully unified data store architecture.
    - *Answer:* SproutCore was backend-agnostic so we were able to connect seamlessly with a legacy backend and develop in parallel.
- **Required! **We had a need for fast and snappy application for getting large amounts of data.
    - *Answer:* Only SproutCore has things like SparseArrays to speed up data delivery
    
- **Required!** We were going to try some new and innovative things that we haven't seen before so we needed a platform that could easily adapt.
    - *Answer:* SproutCore has a great extensible architecture and since it is only JavaScript we can do what we needed to do when we needed to do it

Clearly, Only SproutCore provided the basis for innovation that we were looking for.  We looked at the principles that it was based on, inspiration from Cocoa, but not limited to that framework.  SproutCore used the limitations of the web in resources and used to its advantage to make an awesome desktop-like experience.  And better yet it was free and open!  We, as an engineering team, decided that we were going to be an open company with our technology.  We needed to find a project that supported those ideals.  We also needed a project that was backed by at least one respected company, was stable, and looked like it had the brightest future.  Again, the only clear winner was SproutCore.

Now that we have chosen to use SproutCore we needed to see how far we could push it.  So we wanted to innovate and release it to the SproutCore Community.  Here is a small list of features that came directly out of our work with Eloqua that we have open sourced:
  
  - [SCUI](http://github.com/etgryphon/sproutcore-ui): One of the first official third party libraries that provides the following features:
   - LinkIt: directed and non-directed graphing library that came from our work in Campaign Canvas work flow in Eloqua 10
   - Dashboards: a OSX/Windows 7 dashboard like framework
   - Foundations: Lots of the missing UI elements that we wanted to release like Calendars, Datepickers, mixins and other views that are helpful
  - [SCUDS](http://github.com/etgryphon/sproutcore-uds): Local data storage with cascading data sources
  - [Lebowski](http://github.com/FrozenCanuck/Lebowski): Our testing framework for Sproutcore-specific applications
  - Greenhouse: the free SproutCore IDE that comes directly from our with with our work in the Email and Landing Page Editor. Only possible with the power of SproutCore's design framework
  - [Sai](http://github.com/etgryphon/sai): The VML/SVG vector graphing library
  - [Ki](http://github.com/FrozenCanuck/Ki):  Statecharts for the Faint of Heart for building really world class level applications
  - [Tasks](http://github.com/suvajitgupta/Tasks): This is the project management tool that we use internally to deliver our project on time
  
So we have accomplished something remarkable in Eloqua10.  If you would like to see and here more about this application you can check it out at:

  - [Eloqua 10](http://www.eloqua.com/eloqua10)
  - [The Day “Or” Died: Eloqua10 Launch](http://blog.eloqua.com/Eloqua10)
  
So the question still is: How do you really build large impressive web applications?  You choose SproutCore.  The market has just taken notice.  In fact, tech analyst commented that this could be one of the greatest reinventions of a SaaS company in history.  We could have only done this with SproutCore and the great community behind it.  I am proud to call myself a Core Team member and I am really proud of all the work that my team at Eloqua has done.

They always say, "Fortune favors the bold" and when choosing technology for a large project like ours you have to find a technology that is shooting for a spot in the future. We are looking to keep pushing Eloqua and SproutCore to new and greater heights.
