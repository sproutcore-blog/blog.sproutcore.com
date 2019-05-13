---
author: admin
comments: true
date: 2010-01-29 12:13:06+00:00
layout: post
link: http://blog.sproutcore.com/testing-and-auto-generated-ids-in-sproutcore/
slug: testing-and-auto-generated-ids-in-sproutcore
title: Testing and auto-generated ids in SproutCore
wordpress_id: 66
post_format:
- Aside
tags:
- Testing
---

[martinottenwaelter](http://martinottenwaelter.fr/post/355872976/testing-and-auto-generated-ids-in-sproutcore):




<blockquote>

> 
> If you’re trying to automate tests of your [SproutCore](http://sproutcore.com) application with [Selenium](http://seleniumhq.org/), for example, you’ll realise that the HTML element ids are automatically generated. They change every now and then and break all your tests.
> 
> 

> 
> To get rid of this problem, you can override the `layerId` method of certain view classes to generate a stable, and human readable, id.
> 
> 

> 
> The following code takes the view hierarchy, and generates an id based on the parents’ names. For example, the `mainPage.mainView.someOtherView.theTargetView` view will be given the `mmsome.theTargetView` id.
> 
> 
</blockquote>


 
