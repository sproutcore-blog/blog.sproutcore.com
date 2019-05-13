---
author: dcporter
comments: false
date: 2013-04-15 18:11:22+00:00
layout: post
link: http://blog.sproutcore.com/classnamebindings-easy-dynamic-css/
slug: classnamebindings-easy-dynamic-css
title: 'classNameBindings: Dynamic CSS classes made easy'
wordpress_id: 2127
tags:
- Docs
- Features
---

As a mature framework, SproutCore is full of little features to make common tasks drop-dead simple – including some hidden gems. I recently added some documentation to the framework (and to the indispensable [docs.sproutcore.com](http://docs.sproutcore.com)) for one of them, and wanted to highlight it here on the blog too.

Dynamically adding and removing CSS classes on a view is a common need — for example, to swap background images when a property changes. But there's no obvious way to do this; I burned my share of time trying to crack it manually, and I've watched other devs do the same. The usual solution ends up being a custom renderer, but that's messy and verbose, operates at the wrong level of abstraction, and opens the door to all kinds of bugs if you're not intimately familiar with the render API.

Enter classNameBindings. It's is a quirky but powerful little property that makes dynamic class names a breeze. (No relation to the convenience key format [fooBinding](http://guides.sproutcore.com/core_concepts_kvo.html), by the way.) Here's what classNameBindings looks like:

<!-- more -->

`classNameBindings: ['isRed:my-red-view', 'isUpsideDown'],
isRed: YES,
isUpsideDown: NO`

The classNameBindings property is an array of strings. My first entry here is in the format 'localProperty:mediated-css-property' – the class 'my-red-view' will be appended to the view's layer whenever the local property isRed is true, and will be removed if isRed turns false (or null or undefined). If you don't specify a class, then the property name itself will be dasherized and used; so in my second entry, the local property 'isUpsideDown' will mediate the class 'is-upside-down'. It just works!

You can get fancy with it, too. (Here be dragons.) If your property's value is not strictly boolean, that value will be used as the mediated class name instead. For example:

`classNameBindings: ['ketchupClass'],
hasKetchup: false,
hasKetchupBinding: SC.Binding.oneWay('MyApp.condimentController.ketchup'),
ketchupClass: function() {
if (this.get('hasKetchup')) return 'is-covered-in-ketchup';
else return 'ketchup-free';
}.property('hasKetchup').cacheable()`

By returning a string, the ketchupClass property can directly control what class gets injected into the DOM. Be careful with this, though: numbers will be appended verbatim, and objects will be stringified, leading to unintended results like `class="4"` and `class="object Object"`.

A couple footnotes. First, classNameBindings are implemented, not surprisingly, with some hidden KVO -- which is fine as long as you aren't in a rapidly-scrolling CollectionView, in which case you should reduce your reliance on this and all other bindings. Second, if you specify classNameBindings on a subclass, it stacks with superclass values rather than overriding, just like displayProperties and classNames do. Finally, if you want to hook up dynamic DOM attributes instead of classes, go experiment with the closely-related attributeBindings property.

That's all for now. Be well, write beautiful code, and contribute back.
