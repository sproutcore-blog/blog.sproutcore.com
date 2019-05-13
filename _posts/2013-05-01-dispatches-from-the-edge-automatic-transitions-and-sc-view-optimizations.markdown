---
author: tkeating
comments: false
date: 2013-05-01 19:39:25+00:00
layout: post
link: http://blog.sproutcore.com/dispatches-from-the-edge-automatic-transitions-and-sc-view-optimizations/
slug: dispatches-from-the-edge-automatic-transitions-and-sc-view-optimizations
title: 'Dispatches From the Edge: Automatic Transitions and SC.View Optimizations'
wordpress_id: 2144
tags:
- Dispatch
- Features
---

Version 1.10 is shaping up to be a fundamental advancement of SproutCore as the best framework for creating powerful user experiences on the web.  We've already been doing the best of breed practices for creating dynamic web applications for some time.  For example, running in the client, maintaining the application "truth" in code, minimizing touching the DOM and many other practices that keep SproutCore apps as fast as possible.  These features allow you to create extremely complex interfaces that update instantly as the user interacts with them.  However, while instant updates were a major advancement, they can give the interface a jarring feel and therefore the next level of application design is to go beyond instant updates and add "life" or "play" to your user interface with subtle transitions.

As such, SproutCore 1.10 will include a new automatic transition architecture that is so easy to use, developers can actually play around with complex transitions while first implementing a view rather than needing to commit more time to it later.  To do so, you simply specify a transition plugin to use during one of the four state changes: appending, becoming visible, becoming hidden and removing.  To make it even easier, SproutCore includes a few built-in transition plugins: SC.View.FADE, SC.View.MOVE, SC.View.BOUNCE, SC.View.SPRING and SC.View.SCALE and it's very easy to write your own transition plugins to do any type of advanced animation based on the SC.Transition protocol.

<!-- more -->

Here's an example,

    
    MyApp.MyView = SC.View.extend({ 
      // Automatic transition on append to document
      transitionIn: SC.View.SCALE,
    
      // Automatic transition on isVisible set to true from false
      transitionShow: SC.View.BOUNCE,
    
      // Automatic transition on isVisible set to false from true
      transitionHide: SC.View.SPRING,
    
      // Automatic transition on remove from document
      transitionOut: SC.View.FADE
    
    });


In this example, when the above view is appended via its pane being appended or by being added to a parent view that is already appended it will automatically scale smoothly in.  When the view's isVisible property is set to false, the view will spring out and when the property is set back to true it will bounce back in.  Finally, when the view is removed it will fade out.  All of which replaces the regular jarring appearances and disappearances with smooth transitions.

Each transition plugin has default values that it uses and to fine tune the transition, you can also provide a simple corresponding transition options object that will be used.  For example,

    
      // …
      transitionShow: SC.View.MOVE,
    
      // Move in from the bottom and ease-out over 0.8 seconds
      transitionShowOptions: {
        direction: 'bottom',
        timing: 'ease-out',
        duration: 0.8
      },
      // …


Note that SproutCore's built-in transitions work with any type of layout (they temporarily convert flexible layouts to fixed layouts for moving for example) and can all be hardware accelerated.  To hardware accelerate a transition, set _wantsAcceleratedLayer_ to true on the view.

_Be warned that hardware accelerated rendering causes the font smoothing to change from subpixel antialiasing to regular antialiasing so you will need to either:  only hardware accelerate the top most layers (i.e. highest z-index) and/or add -webkit-font-smoothing: antialiased; to text so that you don't see a flicker in Webkit browsers._

Lastly, I wanted to mention a lot of the work that made these transitions possible.  In 1.10, SC.View has been refactored to implement a simple internal statechart.  This makes the current state of the view precisely known and allows for the addition of transitionary states for building in, showing, hiding and building out, but there is more to it than that.  Because the view state is explicitly maintained, we can use the current state to ensure that only the right actions are performed and can further optimize SC.View for speed.  For example, display property observers are no longer created when the view is created and are now instead created only if it is rendered and are also removed if the view's layer is destroyed.  This reduces the creation time for some views by more than half.

Other optimizations and improvements include:



	
  * added _willShowInDocument_, _didShowInDocument_, _willHideInDocument_ and _didHideInDocument_ view notifications.  This allows for the removal of all _isVisible_ observers outside of the one in SC.View.

	
  * changes to the _layout_, _layerId_ or _isFirstResponder_ properties no longer cause the entire layer to update, only their respective layer attributes

	
  * changes to any display property no longer cause the _id_, _style_ and _class_ attributes to update, only the layer contents

	
  * speed improvement in determining _isVisibleInWindow_ status of views

	
  * new _createdByParent_ property that is used by several SproutCore container style views to properly destroy child views that they create and thus avoid memory leaks

	
  * removed _layerNeedsUpdate_ observer from SC.View

	
  * removed _isVisibleInWindow_ observer from SC.CollectionView

	
  * removed _layer_ observer from SC.ImageView

	
  * calling _removeAllChildren_ is optimized to destroy all child view layers in one action rather than destroying them one at a time

	
  * internal style manipulation has been improved to avoid clearing the style attribute momentarily before setting the new style

	
  * removal of many lines of code due to previously having to handle an unclear view state


All of these changes are now available in the master branch of SproutCore and will be released with version 1.10 as soon as they have had a bit of time to be thoroughly tested.

Finally, you can see the new transitions in action with a brand new demo:  [Creating Playful Interfaces](http://showcase.sproutcore.com/#demos/Creating%20Playful%20Interfaces). Be sure to check out the demo's [source](https://github.com/sproutcore/demos/tree/master/apps/lively_view_demo) to see how easily all the transitions are added.
