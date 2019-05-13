---
author: admin
comments: true
date: 2009-08-17 02:36:44+00:00
layout: post
link: http://blog.sproutcore.com/aspect-oriented-programming-and-you/
slug: aspect-oriented-programming-and-you
title: Aspect-Oriented Programming and You
wordpress_id: 118
post_format:
- Aside
---

One of the coolest parts of the new SproutCore View layer is its ability to use aspect-based programming to add behaviors to views.




[Aspect-based programming](http://en.wikipedia.org/wiki/Aspect-oriented_programming) is built on the premise that often objects that don't follow from the same class hierarchy may in fact need similar behaviors.




This is especially true in GUI programming when designers come to you and say something like "I came up with this new widget - it looks kind of like a progress bar but it acts like a button when you click on it".




In SproutCore, you capture these common behaviors in a "mixin".  A mixin is just a collection or properties and methods that are added to your class when you define it.  The view layer will actually look for specific hooks on your mixin so that you can automatically hook into the drawing engine, listen for events, etc.  It's very powerful.




Take the example above: with the button-y progress bar.    SproutCore has an SC.Button mixin that implements button-like behavior.  Just apply it to an SC.ProgressView and update a few hooks to get the API you want.





<blockquote>`MyApp.ProgressButton = SC.ProgressView.extend(SC.Button, {

> 
> // ... extra properties here
> 
> 

> 
> });
> 
> 
`</blockquote>




SproutCore comes with built in aspects that implement most of its common APIs including managing content properties (SC.Control, SC.ContentDisplay), rendering (SC.Border, SC.Shadow), and some behaviors (SC.Button).




Over time I expect we'll add more.  In the mean time, this is a great technique to learn to rapidly build high-quality views with composite behaviors without having to rewrite code.




If you want a further example of how mixins can be used, take a look at this [tutorial by FrozenCanuck](http://frozencanuck.wordpress.com/2009/08/16/creating-a-simple-custom-view-in-sproutcore-part2/) on using the SC.ContentDisplay mixin to easily auto-render a bunch of properties on a content object.
