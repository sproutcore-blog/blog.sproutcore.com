---
author: tkeating
comments: false
date: 2014-11-07 18:52:32+00:00
layout: post
link: http://blog.sproutcore.com/developer-journal/
slug: developer-journal
title: Developer Journal
wordpress_id: 2337
---

Since there has been so much activity in SproutCore lately in the run up to 1.11.0, I thought it would be best to start a more regular update on the changes occurring in master. While we occasionally highlight a specific new feature in depth through a "Dispatches from the Edge" post, there are actually hundreds of small, yet interesting, changes occurring weekly that aren't large enough to warrant their own post. It's my hope to capture these changes in a weekly to bi-weekly developer update. So let's begin with the last couple of weeks (Note: no changes are final).



## Touchy Mice



If you own an Apple Magic Mouse, you may have found some web apps difficult to use. A notable public example of this problem was in the Google Maps app. When you released your finger after dragging the map around, the extra mouse wheel events that were sent as your finger was lifted caused the map to zoom in and out rapidly. Now I believe Google has fixed that problem with their app and we have as well for SproutCore's `SC.SliderView` and `SC.ScrollView`, both of which use mouse wheel events. To prevent the extra mouse wheel events that can occur on click or release from triggering the control, we ignore any mouse wheel events that fire while the mouse is pressed up until 250ms after the mouse up event. Depending on how adept your users are with their mice clicks, the result may be a huge improvement or barely perceptible, but even as small a change as it is to prevent scrolling jiggle on mouse click, it's just one more brick in the incredible user experience wall that we're trying to build with SproutCore.



## Performance



We've been working diligently on `SC.ScrollView` performance (more on that later), but in the process we've implemented some other performance improvements.

We fixed a problem with excessive layout updates for certain types of views. If a view used `viewDidResize` to check for size changes and then make further adjustments to its position, the adjustments to its position would have appeared as further changes to its size. In particular, `SC.PickerPane` suffered from this, since it re-positions itself whenever its size changes.

Speaking of `SC.PickerPane`, this one got a performance scrub down. You may not have been aware, but `SC.PickerPane` now has some special code enabling it to appear within scrollable content and move correctly when the content scrolls. It's a really nice advanced feature, but there were a couple of issues hampering the performance of it. The first was that the scroll view observers were too greedy observing offsets of the scroll view for changes and repositioning on each change. What this meant was that an `SC.PickerPane` could reposition itself up to 6 times in a single run loop as the content of the scroll view changed. Instead, the proper pattern for observing multiple properties (or noisy properties) is to filter the input through an `invokeX` (i.e. so even though 6 calls to the observer function may occur, we only call `positionPane` once). Additionally, we no longer observe the offsets if the scroll view can't even scroll and finally, there is a bug fix in there too. When the picker's anchor gets moved on its own, we ensure that the anchor is in its new position _before_ we re-position.

One of the most important classes within SproutCore has been sped up a bit too. `SC.State` had two `observes` helper functions used to be notified when its `enteredSubstates` and `currentSubstates` arrays changed. Since these arrays are modified by the owner statechart, the observers needed to be chained enumerable observers. However, this resulted in slower object initialization for each state object and excess observer firing as the entered and current substates change. Instead, we simply notify the target state directly each time that the owning statechart makes a change to its `enteredSubstates` and `currentSubstates`. This one has has a couple benchmarks to site:

Benchmarks:





  * initStatechart in unit tests: ~21ms to ~13ms (~38% faster)


  * initStatechart in large application: ~81ms to ~51ms (~37% faster)



While a reduction of 30ms in a, generally once run, method isn't much to write home about, we are relentless in shaving every possible millisecond that we can. More notably, we've recently made some serious performance improvements to the core SC methods: `SC.mixin`, `SC.supplement` as well as to `SC.Function.enhance`. `SC.mixin` and `SC.supplement` iterated the `arguments` object to insert a boolean flag to pass to a private function that then iterated the `arguments` again in order to remove the flag argument, which is totally unnecessary. Instead, `SC.mixin` and `SC.supplement` iterate the `arguments` once and pass the new Array to the private function, removing the need for a second iteration.

More importantly though, is that these three areas no longer access the `arguments` object to copy it, which required the browser to instantiate it and is costly. Instead, we now do a fast copy (similar to this: [http://jsperf.com/closure-with-arguments]()) without instantiating the `arguments` object. By doing a fast copy of arguments these functions are now optimizable by V8.

Benchmark: `SC.mixin` & `SC.supplement` ~ 58% faster

Also,`SC.RenderContext`'s `setStyle` method was updated so that it could be optimized for V8 as well.



## `SC.ScrollView` and `SC.MenuScrollView` Refactor



This one will actually get its own blog post. For now, I just wanted to mention that these views have seen massive refactoring. The purpose of the changes has been to simplify the logic, which had gotten fairly unruly, but more importantly to grind and grind on the little details so that scrolling and scaling should feel as good and as natural as possible. We'll post an in-depth on `SC.ScrollView` in the next couple weeks.



## `SC.MenuPane` Tidy



We fixed `SC.MenuPane` automatic resizing to fit within the window. The positioning code used in `SC.PickerPane` failed to apply adjustments to the width or height of the pane, which had been calculated in order to fit long menus within the window. This included improving the menu positioning code to respect the value of `windowPadding` and fixing a problem where the items array was not observed for content changes if it was set on create.

We removed an unnecessary layout change in `createChildViews`, which also meant that creating a menu pane as a singleton (i.e. with no run loop) would throw `invokeOnce` warnings.

**WARNING** We removed the `SC.MenuPane.VERTICAL_OFFSET` property. `SC.PickerPane` already has a provision for offsetting panes from the window's edges, `windowPadding`, and that is the property that is being used now.



## General fixes and changes



Finally, there are always a large number of little changes. Here are some from the last few weeks.





  * Removed an extra call to `SC.RootResponder`'s `computeWindowSize` each time that a pane is appended. This is unnecessary, since the root responder recomputes its window size property whenever the window actually resizes.


  * Improved the default styling of overlay scroller views. Making them look more like natural overlay scrollers in OS X and making them more visible against dark backgrounds.


  * Improved the view management of `SC.ContainerView` a bit. If `contentView` is set as an uninstantiated view class, it will instantiated correctly (you should set `nowShowing` though normally).


  * Fixed `SC.ObserverSet` to pass the given context to the observer method. `SC.ObserverSet.prototype.add()` accepts a third argument, `context`, but it did not actually pass it along to the observer method.


  * Improved `SC.MenuItemView` handling of submenus. Previously if the item's submenu was visible and the mouse exited back onto the menu item view, it tried to re-append the same submenu. Instead, it now checks to see if its submenu is already attached before attempting to enter it again.


  * Fixed a bug in `SC.ContainerView`'s override of `set` so that it may be chainable.


  * Did you know you can cancel animations created with `animate` _in place_? This includes `transform` transitions whose in place value is represented as a 4x4 matrix that must be decomposed to find the current value for translate, scale and rotate in the three planes. We're still working on rotation around the X and Y axis, but all other transforms can be cancelled. A demo on this will come later.



I apologize that this post is quite long, if it actually included all the work in the scroll and scroller views it would be three times longer, but as you can see, there is a lot going on. I hope to keep these posts much shorter from now on by keeping them more regular.
