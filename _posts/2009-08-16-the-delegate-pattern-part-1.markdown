---
author: admin
comments: true
date: 2009-08-16 17:31:51+00:00
layout: post
link: http://blog.sproutcore.com/the-delegate-pattern-part-1/
slug: the-delegate-pattern-part-1
title: The Delegate Pattern (part 1)
wordpress_id: 119
post_format:
- Aside
---

[joshholt](http://blog.thesempiternalholts.com/post/164245451/the-delegate-pattern-part-1):




<blockquote>

> 
> In my previous post I promised some information on the “Delegate Design Pattern”, how Sproutcore uses it, and how to take advantage of it. In part 1 I will try my best to describe the Delegate Design Pattern. In part 2 I will explain this pattern in the context of Sproutcore ( with examples ), and part 3 is still in the works.
> 
> 

> 
> **_What is the “Delegate Design Pattern” ?_**
> 
> 

> 
> Let’s talk about the meaning of a delegate. In languages such as C#, Java, etc… you usually think of a delegate as nothing more than a function pointer. In languages such as Objective-C, javascript, ruby, etc… you can think of a delegate as an instance of a class (an object) to which work is delegated. It may or may not be obvious how powerful this concept is, so I’ll give an example:
> 
> 

> 
> In most applications you will inevitably need to display a list of data. There are several approaches to get the data into the list. You could use straight data binding and cram all of the data into your view ( inefficient ) and let the view deal with pagination and so on, or you can use a delegate with data binding. The use of a delegate will allow the view to just worry about displaying data and it decouples the view from the model. In this case the delegate and the controller ( sometimes the same object ) work together to provide the data that the list needs at any given time.
> 
> 

> 
> Given a list in this fashion you can set up the view so that all it cares about is it’s size and that it is displaying a “name property”.  The List can then ask the controller for the data it needs and only the data it needs based on it’s size. The controller will then [call | invoke] a method on the delegate to calculate the number of records that can be displayed in the area of the list, then it returns this number of records to the controller and the controller will give this to the list(view) and it gets displayed.
> 
> 

> 
> **There are at least two distinct advantages that I can think of here:**
> 
> 

> 
>   1. In straight data binding it becomes too easy to tie your view down to just one specific model.
> 

>   2. In straight data binding your controller will stuff all of the result-set (RecordArray) down the list’s throat and expect the list to be ok with it, not choke and spew. What I’m trying to get at here is that this can really be inefficient.
> 

> 
> Well that’s it for my humble explanation of the delegate design pattern, In the next post I will expand on my example of a list view and show you how this pattern is used in sproutcore’s CollectionView.
> 
> 
</blockquote>


 
