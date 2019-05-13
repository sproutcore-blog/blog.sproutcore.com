---
author: dcporter
comments: false
date: 2013-10-02 14:40:09+00:00
layout: post
link: http://blog.sproutcore.com/1-10-upgrade-invokefoo/
slug: 1-10-upgrade-invokefoo
title: 'v1.10 Upgrade Tips: invokeFoo Developer Warnings'
wordpress_id: 2209
---

Upgrading your project to 1.10 is a no-brainer – even if you never get around to adding a little easy flare with view transitions, you get a free performance boost from the plugged memory leaks and Tyler’s great work refactoring SC.View. 1.10 also makes some changes under the hood which take some previously _not great practices_ and turn them into warnings or breaks. These are good changes, and enable a lot of the efficiency gains that we packed into this release, but there are some previously-common practices that trigger some new developer warnings, so I want to go over what’s causing them and how to fix it.

You should read this post if you’re receiving unexpected developer warnings to the effect of “`Developer Warning: invokeOnce called outside of the run loop. This can cause problems in production code if not addressed.`” I'm going to cover these possible causes of this issue:



	
  * Misusing .create() when defining your view layer

	
  * Using SC.MenuPane.create() when defining your view layer

	
  * Using SC.FileFieldView ever

	
  * Handling browser events directly, without setting up a run-loop




<!-- more -->




### The Background


Some quick background. **If you’re on a deadline and just need to get things fixed, you can skip this section** (though I hope you’ll come back later).

The RunLoop is one of SproutCore’s key foundational technologies. It allows SproutCore to queue changes in an orderly fashion, powers the bindings/properties/observers KVO engine, and allows for the progressive UI rendering that’s crucial for SC’s speed and scalability. It also enables the crucial invokeLast, invokeOnce and invokeNext methods. This means that any SproutCore code, whether at the framework or application level, has to run in a RunLoop, or lots of important things don’t happen. It’s why you use SC.Request instead of XHR, and SC.View events instead of DOM events.

Previously, if invokeOnce and friends were called outside of a run loop, they would simply fire one up and continue on their way. This was a flexible response, but it had some unintended consequences, and was certainly not “correct”. It also enabled some bad practices, which is what this post is about.

In v1.10, the invokeFoo methods no longer fire up a run loop if needed, instead throwing a developer warning to the console. This puts more responsibility on you to ensure that run loops happen when needed, and that you’re not inadvertently triggering certain code from outside a run loop.

So if you’ve upgraded your app and suddenly see a string of developer warnings about the run loop, here’s what’s probably causing it, and how to fix it.


### 1. SC.View#create


The most likely cause of the run loop developer warnings is the use of the `create` method when defining your view layer. Unless you’ve gotten fancy and have a method which is manually creating and appending child views, you probably not be using `SC.View#create`. (Creating views is expensive, so SproutCore goes to great lengths to defer it.)

The best practice for defining your view layer is to create an SC.Page instance, and populate it with your application’s panes. You should use SC.FooView.extend or SC.FooView.design, and the same with pane classes. Then, when you first append your pane in your app’s `main` method, make sure to use `MyApp.myPage.get(‘myPane’)` rather than `MyApp.myPage.myPane`. You should do this all the time anyway, but SC.Page’s superpower is taking uninstantiated views and panes and lazily instantiating them the first time you `get` them.

This important best practice will speed up the launch of your application by deferring view creation until the views are needed, and is highly recommended. It also happens to be the solution to this set of developer warnings: by extending or defining your views, and letting an SC.Page handle instantiation, you ensure that things happen when they're supposed to.

More details on this, if you’re curious. (Again if you're not, you can skip this paragraph.) First, creating views is expensive, so SproutCore goes to great lengths to defer it. Second, it’s important to keep in mind that all of your application’s initial setup (the actual parsing and execution of your application’s files) happens prior to your app’s `main` method, and therefore before the run loop gets going. Finally, SC.View#create calls invokeOnce to schedule deferred layout updates, for great efficiency gains when your code makes multiple layout adjustments in one runloop.


### 2. SC.MenuPane#create


The next most likely reason for these warnings is SC.MenuPane or its subclasses, which tend to be used in ways that encourage premature creation. This is a specific case of the above `create` issue, but I want to call it out specifically. If you’ve got any PopupButtonViews, for example, which take a menu property, make sure that you `extend` or `design` that MenuPane.


### 3. SC.FileFieldView


Another problematic view with v1.10 is the third-party framework view SC.FileFieldView. Unfortunately, this old but popular view badly breaks v1.10 applications, and you will need to transition away from it. The currently best-maintained branch of this view’s repo is maintained by LearnDot [here](https://github.com/learndot/sproutcore-upload/) (shout-out to the inimitable Joe Gaudet), which contains a number of better options, for example the excellent single-file-only view SC.FileChooserView.


### 4. Handling Browser Events Directly


Finally, it’s also possible that you’re actually running your own methods outside of a run loop. The most likely cause of this is direct handling of browser events that should be proxied through SproutCore. For example, you should be using SC.Request instead of directly using JavaScript’s XMLHTTPRequest, and you should be using SC.View’s event handlers (‘click’, ‘doubleClick’, ‘mouseDown’, etc.) instead of trying to set up your own DOM event handlers. If you absolutely need to handle your own browser events – for example, if you’re running WebSockets, for which SproutCore does not (yet) have a wrapper class – then you need to make sure to call SC.RunLoop.begin() at the beginning if the handler, and SC.RunLoop.end() at the end. (You can also wrap some code up in a function and pass it to SC.run(...), which accomplishes the same thing.)


### Wrapup


These tips and best practices should get you well on your way to a warning-free console, and a solid upgrade. If you still have any questions or are still seeing warnings, please hit up the [mailing list](http://groups.google.com/group/sproutcore), and if you’ve discovered a new cause of the run loop developer warnings, I’ll be sure to add it here!
