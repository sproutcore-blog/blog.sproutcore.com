---
author: admin
comments: true
date: 2009-05-22 22:15:44+00:00
layout: post
link: http://blog.sproutcore.com/introducing-scfreezable-and-sccopyable/
slug: introducing-scfreezable-and-sccopyable
title: Introducing SC.Freezable and SC.Copyable
wordpress_id: 157
post_format:
- Link
tags:
- Features
---

Link: [Introducing SC.Freezable and SC.Copyable](http://github.com/sproutit/sproutcore/commit/3b4725276916a900d181d78cee8118d66777215b)

		

Following up on my earlier post about adopting ES5 conventions.  One of the API changes we recently made to SproutCore 1.0 was the introduction of the SC.Freezable and SC.Copyable mixins (linked to this post).




SC.Freezable adds a freeze() method to objects that use it.  In ES5 engines, this will actually freeze the object so that further modifications raise an exception.  Today, it simply sets the isFrozen property to YES.  Mutating methods can then be implemented to throw an exception if they are called while the object isFrozen.




Freezing is most useful in conjunction with the SC.Copyable mixin.  This mixin defines some standard methods for copying an object.  copy() returns a clone of the object.  frozenCopy() returns a clone of the object that has been frozen.  If you call frozenCopy() of an object that is already frozen, the method simply returns itself.




This pattern is great because now if you want to modify an object, you can get a copy by calling copy().  Even if the object is frozen, you'll get a new object that is not frozen.  Likewise, if you want to keep a copy of the object around for later use and you want to be sure it won't change, you can use frozenCopy().  If the object you are working on is already frozen, this won't allocate more memory and slow your program down, so its really efficient.




One of the big reasons ES5 introduces the concept of freezing is to make it easier to work with objects as a kind of primitive type.  For example, a Range - with an start and a length value - should often be treated like a primitive value like a number; once it is created it can never be changed.  Freezing makes this possible.




By using SC.Freezable, copy(), frozenCopy() you can take advantage of this new capability in ES5 in your SproutCore applications today simply by following this simple protocol.
