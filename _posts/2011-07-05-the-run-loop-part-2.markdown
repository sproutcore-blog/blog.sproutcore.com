---
author: tkeating
comments: true
date: 2011-07-05 14:00:32+00:00
layout: post
link: http://blog.sproutcore.com/the-run-loop-part-2/
slug: the-run-loop-part-2
title: 'The Run Loop: Part 2'
wordpress_id: 1413
tags:
- Run Loop
---

Previously, we delved into the operation of SproutCore's RunLoop, a powerful mechanism that we rarely work with directly. While understanding the function of the Run Loop is akin to understanding the function of your vehicle's transmission– you don't need to know how it works in order to go really fast – they both definitely help you go really fast.

So, as promised in the last post, let's look a bit further at what we get out of having a Run Loop in SproutCore.


## You DOM the Truth?  You DOM the Truth!?  The DOM can't handle the Truth!


In a lot of web applications, the first wall that developers hit as the application grows in complexity is that they can no longer keep data synchronized throughout the application.  This is typically because they're using selectors to pull and push data to and from the DOM and it quickly gets out of hand, in particular when you add the complexity of synchronization with a backend and multiple event entry points.

SproutCore's answer to this has always been that the application has a single "truth" which is maintained in the Model layer. To represent a change in the View layer, you make a change to the underlying Model data and let bindings take care of the rest.
<!-- more -->
So why mention this in a post about the Run Loop?  Well, partially because I had that possibly hilarious "DOM the truth" subtitle lined up, but mostly it's because it's easy to imagine that an improper MVC implementation could still result in inconsistencies between the View and Models. Therefore I wanted to re-highlight a component of the Run Loop's function that was touched on in the previous post, which is to recursively flush all the bound properties until the application's state is guaranteed to be in sync.

For instance, suppose property A is bound to property B and property B is bound to property C. With SproutCore, when we change property C, we know that by the end of the current Run Loop, the change will have propagated fully such that property A is correct.  This is important, because there are several ways to have a property change, and as a developer you shouldn't have to provide for every possible event, callback or expired timer.

So the Run Loop helps make MVC work, and that's nice, and I have a little warm feeling in my heart or possibly pancreas, but really how does this make my application faster?


## The Sauce that Makes SproutCore Apps Faster


So what happens when we want to render our data?  Take the Todos example for instance, [Getting Started with SproutCore 2.0](http://guides.sproutcore20.com/getting_started.html).  You'll notice that there is a "Mark All as Done" checkbox that is bound to the controller's `allAreDone` property. By setting the value of `allAreDone`, it will in turn set each of the item's `isDone` values to match.  You'll also notice that the `remaining` property will also change as each item's `isDone` property changes, and that this is bound to the `remainingString` of the StatsView.

To summarize, if we have 100 items in our Todos list, checking `allAreDone` is going to change 100 `isDone` properties.  If we traversed and updated the DOM to display `remainingString` each of these times, we would have a serious problem on our hands.  This is where the Run Loop comes in.

Although the StatsView is bound to `remainingString`, because we have ordered execution within the RunLoop, SproutCore can delay rendering any views until _after_ all of the bindings have flushed.  This means that once the bindings have flushed, StatsView will be rendered, `remainingString` will be calculated once, and we only traverse and update the DOM once for those 100 changes!

This is a very important piece of SproutCore's architecture and shouldn't be taken lightly, because what this means is that even the most complex web applications with several hundred bindings can still remain fast. This is, as far as I know, unique among JavaScript MVC frameworks.


## Conclusion


Thanks for following along.  Now that we've explored all that the Run Loop does, how it does it, and why it does it, you can feel free to tuck it in the back of your brain knowing that as long as you are using SproutCore with a proper MVC architecture and bindings, your app will run faster than it would with any other JavaScript framework.
