---
author: tevans
comments: true
date: 2011-06-30 18:52:32+00:00
layout: post
link: http://blog.sproutcore.com/scrolling-in-sproutcore-part-2/
slug: scrolling-in-sproutcore-part-2
title: 'Scrolling in SproutCore: Part 2'
wordpress_id: 1433
tags:
- ScrollView
---

Continued from last week's post ["Scrolling in SproutCore"](http://blog.sproutcore.com/scrolling-in-sproutcore). Tim presents his solution for making SC.ScrollView feel awesome.


* * *


I began discussing possible solutions to the problem with Colin Campbell, who pointed me in the direction of Cappuccino as a reference implementation. Cappuccino’s scroll views were buttery smooth and offered all of the benefits that SproutCore needs. So, I began investigating.

This is what I found:
[![](http://blog.sproutcore.com/wp-content/uploads/2011/06/Evans-pic-11.png)](http://blog.sproutcore.com/wp-content/uploads/2011/06/Evans-pic-11.png)
See that blue box in the center of the screen - the one that I pointed an arrow to? This is how Cappuccino applications take scroll events. Normally, you'll never see this because it has an opacity of 0, and its purpose is to swallow scroll events. Yes. This little element, which I'll call the scroll catcher for the remainder of this discussion, takes in scroll events and then creates normalized events from it.
<!-- more -->
To remove any ambiguity on how they do scrolling, here's the code that turns scrolling into cross-platform events (with some minor omissions so we can focus on the problem at hand):


    
    
        // We lag 1 event behind without this timeout.
        setTimeout(function()
        {
            // Find the scroll delta
            var deltaX = _DOMScrollingElement.scrollLeft - 150,
                deltaY = _DOMScrollingElement.scrollTop - 150;
    
            // If we scroll super with momentum,
            // there are so many events going off that
            // a tiny percent don't actually have any deltas.
            //
            // This does *not* make scrolling appear sluggish,
            // it just seems like that is something that happens.
            //
            // We get free performance boost if we skip sending these events,
            // as sending a scroll event with no deltas doesn't do anything.
            if (deltaX || deltaY)
            {
                event._deltaX = deltaX;
                event._deltaY = deltaY;
    
                [CPApp sendEvent:event];
            }
    
            // Reset the DOM elements scroll offset
            _DOMScrollingElement.scrollLeft = 150;
            _DOMScrollingElement.scrollTop = 150;
        }, 0);
    



The scroll catcher sets its position to 150 pixels in. After that, it waits until the next event loop and then calculates the delta from the center of the element, firing off a simulated scroll event into Cappuccino using the calculated delta values. Lather, rinse, repeat.

This approach seems like it could work! When beginning an implementation that did exactly this (essentially converting the Objective-J code into JavaScript), there were a few hurdles that made it plain that this approach couldn't work well for SproutCore.

First of all, SproutCore uses the target DOM element found on native events to shoot the event off to the given view. It's really optimal for SproutCore to do this because it has a reverse hash lookup to get the view for a given element ID. Using this approach, all events after the first one will end up having a target of the scroll catcher. But we don't want that. We want the element directly underneath it.

To find that element, SproutCore needs a way to find a view given a point on the page. There's a function for that, `elementFromPoint`, but I've found that it's not a satisfactory solution because you still need to toggle the visibility of the scroll catcher. If we could get this working, then this solution could leave SproutCore with solid `mouseWheel` events for the whole framework. However, for optimization purposes, this solution is not the best since it requires touching the DOM a lot.

Here’s the idea that I’ve implemented as a working replacement for the current SC.ScrollView: 


	
  * make SC.ScrollView scrollable by native events

	
  * hide native scrollbars by making them just out of view (so we can maintain themes)

	
  * and proxy the scroll events so SproutCore will be notified about scroll events happening



 If you follow what’s going on with this solution, you'll find that it runs contrary to SproutCore philosophy that "truth is in JavaScript, not the DOM".

For a better idea of how this is working, here’s a picture:
[![](http://blog.sproutcore.com/wp-content/uploads/2011/06/Evans-pic-2-211x300.png)](http://blog.sproutcore.com/wp-content/uploads/2011/06/Evans-pic-2.png)


I’ve made SproutCore’s scrollbars transparent so you can see how this is working. You’ll see that the native scrollbar here is hidden behind SproutCore’s. You can guess that, from here it works like normal scrolling. The only difference is that the DOM notifies SproutCore that it scrolled and therefore reality must be a duality. SproutCore holds the same truth as the DOM through syncing.

Here’s what the syncing looks like:

    
    
      /**
        The current horizontal scroll offset.
        Changing this value will update both the `contentView`
        and the horizontal scroller, if there is one.
    
        @field
        @type Number
        @default 0
       */
      horizontalScrollOffset: function (key, value) {
        if (arguments.length === 2) {
          var minOffset = this.minimumHorizontalScrollOffset(),
              maxOffset = this.get('maximumHorizontalScrollOffset'),
              layer = this.getPath('containerView.layer'),
              offset = Math.max(minOffset, Math.min(maxOffset, value));
    
          this._scroll_horizontalScrollOffset = offset;
          if (layer && layer.scrollLeft !== offset) {
            layer.scrollLeft = offset;
          }
        }
    
        return this._scroll_horizontalScrollOffset || 0;
      }.property().cacheable(),
    
      /**
        The current vertical scroll offset.
        Changing this value will update both the `contentView`
        and the vertical scroller, if there is one.
    
        @field
        @type Number
        @default 0
       */
      verticalScrollOffset: function (key, value) {
        if (arguments.length === 2) {
          var minOffset = this.get('minimumVerticalScrollOffset'),
              maxOffset = this.get('maximumVerticalScrollOffset'),
              layer = this.getPath('containerView.layer'),
              offset = Math.max(minOffset, Math.min(maxOffset, value));
    
          this._scroll_verticalScrollOffset = offset;
          if (layer && layer.scrollTop !== offset) {
            layer.scrollTop = offset;
          }
        }
    
        return this._scroll_verticalScrollOffset || 0;
      }.property().cacheable(),
    



The properties for `verticalScrollOffset` and `horizontalScrollOffset` are changed, so they will set `scrollTop` and scrollLeft. This is done so we don’t end up recursing forever when we want to scroll (something that I’ve encountered when trying to proxy scroll offsets properly).

When the user scrolls, I’ve set up an event handler for scroll events, which ends up in the following function:

    
    
        /** @private
          Notify the container that the scroll offsets have changed.
         */
        scroll: function (evt) {
          var layer = this.get('layer'),
              scrollTop = layer.scrollTop,
              scrollLeft = layer.scrollLeft,
              parentView = this.get('parentView');
    
          // I'm using `verticalScrollOffset` and `horizontalScrollOffset`
          // as proxies for the the actual scroll offsets.
    
          // Since we know what the offsets are (we got the event), this
          // needs to set the cached value, and let properties know that
          // the offset changed.
          if (parentView._scroll_verticalScrollOffset !== scrollTop) {
            parentView.propertyWillChange('verticalScrollOffset');
            parentView._scroll_verticalScrollOffset = scrollTop;
            parentView.propertyDidChange('verticalScrollOffset');
          }
    
          if (parentView._scroll_horizontalScrollOffset !== scrollLeft) {
            parentView.propertyWillChange('horizontalScrollOffset');
            parentView._scroll_horizontalScrollOffset = scrollLeft;
            parentView.propertyDidChange('horizontalScrollOffset');
          }
    
          return parentView.get('canScrollHorizontal') || parentView.get('canScrollVertical');
        }
    


This is a bit tricky right here. There’s a manually cached value for the scroll offsets that gets updated on sets, but also sets the scroll offset for the element. I don’t want to set the scroll offset- I just want to notify the ScrollView that its value updated. So I change the internal cached value and notify SproutCore that the value changed. And voilà- scroll events proxying between SproutCore and the DOM seamlessly!

There’s another benefit that comes along with this approach. Since I’m syncing the DOM and SproutCore, you can use native scrollbars. You can do so using a flag called `wantsNativeScrollbars`, which will use native scrollbars instead of rendering Ace’s scrollbars.

There is a downside to this approach. When rendering collections, SproutCore can’t update the views fast enough to make sure that that the list always seems complete. With sufficiently complex item views, scrolling can be full of hitches. In the end, this means that incremental rendering will be a bit more noticeable than with the previous approach. SproutCore has no “heads-up” when scrolling is about to happen, just that it happened. We’ve encountered this in an application we’re working on and are trying to think up some ways to make scrolling work better.



* * *


This post is by Tim Evans, software engineer for [OnSIP Hosted PBX](http://www.onsip.com/).
