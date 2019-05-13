---
author: tevans
comments: true
date: 2011-06-23 18:01:22+00:00
layout: post
link: http://blog.sproutcore.com/scrolling-in-sproutcore/
slug: scrolling-in-sproutcore
title: Scrolling in SproutCore
wordpress_id: 1400
tags:
- ScrollView
---

Converting native widgets into SproutCore compatible widgets can be an adventure, especially if the browser vendors don't agree on the events that the widget produces. Scrollable elements are one of those things.

For those of you who find SproutCore's ScrollView insufferable on various platforms because it's not scrolling how you expect it to, this should shed some light on how **really hard** the problem actually is. And, hopefully you’ll be satisfied with the solution that I propose.

First, let me answer the question of _why_… Why, that is, SproutCore needs its own ScrollView. There are two primary reasons for this: cosmetic and performance.

The cosmetic reason is theming. SproutCore has the ability to skin pretty much everything in your application, including scrollbars. This gives a consistent look and feel across platforms and eases the headache of UI consistency. However, some people want their applications to have the native look and feel. The current implementation of SC.ScrollView doesn’t allow that. This can be a turnoff, especially when mixing-and-matching SC.ScrollView and native scroll views. It creates inconsistency, which leads to bad user interaction.

SproutCore prides itself on being able to render gigantic lists of items without hosing your browser. It does this by incrementally rendering the list. This means that what you see is all there is with SC.ListView. Anything you can’t see is not actually rendered in the DOM. Implementing this requires SproutCore to know about the clipping frame (the rectangle that gives the information on what’s currently visible). To get the clipping frame, SproutCore needs to observe when scrolling happens. Hence, SC.ScrollView.

Now for a quick dig into the internals of how 1.x SC.ScrollView works in "desktop" mode, so when we start looking at our solutions, we know what stuff is changing.

I'm going to take it backwards from where the `scrollTop` and `scrollLeft` are set in the DOM being controlled by SC.ScrollView. For those of you who'd like to follow along, I'm looking at the adjustElementScroll function in scroll.js in the desktop framework.

