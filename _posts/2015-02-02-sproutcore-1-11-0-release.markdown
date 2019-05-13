---
author: admin
comments: false
date: 2015-02-02 15:57:02+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-1-11-0-release/
slug: sproutcore-1-11-0-release
title: SproutCore 1.11.0 Release
wordpress_id: 2373
---

The SproutCore team is very pleased to announce the final release of SproutCore version 1.11.0. This version continues in the tradition of SproutCore releases to become the fastest, most feature-rich and most stable version of SproutCore to-date and includes several new additions and improvements to make development with SproutCore even easier and to make SproutCore apps even more impressive.

For those wishing to install SproutCore for the first time, please visit [http://sproutcore.com/install/]() for instructions. If you are upgrading from a previous version of SproutCore, simply run the following:


    
    <code>$ gem update sproutcore
    </code>



If you have any trouble installing or upgrading to 1.11, be sure to visit the mailing list [sproutcore@googlegroups.com](mailto:sproutcore@googlegroups.com) or the IRC channel #sproutcore for support. As always, the team and community are here to help!



# Highlights of Version 1.11.0



The majority of the work done in 1.11.0 was to improve the existing API and to fix bugs. The list of changes is too long to include, but the following are the highlights.



## Major New Features





### Polymorphic Records (SC.Record.prototype.isPolymorphic)



The experimental polymorphic record support has been rewritten. It is now bug free, significantly faster and included in the datastore framework by default. This allows you to support truly polymorphic record types in the store. For more information on using polymorphism, there is a detailed description and useful examples in the `SC.Record` documentation here: [http://docs.sproutcore.com/#doc=SC.Record&src=false]().



### SC.Binding Transforms



There are a few new binding transforms that can be used to reduce the amount of code you as a developer need to write. These are `string`, `integer`, `equalTo` and `mix`. The transforms `string` and `integer` are very simple and simply transform the value into a String or an Integer (according to radix argument). This is useful in particular for custom views that don't want have to coerce every possible defined property value into a String or an Integer when necessary. See here: [http://docs.sproutcore.com/#doc=SC.Binding&method=string&src=false]() and here: [http://docs.sproutcore.com/#doc=SC.Binding&method=integer&src=false]().

The `equalTo` transform is also very simple and simply returns `true` or `false` depending on whether the bound value is equal to the argument value. See here: [http://docs.sproutcore.com/#doc=SC.Binding&method=equalTo&src=false]().

Finally, the `mix` transform is a more powerful transform that may take some research to use properly. The benefit of `mix` is that it allows you to mix together multiple bound values into a single transform function. This is similar to the way that the `and` and `or` transforms work (in fact these were refactored to use `mix`), but `mix` allows you to specify a custom transform function. See here: [http://docs.sproutcore.com/#doc=SC.Binding&method=mix&src=false]().



### Cross-origin resource sharing (CORS) with credentials



To allow SC.Request to work properly with cross-site Access-Control requests, we've added a new property to `SC.Request`, `allowCredentials`. This will allow cookies and authorization headers to be sent by configuring the `withCredentials` property of the XHR request. As part of this change, `SC.Request` includes a new property, `isSameDomain`, which correctly identifies if a request is cross-origin or not and only attempts to set the `withCredentials` property when not targeting the same domain. A brief description of this property is available here: [http://docs.sproutcore.com/#doc=SC.Request&method=allowCredentials&src=false]().



### SC.WebSocket



To simplify using WebSockets and to ensure that WebSocket messaging triggers a run of the SproutCore run loop, we've added a new class `SC.WebSocket`. Using `SC.WebSocket` makes communicating with WebSockets trivial to add to any SproutCore app. For details and examples, please see the documentation here: [http://docs.sproutcore.com/#doc=SC.WebSocket&src=false]().



### SC.NestedStore



The nested store is an extremely powerful feature of SproutCore that allows for complex data management within the client. For 1.11, nested stores have been expanded slightly to support even more advanced uses. The first addition is a new property `conflictedStoreKeys` that contains a list of all store keys that are in conflict with the main store. The purpose of this is for applications that automatically update shared live data that multiple users may edit. In such a scenario, one user might be editing a record that another user already completed and saved. Using `conflictedStoreKeys` the application can check for the presence of any conflicts from new data coming in before attempting to commit the changes from the nested store. Here: [http://docs.sproutcore.com/#doc=SC.NestedStore&method=conflictedStoreKeys&src=false]().

The other addition is the new `SC.Store.prototype.chainAutonomousStore()` method, which returns a nested store that is allowed to interact directly with a remote data store. Typically, nested stores are prohibited from committing changes directly to a remote data store, instead having to commit them to the main store which would then forward the changes on to the remote data store (via a data source which handles the actual communication and integration between client and server). However, by using an autonomous nested store, you can choose to commit changes within the autonomous nested store and only push successful changes to the main store. This can simplify the process when commits to the remote are expected to fail occasionally and we wish to avoid pushing any possibly invalid data into the main store. Here: [http://docs.sproutcore.com/#doc=SC.Store&method=chainAutonomousStore&src=false]().



### Scale and Transform Origin



Scale is now a first-class layout property, correctly impacting `frame` and `clippingFrame`. If a view is scaled, the width & height of the frame will be correct as the view _appears_. For example, a view with layout equal to `{ width: 100, height: 100, scale: 2 }` will report a frame of `{ x: 0, y: 0, width: 200, height: 200, scale: 2 }`. The `clippingFrame` also takes a scaling origin into account as well and as part of this change, there are two new layout properties: `transformOriginX` and `transformOriginY`, which define the percentage (between 0.0 and 1.0) on the respective axis about which the scale transform is applied. These properties affect all transform styles and so can be used to also change the origin of a rotate style. You can learn about using layouts here: [http://docs.sproutcore.com/#doc=SC.View&method=layout&src=false]().



### Legacy Framework



SproutCore will work with browsers as old as IE7 (don't laugh, we all have customers that can not/will not move to newer browsers for some time), however in order to prepare for the day when the lowest common denominator can be raised, there is a new sub-framework within SproutCore, `:'sproutcore/legacy'`, which is meant to contain all code providing _support for legacy browsers_. Currently, this includes the existing polyfill for `window.requestAnimationFrame` and a new polyfill for `Object.keys`, but will continue to grow to include any specific workarounds for these older browsers. Because it's important for SproutCore apps to "just work" as much as possible, the legacy framework is included _by default_ by requiring `:sproutcore` in a project's or an app's Buildfile.

To build an app that will only work with the newest browsers (probably not a great idea —), you may change your Buildfile requirements to include only the specific SproutCore sub-frameworks you need. For example,


    
    <code>config :my_app, :required => [:"sproutcore/desktop", :"sproutcore/datastore"]
    </code>





## Major Changes & Improvements





### SC.Gesturable & SC.Gesture (SC.TapGesture, SC.PinchGesture, SC.SwipeGesture) Refactor



After some investigation, it was found that there were a number of issues with the built-in gesture support. For example, two touch taps would throw an exception, pinches would fail to register and in particular, supporting multiple gestures concurrently failed in a number of scenarios. In order to fix these problems, the gesture code has been rewritten from the top-down.

It is now possible to mixin `SC.Gesturable` to a view and use events to react to multiple gestures concurrently. Examples of the advanced type of behavior that the gesture code allows include,





  * Responding to single finger, two finger or any other number of touch taps, pinches (> 2 touches) or swipes individually or as a group. For example, your code may want to perform different actions when a single finger taps vs. when there is a two finger tap.


  * A touch session, the time between when the first touch begins and the last touch ends, may contain more than one gesture. For example, it's possible for the user to perform a pinch, then use a third finger to tap, then swipe the remaining fingers. At the least, the ability to perform gestures in a single touch session multiple times, makes the gesture recognition more robust against stray accidental touches.


  * Swipe gestures can now be configured to match against any combination of arbitrary angles, not just combinations of left, right, up & down.


  * Swipe gestures no longer trigger by simply moving far enough in one direction. They must also move _quickly_ and end _quickly_ (configurable).





#### How does this affect your code?



For the most part, this should have no effect on existing implementors of `SC.Gesturable`. The three built-in gestures: `SC.TapGesture`, `SC.PinchGesture`, and `SC.SwipeGesture` are still defined and they work much better than before. However if you have defined a custom `SC.Gesture` subclass, it will unfortunately not work correctly with this update. Because we felt the previous version of `SC.Gesture`'s API was too complex and incompatible with the behavior we needed to achieve, we decided it was better to rewrite it in a simpler form. We're very sorry for this backwards incompatibility, and would be happy to help with a migration (see mailing list and IRC info above).



### SC.PickerPane Pop "Out of the Anchor"



This view has been given special behavior when used with SC.View's `transitionIn` plugin support. If the plugin defines `layoutProperties` of either `scale` or `rotate`, then the picker will adjust its transform origin X & Y position to appear to scale or rotate _out of the anchor_. The result is a very nice effect that picker panes appear to pop right out of their anchors, rather than just appearing offset.
To see it in effect, simply set the `transitionIn` property of the pane to one of `SC.View.SCALE_IN` or `SC.View.POP_IN`.



### SC.ScrollView Refactor



The most ambitious undertaking in 1.11, was a total refactor of SC.ScrollView. There were a few features that we wanted to fix and improve in scroll views, such as scaling, alignment and touch handling and after a few attempts, we rebuilt it entirely from scratch method-by-method. This allowed us to question each design decision that went into the original `SC.ScrollView` and search for improvements and the result is that SC.ScrollView works better and is faster then ever before. We were able to reduce the amount of code, remove some internal observers and still do a better job of supporting touch, scale and alignment.

For example, scaling the content of a scroll view will now maintain its visual center rather than hugging the side, which dramatically improves the zooming experience. Touch gesture animations, such as the bounce back and deceleration, are now animated using `requestAnimationFrame` for smoother performance.

Here is a list of important changes,





  * SC.ScrollView.prototype.scale now works as advertised!


  * If `horizontalOverlay` or `verticalOverlay` is true, the scroll view will use `SC.OverlayScrollerView` by default. It's no longer necessary to also set `horizontalScrollerView: SC.OverlayScrollerView` in order to get overlaid scrollers.


  * Overlaid scroller bars now fade out when not in use.


  * Use `horizontalAlign` and `verticalAlign` properties to align fixed-width or -height content.


  * SC.ScrollView alignment handling has been improved for container (i.e. the scroll view) or content size changes to support the following scenarios:  





  1. The scroll view is left (or top) aligned, scrolled to the maximum right (or bottom) edge and container or content changes size: the content should stick to the right (or bottom) side.


  2. The scroll view is left (or top) aligned, scrolled to the minimum left (or top) edge and container or content changes size: the content should stick to the left (or top) side.


  3. The scroll view is right (or bottom) aligned, scrolled to the maximum right (or bottom) edge and container or content changes size: the content should stick to the right (or bottom) side.


  4. The scroll view is right (or bottom) aligned, scrolled to the minimum left (or top) edge and container or content changes size: the content should stick to the left (or top) side.


  5. The scroll view is center (or middle) aligned, scrolled to the center (or middle) and container or content changes size: the content should stick to the center (or middle).



Finally, a critical difference in the new `SC.ScrollView` is that it uses `SC.View` layout changes to position its content rather than adding margins that pushed the content beyond what its layout was set to. The reason for this change was to allow for GPU accelerated content positioning without duplicating code (the `SC.View` layout code already supports it). This means that it is possible to fix the layout of your content (layout with `top`, `left`, `width` & `height`) and set `wantsAcceleratedLayer` to `true` to get your content scrolled via GPU accelerated positioning. This can improve each scroll event render by as much as 50%.



### SC.MenuScrollView Refactor



As with the `SC.ScrollView` refactor, `SC.MenuScrollView` has been improved greatly in its implementation and performance.



### Responsive Design and Design Modes



Design modes are the answer to the problem of how to create a SproutCore web app that can handle vastly different screen size "designs", beyond just stretching and squishing, as simply as possible and without hurting performance. While CSS media queries may be used for static websites, they don't provide much value to a client side app like those made with SproutCore, primarily because using CSS to change the layout and the visibility of views would break the state of the application that exists in code.

Instead, we use the `modeAdjust` property and add simple overrides to the layout or any other properties of views that will apply for the specific design "mode". For instance, a view can be visible by default and only hidden in the small, 's' mode with a simple hash,


    
    <code>largeOnlyView: SC.View.extend({
      isVisible: true, // visible by default
      modeAdjust: { 's': { isVisible: false } } // hidden on small screens
    })
    </code>



For a demonstration of this, please visit the Showcase here: [http://showcase.sproutcore.com/#demos/Responsive%20Design]() and for more details on using design modes, see here: [http://docs.sproutcore.com/#doc=SC.Application&src=false]().



## General Changes & Fixes



There are are literally hundreds of other changes and fixes, which would take many more pages to write about. To see the entire list, please view the [Change Log](https://github.com/sproutcore/sproutcore/blob/master/CHANGELOG.md) (Note that there were three release candidates with their respective changes listed below them). Here is a small sample of the many changes,





  * Improved: When the online/offline value of `window` changes, SC.device runs the run loop.


  * Improved: Subclasses can now override bindings without issue.


  * Added: DateTime localizations are now available in French.


  * Improved: Updated to jQuery 1.11.1. Notably, there was a serious memory leak in jQuery 1.8 where the tokenCache grew continuously.


  * Improved: SC.State performance by removing expensive observers.


  * Improved: Performance of core SC methods: SC.mixin, SC.supplement as well as SC.Function.enhance. Benchmark: `SC.mixin` & `SC.supplement` ~ 58% faster


  * Improved: Removed several instances of `arguments` instantiation, which is terribly slow.


  * Added: Added `toolTip` property to `SC.MenuItemView`, and the corresponding `itemToolTipKey` to `SC.MenuView`.


  * Added: Added horizontal layout for `SC.ListView` using `layoutDirection` property.


  * Improved: SC.UndoManager has been refactored to allow easier undo action grouping.


  * Added: SC.DateTime.prototype.toFormattedString now takes '%o' formatter to specify the date's ordinal.



And the list goes on...
