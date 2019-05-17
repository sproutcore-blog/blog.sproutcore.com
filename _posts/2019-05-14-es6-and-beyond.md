---
author: Maurits Lamers
comments: false
date: 2019-05-14
layout: post
title: ES6 and beyond part 1
---

### Introduction
This is the first part of a series of blog posts in which I want to show my
attempts in trying to see in what way SproutCore can be rewritten in more
modern JavaScript without changing the essential concepts or syntax too much.

This also provides an opportunity to show a few concepts that make SproutCore
what it is and show how they are implemented.

Since the beginning of SproutCore in 2007-2008 JavaScript has developed hugely
and changed dramatically. The most eye catching changes came with ES6, such
as classes, arrow functions, and the module system.
At the same time also the way developers dealt with the runtime environment
changed. Many of the early frameworks dealt with problems by changing the
prototypes of standard JS objects, such as Object, Array etc.
Nowadays this behavior is frowned upon, mainly because of the conflicts this
can cause when multiple frameworks meet in a page.

From the start SproutCore was conceived as a Cocoa like framework, in the sense
that the type of API it provides very much resembles that of a desktop framework.
It provides a series of Views, a Model and Controller system and to make it all
work smoothly a Key Value Observing (KVO) system.

In this post I want to mostly concentrate on the KVO system and the way this
has been implemented in a classical inheritance scheme.

<!--more-->

### SC.Object
SproutCore uses a classical inheritance scheme with mixins in order to provide
a single base object providing KVO observing. At the time JavaScript didn't
provide a way to properly inherit from Array, so the KVO observing system was
implemented as a single mixin in order to extend the standard Array prototype
to be observable.
The style of the mixin is heavily inspired by the Ruby mixins.

The basic implementation of a class is the constructor function which gets
a prototype. Class methods are made direct properties of the constructor.
As walking the prototype chain was a very expensive operation, every class is
essentially a complete new prototype, which just has copies of the functions of
its super class.
In extending a class, a new prototype object is created onto which the properties
of the original prototype are copied, as well as any new properties on mixins
or object literals given to the extend class method.

```
  MyMixin = {
    initMixin: function () {

    }
  };

  MyKlass = SC.Object.extend(MyMixin, {
    // props and methods
  });
```

In the copying of these properties a few extra additional actions are performed.
This includes the mapping of the dependent keys of computed properties, as well
as saving the information on local or remote observers that should be created.
By far the most interesting feature though is the `concatenatedProperties` array.

For every property mentioned in this array, as well as for the
`concatedatedProperties`-property itself, it will concatenate
the property value or values on the given object literal to the value of the original.

```
  MyKlass = SC.Object.extend({
    concatenatedProperties: 'test',

    test: 'test2'
  });

  MyKlass.prototype.test
  -> ['test2'];

  MySubKlass = MyKlass.extend({
    test: 'test3'
  });

  MySubKlass.prototype.test
  -> ['test2', 'test3']
```


Especially for the View layer, this is very useful. Every View has a
displayProperties property, which contains all the properties that should cause
a view to rerender when their value changes. In creating custom views, it becomes
almost impossible to break the caching behavior of a view by overwriting the
array of properties, while still being able to add your own variables to the list.

By performing these actions during the extending process, creating new objects
becomes lighter as part of the heavy lifting has already been done.
Creating an SC.Object will initialize and setup the observables and computed
properties and call all init functions of the super classes, as well as any
specific initMixin function which initialize the parts of the mixin it belongs to.

The inheritance system of SproutCore therefore has two stages. First is the
extend, which creates new classes. The second stage is the creation of objects.
This creation process essentially does another extend with the properties given,
then returns an instance of that object.

```
myObject = MySubKlass.create({
  test: 'test4'
});

myObject.get('test');
-> ['test2', 'test3', 'test4']
```

In both cases object literals are accepted as arguments. In case a method is
detected, it is given a base property which is a reference to the method it
overrides. When writing an application in SproutCore you can use the `sc_super()`
method, which is translated to a call to the base property. In Abbot (the original
Ruby build tools) this was `arguments.callee.base.apply(this, arguments)`. In
order to be ES5 strict compatible the NodeJS BT will rewrite the function to be
a named function, then calls `[name].base.apply(this, arguments)`.

This also works for the computed property and observer functions. SproutCore
provides a very nice system for indicating which functions are computed properties
by changing the Function prototype to provide the methods `.property()`,
`.cacheable()` and `.observes()` (and a few more that are hardly used).

```
myObject = MySubKlass.create({

  name: 'test',

  myComputedProp: function () {
    return this.get('test') + "!";
  }.property('name').cacheable(),

  myObserver: function () {
    console.log('name has changed');
  }.observes('name')

})
```

These functions will prepare the object to observe the changes on these properties
and invalidate caches or call the observer function in case something changes
through the `.set()` method.

### ES6 classes

The inheritance syntax of SC cannot be recreated with ES6 classes. The biggest
obstruction is the lexical binding of `super`: `super` gets bound to the object
it is used in. In classes that is the class, in an object literal that specific
object instance it creates.

SproutCore uses object literals to define options or extend a class. So, in
every case super gets bound to that object literal. Copying the function
onto a different object doesn't change this binding, so it will permanently
point to `Object.prototype` instead to the class we want to point it to.

Also, the ES6 keyword `extend` doesn't accept parameters like a function does.
Providing options or additional methods through an object literal either
requires copying the values onto the prototype, or add that object as a link in
the prototype chain. This last option would look like a nice solution, but it is
still impossible to use `super`.
As a last option, redefining functions as part of the prototype itself would
make `super` work, but requires `eval`, which is simply a bad idea and a no-go
approach.

Rewriting the inheritance using pure classes causes its own set of challenges.
As there are no hooks available to influence the extending process itself,
computing the `concatenatedProperties` moves to the object instantiation process.

The syntax of `class` also prohibit defining public or private properties, except
when the default JS getters and setters are used. It also has a way of defining methods
where the method will be converted into a named function, but there is no
return value. Because of that, the dot-method system to tag functions to be
handled as either computed properties or observers causes a syntax error.

```
class SCObject {
  isSCObject: true // syntax error

  /*
    This is an example of the default JS getters and setters.
    It is impossible though to extend this behavior into the computed
    property behavior of SproutCore

  */
  set prop() {

  }

  get prop() {

  }


  mymethod () {

  }.property()
  // syntax error, because mymethod () {} does not return a function
  // instance
}

```

Of course it is possible to set property values in the constructor function, by
either accepting an object literal or setting them manually, but that only works
properly for data properties. Overriding methods that way doesn't (again) allow
`super` to be used.

### ES6 modules

A lot of the work of the build tools currently is to make sure code loads in the
correct order for everything to work.
The ES6 module system could take over much of this work. There are also a few
issues here.

SproutCore currently relies on being able to adjust standard prototypes,
especially for Function (for the computed property and observer setup helpers),
String (add a few nice useful features), but mainly Array which is completely made
observable.

When using ES6 modules, this is still possible, but at the same time it is still
wise to reconsider this approach and to see whether that can reduced as much as
possible.

The biggest hurdle however is runtime dependencies. While later ES versions than 6
added a dynamic import, it is still available everywhere.

### Conclusion

In this post I have set out a few of the issues that cause SproutCore still not
to be rewritten in more modern versions of ES6. Next time I am going to write
about a few possible solutions.

### Comments
The SproutCore blog has moved to github pages. Please use [the issue tracker](https://github.com/sproutcore-blog/sproutcore-blog/issues) to leave any comments!