I'm going to break this down, 'cause this function contains the core of what makes SC.ScrollView tick.


    
    
      /** @private
        Called at the end of the run loop to actually adjust the scrollTop
        and scrollLeft properties of the container view.
      */
      adjustElementScroll: function() {
        var container = this.get('containerView'),
            content = this.get('contentView'),
            verticalScrollOffset = this.get('verticalScrollOffset'),
            horizontalScrollOffset = this.get('horizontalScrollOffset');
    



Pretty self-explanatory, continuing on...


    
    
        // We notify the content view that its frame property has changed
        // before we actually update the scrollTop/scrollLeft properties.
        // This gives views that use incremental rendering a chance to render
        // newly-appearing elements before they come into view.
        if (content) {
          // Use accelerated drawing if the browser supports it
          if (SC.platform.touch) {
            this._applyCSSTransforms(content.get('layer'));
          }
    
          if (content._viewFrameDidChange) { content._viewFrameDidChange(); }
        }
    



Here's the first interesting bit. Ignoring the accelerated drawing, which is for the touch version of SC.ScrollView, we have the last line calling `content._viewFrameDidChange`. Hmm. What does that do? 
<!-- more -->
Let's take a respite from this function and find out what _viewFrameDidChange does. Digging around, you find the function call in `core_foundation/views/view/layout.js`. This function is pretty straightforward:

    
    
      /** @private
        Invoked by other views to notify this view that its frame has changed.
    
        This notifies the view that its frame property has changed,
        then propagates those changes to its child views.
      */
      _viewFrameDidChange: function() {
        this.notifyPropertyChange('frame');
        this._sc_view_clippingFrameDidChange();
      }
    



So this let's the view know that it's frame changed, then makes a call down to `_sc_view_clippingFrameDidChange`. Digging again, we end up in `core_foundation/views/view.js`.


    
    
    /** @private
        This method is invoked whenever the clippingFrame changes, notifying
        each child view that its clippingFrame has also changed.
      */
      _sc_view_clippingFrameDidChange: function() {
        var cvs = this.get('childViews'), len = cvs.length, idx, cv ;
        for (idx=0; idx<len; ++idx) {
          cv = cvs[idx] ;
    
          cv.notifyPropertyChange('clippingFrame') ;
          cv._sc_view_clippingFrameDidChange();
        }
      }
    



This code is also fairly straightforward. It simply notifies all views that are descendants of the current one that their `clippingFrame` changed.

Back to `adjustElementScroll`, we're at the point where the content is notified that the scroll offset did change. This lets the child view know _beforehand_ that it is going to scroll. This is used to make incremental rendering of collection views appear seamless to the user (effectively making collections look like continuous for most platforms).

Here's the last part of `adjustElementScroll`:


    
    
    if (container && !SC.platform.touch) {
          container = container.$()[0];
          
          if (container) {
            if (verticalScrollOffset !== this._verticalScrollOffset) {
              container.scrollTop = verticalScrollOffset;
              this._verticalScrollOffset = verticalScrollOffset;
            }
    
            if (horizontalScrollOffset !== this._horizontalScrollOffset) {
              container.scrollLeft = horizontalScrollOffset;
              this._horizontalScrollOffset = horizontalScrollOffset;
            }
          }
      },
    



Aha! See `scrollTop` and `scrollLeft` getting set? That's where the view gets scrolled. The next step is to see what triggers this function to be called.

Just above `adjustElementScroll` are two functions that invoke it, when `horizontalScrollOffset` or `verticalScrollOffset` change. For those familiar with the SproutCore adage "reality is in JavaScript, not the DOM", this is one great example of it being put to use to great benefit.

I'm going to save some time and jump to where scroll events are handled, in `mouseWheel`.

Inside the code for `mouseWheel` and its dependent function `_scroll_mouseWheel`, there are some curious things happening. The first line of the mouseWheel function has a delta adjust for webkit browsers that mutates the event from the browser. This is the first glimpse at how troublesome scrolling is for SproutCore.  We’re going to dig into `SC.Event` to get the rest of the story of how scroll events are dealt with.

Walking through `SC.Event` (in `core_foundation/system/event.js`), we find this code relating to scroll events:


    
    
    // Normalize wheel delta values for mousewheel events
      if (this.type === 'mousewheel' || this.type === 'DOMMouseScroll' || this.type === 'MozMousePixelScroll') {
        var deltaMultiplier = SC.Event.MOUSE_WHEEL_MULTIPLIER,
            version = parseFloat(SC.browser.version);
    
        // normalize wheelDelta, wheelDeltaX, & wheelDeltaY for Safari
        if (SC.browser.webkit && originalEvent.wheelDelta !== undefined) {
          this.wheelDelta = 0-(originalEvent.wheelDeltaY || originalEvent.wheelDeltaX);
          this.wheelDeltaY = 0-(originalEvent.wheelDeltaY||0);
          this.wheelDeltaX = 0-(originalEvent.wheelDeltaX||0);
    
        // normalize wheelDelta for Firefox
        // note that we multiple the delta on FF to make it's acceleration more 
        // natural.
        } else if (!SC.none(originalEvent.detail) && SC.browser.mozilla) {
          if (originalEvent.axis && (originalEvent.axis === originalEvent.HORIZONTAL_AXIS)) {
            this.wheelDeltaX = originalEvent.detail;
            this.wheelDeltaY = this.wheelDelta = 0;
          } else {
            this.wheelDeltaY = this.wheelDelta = originalEvent.detail ;
            this.wheelDeltaX = 0 ;
          }
    
        // handle all other legacy browser
        } else {
          this.wheelDelta = this.wheelDeltaY = SC.browser.msie || SC.browser.opera ? 0-originalEvent.wheelDelta : originalEvent.wheelDelta ;
          this.wheelDeltaX = 0 ;
        }
    
        // we have a value over the limit and it wasn't caught when we generated MOUSE_WHEEL_MULTIPLIER
        // this will happen as new Webkit-based browsers are released and we haven't covered them off
        // in our browser detection. It'll scroll too quickly the first time, but we might as well learn
        // and change our handling for the next scroll
        if (this.wheelDelta > SC.Event.MOUSE_WHEEL_DELTA_LIMIT && !SC.Event._MOUSE_WHEEL_LIMIT_INVALIDATED) {
          deltaMultiplier = SC.Event.MOUSE_WHEEL_MULTIPLIER = 0.004;
          SC.Event._MOUSE_WHEEL_LIMIT_INVALIDATED = YES;
        }
    
        this.wheelDelta *= deltaMultiplier;
        this.wheelDeltaX *= deltaMultiplier;
        this.wheelDeltaY *= deltaMultiplier;
      }
    



I think that this code speaks for itself, showing how complex and inconsistent scroll events are. There is no unanimous agreement across browser vendors as to how scroll events should be interpreted. There are some standard ways that they should be interpreted for traditional mice, but this uniformity breaks down when using pixel precise input devices like the ones found on Apple’s current generation of devices (magic trackpad / magic mouse, etc.).

These new devices are new to the industry, so browser vendors are trying to figure out a way to interpret the events. Unfortunately, there hasn’t been any agreement on what the events should look like. This means that as the code stands now, members of the core team have to test browsers that support these devices and ensure that they have equivalent (or similar) behavior to the native widgets.

As of now, the current state of SC.ScrollView is tightly coupled to browsers, down to specific versions of them, to correctly compute scroll events. The views don’t feel as responsive as they do in native applications, and it hiccups every once in a while, resulting in a user experience that is... well, lacking.

I think that SproutCore can do better, so I started brainstorming ideas of how to make SC.ScrollView feel awesome.



* * *


This post is by Tim Evans, software engineer for [OnSIP Hosted PBX](http://www.onsip.com/).

Stay tuned for next week's post, where Tim will walk you through his solution to scrolling in SproutCore.
