---
author: tkeating
comments: true
date: 2011-08-18 00:49:53+00:00
layout: post
link: http://blog.sproutcore.com/hubbub-%e2%9d%a4-sproutcore/
slug: hubbub-%e2%9d%a4-sproutcore
title: Hubbub ❤ SproutCore - Introduction
wordpress_id: 1666
tags:
- Tutorial
---

I was recently asked to do a write-up about my SproutCore app, [Hubbub](https://hubbubapp.com) ([@hubbubapp](https://twitter.com/#!/@hubbubapp)), as a general anecdotal guide to those interested in writing large scale applications in SproutCore for the first time.

I'm afraid this first post won’t be very technical, but I will at least attempt to make it an enjoyable read, and to tell you about some of my early bumps in the road so that you can avoid them. My overview of Hubbub will also span a few posts, so if you have particular questions, I can spend some time on them in future.


## What’s all the Hubbub?


This isn’t the place to talk up the app itself, only how it operates, so i’ll just give you the briefest of descriptions now to help set the stage.

The premise for Hubbub is that we still live in the physical world; that we all have real families, real friends and real coworkers and that we also all have a lot of real stuff. Hubbub is a companion app for our real lives, helping us keep track of our real stuff and helping us share with our real friends and neighbours.  So with that idea in mind, let me present to you the development history.


## Uh, but I don't remember much about writing Hubbub.


It's true, but not in the drunken orgy of code way that you’re imagining (calm yourself!). It’s just that Hubbub was written entirely in my spare time, evenings and weekends, going back over a year, which means my brain has jetissoned a lot of those early efforts to make space for everything I've learned since then (and to not lose the essentials, like using a spoon, my kids’ names and the order of pants vs. underwear).
<!-- more -->
Typically, it won't take so long to write an application, but I switched careers and postponed the app for several months, only recently picking it up again and releasing the beta. Hopefully the cathartic process of writing will shake loose a few of those early memories for you (or else you may find me wearing my underwear on the outside with a spoon stuck up my nose yelling at… uh, Morticent?).

So enough excuses, at least I should begin with an answer to:


## Why SproutCore?


That's easy. Like you, I knew right from the start that I wanted my app to be used by every person in the world, which meant it had to be on all the varied devices, which meant writing versions for iPhone/iPod Touch, iPad, Mac OS, Windows OS, Android Phone, Android Tablet, Blackberry Phone, Blackberry Playbook, Windows Phone, Linux OS, Web OS and…  stop!  I'm not a lunatic!  Of course I was going to build Hubbub as an application for the one decent common environment, the browser! In fact, I just can't imagine building any application these days not as a “web application”1, other than perhaps writing a money-grubbin’ iPhone game.

So yes, a web application; but why a SproutCore web application? Why not a Ruby-on-Rails, Cappuccino or micro-Frankenstein app for example? That’s also easy. I have a preternatural knack for spotting winners.

Well, I did feel immediately that SproutCore was going to be the future for writing applications, but I’ll admit that there was a bit more to it than that.  For instance, I knew that I wanted to write a large-scale application (MVC, localizations, bindings, etc.), which excluded all of the smaller client-side frameworks that were going to leave me hanging after my app grew, and I knew that I wanted the application to be super fast and work offline, which excluded all of the server-side frameworks. Thus it came down to Cappuccino vs. SproutCore. I came from a background of writing Mac and iOS apps, so Cappuccino was appealing… but oh, Apple uses SproutCore. Oh, okay, sure why not.


## The Company Line


Now, I realize “Tyler’s gut feeling” isn’t as compelling an argument for your VP of Engineering as it should be, but the only words I’ve ever found compelling have followed an action, not preceded it. I’m not going to waste time formulating theories that SproutCore's apples are better than framework X's oranges, but leave you to just look at the existing SproutCore apps like those from Eloqua and Apple and try and argue that they are not a higher class of web application.

For my part, my action is Hubbub, which I built entirely on my own, which means that that also is possible, which means imagine what you can do with a team and money and talent!

For a more scientific approach to choosing SproutCore, you can also read the excellent posts by Evin Grano and Majd Taby, [How do you really build large impressive web applications?](http://blog.sproutcore.com/how-do-you-really-build-large-impressive-web-applications/) and [When To Use SproutCore, and When Not To](http://blog.sproutcore.com/when-to-use-sproutcore-and-when-not-to/) respectively.  Now back again to Hubbub ❤ SproutCore.


## Standing on the Shoulders of People of Prodigious Size and Strength and Possible Gland Issues


I do recall that when I started with SproutCore, I made amazing progress at an amazing pace.  I also made amazing mistakes.  But those mistakes didn’t yet matter as I kept going forward and was also myself amazed time and time again at how little code did such big things.

SproutCore really does contain such a wealth of good ideas that you can simply turn them on as you go for quite a while. But then, eventually, your app will be big and you’ll need to do something no one else thought of before. I know when I hit that wall, it was a bit of a challenge.

The first truth to accept is that SproutCore is open source and so if no one has had your particular itch, then it’s up to you to scratch it.  The second truth to accept is that reading the source is the best way to learn how to use the framework as well as to extend it.

Back to those early mistakes. I recall that I refactored several times. In particular, moving to Statecharts was a big refactor and getting comfortable with the Datastore took a few attempts; so I would recommend that you work hard to understand and use these tools right from the start.  I can confirm that they work very well in concert with an extremely complicated UI and data layer.

The other mistake that I made was moving too quickly in some instances, so that I needed to basically go back and rethink large chunks of code.  Which brings me to the third truth, there are no shortcuts to good code, no matter what framework you use.  So now may be a good time for you to read carefully Colin Campbell’s [thoughts on application structure](http://blog.sproutcore.com/structuring-your-sproutcore-application-part-1/).

Another major mistake I made was not to understand observers and bindings well enough and so I ended up often using the wrong tool for the job and creating unnecessarily complex dependency chains. This both hurt performance and was unwieldy to maintain.


## Tune in Next Time


So, with that high level introduction to my experience with SproutCore out of the way, in my next post, Hubbub ❤ SproutCore - Getting My Feet Wet Behind the Ears (working title), I will describe in further detail the entire architecture of Hubbub, from the MongoDB database and Node.js server of the backend to the carefully tuned SproutCore 1.6 application on the client-side.

There is actually a lot that can be covered, such as:



	
  * the format of the JSON API that I use to communicate between the client and server

	
  * the inclusion of third party libraries like Google maps, Socket.io and Raphaël

	
  * how Statecharts manage the application flow

	
  * how I coordinate state changes to smooth out animations

	
  * or even my process of doing a Hubbub build and deploy.


So be sure to indicate if any of that is interesting and I’ll dedicate more space to it.

Thanks for making it to the end, you’re awesome!

	
  1. Wait! “web application”, like “native application”, is a loaded term. If you think that Hubbub isn’t complex software like any other complex software on your device you’re wrong.  If you think that it won’t be available in the iTunes App Store, Android App Store, Mac App Store, etc., then you’re not thinking very big. Why wouldn’t I embed the Hubbub code and launch it in the stores? I will! Just give me a couple minutes, I mean I have to finish this post and the follow-up posts and we just had another baby and I’ve got a full time job and it’s summer time, and come on!


