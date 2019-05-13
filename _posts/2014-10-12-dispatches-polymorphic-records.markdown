---
author: tkeating
comments: false
date: 2014-10-12 17:40:20+00:00
layout: post
link: http://blog.sproutcore.com/dispatches-polymorphic-records/
slug: dispatches-polymorphic-records
title: 'Dispatches From the Edge: Polymorphic Records'
wordpress_id: 2322
tags:
- Dispatch
---

We have good news for anyone using the experimental `polymorphism` framework from within SproutCore. You'll be glad to know that it has now made its way into the official `datastore` framework as part of `SC.Record`. If you have been using this framework, you'll be even more glad to learn that polymorphic records are now significantly faster and more memory efficient. As well, this change includes a critical bug fix that resulted in polymorphic records getting mismatched when their `id` was changed.

For those interested in what this change means, here's how it works. First, if you're not familiar with polymorphism, it's similar to inheritance, but differs in that polymorphic subclasses share a common "identity". Here's what that means with respect to the data model. In typical inheritance, the subclasses inherit the traits (attributes) of their superclass, but they can't stand-in for that superclass (i.e. their identity or type is unique). In polymorphic inheritance, the subclass still inherits the traits of the superclass, but is now also considered to be the "same" type as the superclass. This means that when you query for records of a polymorphic super type, you'll also receive records of all the polymorphic sub types.

This is especially useful functionality, because data is often stored in exactly this type of generic manner. It's typical in SQL databases to have a large table where certain attributes apply to one specific subtype of the data, other attributes apply to another subtype and some attributes apply to all. With polymorphism, we can model this situation precisely.

So how do we use it in SproutCore? It's simply a matter of adding the `isPolymorphic` property to a record class and extending it. Let's look at an example from the SC.Record documentation that will hopefully clear up any remaining confusion on how polymorphism works.

    
    // This is the "root" polymorphic class. All subclasses of MyApp.Person 
    // will be able to stand-in as a MyApp.Person.
     MyApp.Person = SC.Record.extend({
       isPolymorphic: true
     });
    
    // As a polymorphic subclass, MyApp.Female is "equal" to a MyApp.Person.
     MyApp.Female = MyApp.Person.extend({
       isFemale: true
     });
    
    // As a polymorphic subclass, MyApp.Male is "equal" to a MyApp.Person 
    // also. Not it is not "equal" to a MyApp.Female.
     MyApp.Male = MyApp.Person.extend({
       isMale: true
     });
    
    // Load two unique records into the store.
     MyApp.store.createRecord(MyApp.Female, { guid: '1' });
     MyApp.store.createRecord(MyApp.Male, { guid: '2' });
    
    // Now we can see that these records are in fact "equal" to each other. 
    // Which means that if we search for "people", we get "males" & 
    // "females".
     var female = MyApp.store.find(MyApp.Person, '1'); // Returns record.
     var male = MyApp.store.find(MyApp.Person, '2'); // Returns record.
    
    // These records are MyApp.Person as well as their unique subclass.
     SC.kindOf(female, MyApp.Female); // true
     SC.kindOf(male, MyApp.Male); // true
    



Enjoy!
