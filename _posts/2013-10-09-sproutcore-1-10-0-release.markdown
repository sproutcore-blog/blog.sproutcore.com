---
author: admin
comments: false
date: 2013-10-09 04:37:17+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-1-10-0-release/
slug: sproutcore-1-10-0-release
title: SproutCore 1.10.0 Release
wordpress_id: 2226
---

The SproutCore team is very pleased to announce the final release of SproutCore version 1.10.0. This version is the fastest, most feature-rich and most stable version of SproutCore to-date and includes several new additions and improvements to make development with SproutCore even better and to make SproutCore apps that much more impressive. For a quick introduction to the many changes in version 1.10, please check out the official [press release](http://sproutcore.com/assets/MajorNewSproutCoreRelease-1.10.pdf).

For those wishing to install SproutCore for the first time, please visit [http://sproutcore.com/install/](http://sproutcore.com/install/) for instructions. If you are upgrading from a previous version of SproutCore, simply run the following:


    gem update sproutcore


If you have any trouble installing or upgrading to 1.10, be sure to visit the mailing list [sproutcore@googlegroups.com](mailto:sproutcore@googlegroups.com) or the IRC channel #sproutcore for support. As always, the team and community are here to help!


# Highlights of Version 1.10.0


In this release we dug deep into the core of SproutCore to improve the entire development and runtime experience from start-to-finish. This includes clean-ups of the developer API to improve consistency and memorability; brand new features for automatic layout, transition animations and live updates; extensive internal architectural refactors to boost speed and reduce memory consumption; and more.

<!-- more -->We're sure you will find that this is the most stable, usable and best performing version of SproutCore ever. As such, this is a massive update and there are so many improvements and fixes that we can't possibly cover them all, but here is a list of the key features:


## New Features




### Automatic Child View Layout


In 1.10 we introduce the [`childViewLayout`](http://docs.sproutcore.com/#doc=SC.View&method=childViewLayout&src=false) plugin property of `SC.View`.  This is an incredibly useful utility that makes defining and updating the user interface much easier.  For example, to create a long form previously, you would need to specify the layout of each child view, which was a tedious task.  As well, making an adjustment to the layout of any child view, meant a lot of effort updating all the following child views and it was really difficult to make a live adjustment, say to show an error message under a field for example.

In 1.10, you can now set a child view layout plugin that contains the logic to automatically lay out the child views for you. The plugin architecture is quite simple, so you can create custom child view layouts of your own, but you likely will never need to since the two plugins bundled with SproutCore take care of most needs. These are `SC.View.VERTICAL_STACK` and `SC.View.HORIZONTAL_STACK`, which will automatically lay out the child views in a stack either vertically or horizontally respectively. If the layout of a child view is adjusted, the plugin will re-lay out all the remaining views as efficiently as possible.

Of course, you can use the `SC.FlowedLayout` mixin to perform this and there are actually a lot of similarities between `childViewLayout` plugins and `SC.FlowedLayout`, but `childViewLayout` is significantly easier to use and can be swapped in or out and configured on the fly much more easily. As was already noted, the plugin architecture makes it even easier to create custom layout engines that can be shared among projects and the community. And `childViewLayout` works with the new transition plugins for creating amazing new user interfaces.  See `childViewLayout` in action [here](http://showcase.sproutcore.com/#demos/Child%20View%20Layouts).


### Automatic SC.View Transitions


One of the coolest new features in 1.10 is the addition of `SC.View` transition [plugins](http://docs.sproutcore.com/#doc=SC.View&method=transitionHide&src=false). Similar to the `childViewLayout` plugin, these plugins can be set on views to automatically modify the behavior of the view. For example, instead of simply appending a dialog pane, which is jarring to the user, we can set `transitionIn`: `SC.View.POP` to have it pop in. This allows us to quickly add subtle animations as our views are added, removed, shown, hidden or moved. The overall effect is that the user interface feels smoother and more alive. Best of all, it's so simple to add transition plugins, the challenge will be to not overdo it (* seriously, don't overdo the animations. For users, a little animation is better than nothing, but nothing is better than too much).

There are now five SC.View state changes that you can have transition automatically:




  * `transitionIn`: Animate each time the view/pane is appended to the document. Ex. `SC.View.BOUNCE_IN`


  * `transitionOut`: Animate when the view/pane is removed from the document. Ex. `SC.View.SLIDE_OUT`


  * `transitionShow`: Animate when the view is made visible from being hidden. Ex. `SC.View.SPRING_IN`


  * `transitionHide`: Animate when the view is hidden from being visible. Ex. `SC.View.FADE_OUT`


  * `transitionAdjust`: Animate when the view's layout is adjusted. Ex. `SC.View.SMOOTH_ADJUST`


As you can see in the examples above, SproutCore includes several built-in transition plugins. For transitionIn and transitionShow you can use `SC.View.BOUNCE_IN`, `SC.View.FADE_IN`, `SC.View.POP_IN`, `SC.View.SCALE_IN`, `SC.View.SLIDE_IN` and `SC.View.SPRING_IN`. Likewise, each of these has a matching outgoing transition for use with transitionOut and transitionHide: `SC.View.BOUNCE_OUT`, `SC.View.FADE_OUT`, `SC.View.POP_OUT`, `SC.View.SCALE_OUT`, `SC.View.SLIDE_OUT` and `SC.View.SPRING_OUT`.

You can also transition most layout adjustments and SproutCore includes plugins for `transitionAdjust`: `SC.View.BOUNCE_ADJUST`, `SC.View.SMOOTH_ADJUST` and `SC.View.SPRING_ADJUST`. You will want to use `transitionAdjust` when some other code is adjusting the child views automatically (e.g. a `childViewLayout` plugin) and you want everything to smoothly change.  For example, notice how removing a child view has a smooth transition in this [demo](http://showcase.sproutcore.com/#demos/Child%20View%20Layouts)?

See these transition plugins in action [here](http://showcase.sproutcore.com/#demos/Transition%20Plugins).


### Automatic `SC.ContainerView` Transitions


Last, but not least, there is one more view that received the [transition treatment.](http://docs.sproutcore.com/#doc=SC.ContainerView&src=false) `SC.ContainerView` is a workhorse view that is used extensively in SproutCore and now in 1.10, animating the view swapping is dead simple. SproutCore now includes built-in `transitionSwap` plugins for use by `SC.ContainerView`: `SC.ContainerView.DISSOLVE`, `SC.ContainerView.FADE_COLOR`, `SC.ContainerView.MOVE_IN`, `SC.ContainerView.PUSH` and `SC.ContainerView.REVEAL`.

Just like the other transitions, it is simply a matter of setting the property on the view like so,


      transitionSwap: SC.ContainerView.PUSH


And just like all the plugins, you can easily define custom transitions for even more impressive view swapping. See the container view transitions in action [here](http://showcase.sproutcore.com/#ui/SC.ContainerView).


### Application Cache


One of SproutCore's main goals has always been to provide all the tools a developer needs to create professionally quality web software as quickly as possible and 1.10 makes this easier in many ways, one of which is to make it easier to provide offline support and live software updates for your users. This is all possible using the browser's application cache, but the complex behavior and states of the application cache make it difficult and time-consuming to work with directly.

Instead, SproutCore 1.10 introduces [`SC.appCache`](http://docs.sproutcore.com/#doc=SC.appCache&src=false) which is a simple object that  abstracts out the most important properties of  the application cache for developers to use.  This is done with the following observable properties on `SC.appCache`: `hasNewVersion`, `isNewVersionValid`, `progress` and `isReadyForOffline`.

Using these properties you can update your UI to show the progress of the app cache as it loads or when the application is ready for offline state (i.e. cached), you can check for a new version of your app while running using `SC.appCache.get('hasNewVersion')` and you can even prompt your users to upgrade (i.e. reload) their running apps live.  So as you can see, with `SC.appCache` you will find lots of easy ways to make your SproutCore app's user experience just a little bit more amazing. Note, this can be especially useful in a test environment, where you want to ensure that the testers aren't running the old version (which happens frequently when application cache is enabled and not managed).


### `SC.CollectionView` Performance Increase


Perhaps the change that will have the most noticeable impact on your app is the automatic collection view DOM and item pooling. This is functionality that you would have had to have a deep understanding of `SC.CollectionView` and the now deprecated, `SC.CollectionFastPath` to use previously. That is no longer the case, because it is on by default in 1.10. This means that not only does `SC.CollectionView` optimize list rendering by only rendering the visible items, it now also does this by pooling and re-using the item views and DOM elements so that scrolling through gigantic lists is even smoother.

As part of this work, you will notice a marked improvement of `SC.ScrollView` + `SC.CollectionView` (`SC.ListView` or `SC.GridView`) on mobile.

The caveat to this performance boost is that all item view subclasses should implement render and update. The update function is of critical importance since it allows an existing item view in memory to be re-used with new content and update the layer in place rather than destroying and creating a new item view and layer for each item.

You can read more about this change [here](http://blog.sproutcore.com/dispatches-from-the-edge-super-fast-collections/).


### `SC.DateTime` Additions


Formatting dates and times is always a tricky subject, in particular when localization is concerned. SproutCore has always had excellent date time support in [`SC.DateTime`](http://docs.sproutcore.com/#doc=SC.DateTime&src=false) and in 1.10 this gets even better. You can now use a special SproutCore-only formatter, `%E`, with `SC.DateTime` to return the elapsed time from or since now. This makes it easy to show more human readable time spans like "Right now" or "Last week".

There is an entire set of default values from the number of years ago to right now to a number of years in the future and of course the strings are completely configurable and localizable. For example,


      var date = SC.DateTime.create();
      date.toFormattedString("%E"); // "Right now"

      date.advance({ minute: 4 });
      date.toFormattedString("%E"); // "In 4 minutes"

      date.advance({ day: -7 });
      date.toFormattedString("%E"); // "About a week ago"


There is also a new `SC.DateTime` instance method, difference, which allows you to very easily compute the number of weeks, days, hours, minutes, or seconds between two dates.


### [Animation](http://docs.sproutcore.com/#doc=SC.View&method=animate&src=false)


Animation saw a lot of love in 1.10. Part of this was to pave the way for automatic transitions and part of it was to make using animation even simpler. The biggest change for those already using SproutCore is that calling `SC.View.prototype.animate` now always runs in the next run of the run loop via `invokeNext`. This solves the chronic problem having to wrap a call to animate within an `invokeLast` function so that we could be sure that the DOM had been updated so that the CSS transition would run. Wondering why animations failed to run properly should no longer be an issue in 1.10.

We've also added a new option `delay` to delay the start of the animation and added `SC.View.prototype.cancelAnimation` so that you can cancel animations and revert to where it started, where it was going or even in place (* which is extremely hard to do considering that some animations use CSS transforms, but yeah SproutCore can handle it).

You can also now animate `centerX` and `centerY` and if you animate the `height` or `width` of a centered view, SproutCore will automatically animate `margin-left` and` margin-top` to make the animations smooth.


### Cascading Enabled State


Just like the animation changes should make basic SproutCore development that much easier, we've also reworked `isEnabled` to help you lock down your UI in one simple step. For example, it's often nicer to edit some content modally in place rather than throwing up a modal pane to block the entire UI. However, while editing the content in place we may still want to prevent other visible controls from being active.

While you could search out and bind up every control's isEnabled property so that you could turn them all off, this is a lot of work and prone to error. Instead, isEnabled will now cascade actively to all child views so you can disable whole sections of your app simply by setting `isEnabled` on the top-most view for the section.

Since this cascading can be blocked by any child view by setting `shouldInheritEnabled` to false, you could even set `isEnabled` to false on the main pane and still keep a section of child views separately enabled.


### Overall Performance Increase


The best feature of 1.10 is the one without a specific tagline, but 1.10 results in a large performance increase over previous versions. For instance, `SC.View` has been completely refactored to allow for faster view creation, rendering and updates and improvements to the rendering architecture means that many of `SC.View`'s subclasses, in particular the big three: `SC.ButtonView`, `SC.LabelView` and `SC.CollectionView` were able to be further optimized to use much less memory. For instance, we removed probably a dozen display observers just from these three classes alone, which makes a noticeable difference in how fast these views can be instantiated and the effect they have on run time performance.

This release also includes several memory leak fixes that would have gradually slowed down a previous app. For example, migrating a large 1.9 app to 1.10 resulted in that app being runnable on iPad one, where previously it would crash after several minutes.


### Miscellaneous






  * Improves the regular expression used by `SC.RenderContext` to escape strings so that HTML entities like `&apos;` or `&agrave;` are preserved.


  * Removes the blockers that prevented all browsers that support touch events from using mouse events. This prevented certain configurations of later versions of IE from receiving mouse events.


  * Adds the concept of Infinity to `SC.IndexSet`. Although, the number of indexes will always be constrained to `Number.MAX_SIZE`, attempting to create a range even in the several hundreds of thousands would freeze the client, because it will attempt to generate hints every 256 items. Instead we can use the concept of Infinity and avoid hinting the infinite range. For one, this allows for infinite arrays and infinite lists to be possible without using really large numbers that are very slow to hint.


  * Adds `isEditable`, `isDeletable` and `isReorderable` support for item views. This change uses `canEditContent`, `canDeleteContent` and `canReorderContent` to indicate whether to add the respective properties to the item views. For example, this allows you to toggle `canReorderContent` to hide or show a drag handle on item views that have `isReorderable` as a display property. Note: Setting isEditable to false on the collection view overrides the three other properties.


  * Adds '`sc-item`' class to non-group collection items. Otherwise, you can apply styles to groups, to items and groups, but not items individually without adding custom class names to the example view.


  * Adds `createdByParent` property that is set to true when the view was instantiated by its parent through `createChildView`.


  * Prevents memory leaks and simplifies the code of several views by using `createdByParent` to identify when the child view being removed was automatically created and should now be destroyed.


  * Adds updated SproutCore image [assets](https://github.com/sproutcore/sproutcore/tree/master/frameworks/foundation/resources/images).


  * Renames `SC.FILL_PROPORTIONALLY` to `SC.BEST_FILL`. `SC.FILL_PROPORTIONALLY` is still supported but no longer documented.


  * Allows `SC.State` to represent the empty ("") route. Previously, there was no way for a state to represent the empty route using representRoute:. Now a state can set `representRoute: ""` to be triggered when the empty route is fired.


  * Added platform detection for the Apache Cordova (formerly phonegap) javascript-to-mobile bridge.


  * Added retina stylesheet support to module loading, style sheets were being generated but not loading.


  * Removes `backgroundColor` observer from all `SC.View`s. If anyone actually uses this property AND needs it to update, they'll have to add the `displayProperty` themselves.


  * Makes `SC.ToolbarView` more intelligent about it's styling: not just styled appropriately for top alignment, layout adjusted to include a top or bottom border.


  * Refactors the `SC.PickerPane` positioning code for `SC.PICKER_POINTER` and `SC.MENU_POINTER`. With this refactor, the picker pane properly positions itself on the most appropriate side and will slide itself up/down or left/right if it can in order to fit.


    * adds ability for pointer to automatically adjust its position as the pane shifts left/right or up/down regardless of its size


    * fixes pane positioning to take into account the borderFrame


    * adds `windowPadding` property that ensures pickers are positioned a certain amount of distance from all edges of the screen


    * deprecates the `extraRightOffset` property since the pointer positions itself now





  * Removes the restriction that render delegate data sources can only retrieve `displayProperties` properties. This restriction is not especially helpful, but worse than that, it forces us to have excess display properties, which means excess observers being set up and running although not every property that effects the display necessarily needs to be observed.


  * Adds an '`[]`' observer to the array when an '`@each.key`' observer is used. Previously, changes to the array's membership would noisily call `propertyDidChange` while setting up key observers on each additional item. This change gets rid of this shotgun approach that resulted in multiple fires of the observer when adding multiple new items to the array. It also fixes the problem that removing items from the array also failed to call a change to the array.


  * Adds debug mode only warnings if `invokeOnce` or `invokeLast` are called outside of a run loop. This should prevent developers from writing custom event handling code outside of the run loop, which can cause strange race condition bugs.


  * Improved performance of scroll view on iOS significantly by using request animation frame.


  * Optimizes destroy of `SC.View`. This is a slow part of the view lifecycle, due to recursively running through every descendant and notifying `willRemoveFromParent`, `didRemoveFromParent`, `willRemoveChild`, `didRemoveChild` as well as searching through and clearing all of the childViews arrays. This cuts the destroy time almost in half for the average view tree.


  * All errors are actual `Error` objects, which provide more debuggable stack traces.


  * Updates jQuery framework to 1.8.3 and removes buffered jQuery.


    * Patches jQuery to prevent security warnings in IE.





  * Improves animation support for current and future browsers. The previous platform checks prevented using accelerated layers on non-webkit platforms, plus any browser that dropped the prefixes would indicate that they did not have support for transitions and transforms.


  * Requesting an index beyond the length of a sparse array should not trigger an index or range request on the delegate and just returned undefined. If you need to prime a sparse array to start loading without setting a length, it's best to use `sparseArray.requestIndex(0)`.


  * The SC.Store.reset() method now also clears out all of the record arrays.


  * Added `SC.browser.cssPrefix`, `SC.browser.domPrefix` and `SC.browser.classPrefix`.


  * Added `SC.browser.experimentalNameFor()`, `SC.browser.experimentalStyleNameFor()` and `SC.browser. experimentalCSSNameFor()` methods for working with experimental browser properties in a[ future-proof manner](http://docs.sproutcore.com/#doc=SC.browser&method=.experimentalNameFor&src=false).


  * Added `SC.UNSUPPORTED` constant.


  * The `animate()`function can now accept a target argument as well as a method.


    * if no target is given the view itself will be the value of `this` in the callback. Previously, this would be the `layoutStyleCalculator`, an internal object of SC.View.


    * the `animate()` function is thoroughly documented now, including notes on how to hardware accelerate position changes.





  * `resetAnimation()` has been renamed to `cancelAnimation()`, because reset indicates 'revert', but the default behavior doesn't revert the layout. Reset animation didn't work before either.


    * added `SC.LayoutState` enum for use by `cancelAnimation()`.





  * fixes `hasAcceleratedLayer` to be dependent on the layout. Previously, adjusting a non-accelerated layout to an accelerate-able layout failed toupdate the property and `hasAcceleratedLayer` would be incorrect.


  * Makes `invokeNext` trigger the next run of the run loop if none is scheduled. This makes invokeNext the appropriate method to use when needing the DOM to be up-to-date before running code against it.


  * Refactors `SC.RenderContext`to simplify the API, introduce consistent naming and make it behave appropriately. This should remove the guess work about whether a function is or is not supported by the context and make it easier to remember the names and parameters of each method.


    * There are now 3 similar access methods: `attrs()`, `classes()`, `styles()`


    * There are now 3 similar add methods: `addAttr()`, `addClass()`, `addStyle()`


    * There are now 3 similar remove methods: `removeAttr()`, `removeClass()`, `removeStyle()`


    * There are now 2 similar reset methods: `resetClasses()`, `resetStyles()`


    * Duplicate and inconsistent method names have been deprecated: `css()`, `html()`, `classNames()`, `resetClassNames()`, `attr()`





