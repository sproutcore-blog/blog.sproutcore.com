---
author: admin
comments: true
date: 2009-08-23 01:39:00+00:00
layout: post
link: http://blog.sproutcore.com/event-handling-in-sproutcore-10-part-1/
slug: event-handling-in-sproutcore-10-part-1
title: Event Handling in SproutCore 1.0 - Part 1
wordpress_id: 114
post_format:
- Aside
tags:
- Events
---

SproutCore is one of the first JavaScript frameworks to implement event delegation throughout the entire framework.  In this series of blog posts I'm going to explain a bit about how event delegation works and how you use it to handle events in SproutCore Views.




For starters, let's talk about what event delegation is and how its handled in SproutCore.




## What is Event Delegation?




Event delegation is a much faster and simpler way of handling events.  Rather than register listeners for every DOM event you might be interested in on a page, SproutCore _delegates_ responsibility for handling events to just six listeners added to the **window** and **document** objects.  These listeners take responsibility for calling any Views that are interested in any event that comes in.




Take the simple example shown below.  This diagram shows a simple document with a button.  When you press the mousedown on the button, it calls a method on a corresponding "View" object in JavaScript:




![Regular Delegation](http://idisk.me.com/charlesjolley/Public/Pictures/Skitch/skitched-20090822-180850.png)




So how does this look with event delegation?




In SproutCore, the object that receives delegated events is called the **RootResponder**.  (You can find it in your running app at _SC.RootResponder.responder_).  The RootResponder listens for a mousedown event on the document object.  When this event occurs, the browser will fill in a target property on the event to tell you which DOM element received the event.  The RootResponder uses this property to determine which view should actually be notified of the event, in this case the button view.


<!-- more -->


The diagram below shows how this works.




![Event Delegation](http://idisk.me.com/charlesjolley/Public/Pictures/Skitch/skitched-20090822-181433.png)




For a web application, which may be interested in hundreds of events on many different DOM elements all over the page, it's easy to see how event delegation can really improve performance.  Rather than registering event handlers for each of these DOM elements/events, SproutCore only registers six.  It waits until an event actually occurs on your page before taking the time to figure out which part of your application actually needs to handle the event.




(By the way, some other libraries are starting to implement event delegation as well.  jQuery and Prototype both are getting this feature to varying degrees.  SproutCore takes this feature a lot further than most, but as apps grow in complexity I expect this to appear in lots of other places as well so its useful to know how this technique works.)




## Listening for Events




If you don't register listeners, how do you indicate you are interested in an event?




In SproutCore this is very simple.  When you define your view subclass, just add methods to handle the events you are interested in.  (For more on creating Views in SproutCore see frozencanuck's tutorials [part 1](http://frozencanuck.wordpress.com/2009/08/14/creating-a-simple-custom-view-in-sproutcore-part1/) and [part 2](http://frozencanuck.wordpress.com/2009/08/16/creating-a-simple-custom-view-in-sproutcore-part2/).)




For example, mouseDown() is called whenever a user presses the mouse button over the top of your view's HTML.  To respond to this event, just add the method:




<blockquote>

>     
>     <code>MyApp.MyView = SC.View.extend({
>       // called whenever a mouse down event occurs
>       mouseDown: function(evt) {
>         // do something interesting here
>       }
>     });
>     </code>
> 
> 
</blockquote>




That's all you need to do.  Now your view can respond to mouseDown events.




Usually when writing SproutCore applications, it best to try to ignore the underlying HTML in your document altogether and just let SproutCore handle it.  However if you ever really need to know which HTML element the user needs to click on to get mouseDown(), it is stored in the "layer" property.  Just call:




<blockquote>this.get('layer')</blockquote>




on your view once it is onscreen.




Note that SproutCore defines events slightly differently than the built-in browser events.  In particular "click" and "dblclick" are ignored.  "mouseover" and "mouseout" are also implemented more sanely.   Keyboard event handling also requires a better understanding of the Responder chain - SproutCore's focus management system.




I'll cover these more in the next blog post.




_Any other topics you want covered?  Let me know in the comments!_
