---
author: admin
comments: true
date: 2009-08-24 01:36:11+00:00
layout: post
link: http://blog.sproutcore.com/event-handling-in-sproutcore-10-part-2-dragging-a-view/
slug: event-handling-in-sproutcore-10-part-2-dragging-a-view
title: Event Handling in SproutCore 1.0 - Part 2 - Dragging a View
wordpress_id: 112
post_format:
- Aside
tags:
- Events
---

In my [last post](http://blog.sproutcore.com/post/169308465/event-handling-in-sproutcore-1-0-part-1) I introduced event delegation in SproutCore and the basics of how to handle events.   In this post I'm going to build on this foundation to show you how you can add event handlers to drag a view around the window.*




## Introducing the Mouse Events




As I noted in the first post, SproutCore recognizes several different types of mouse events.  Most of these events are essentially the same events sent by most browsers, though some differ significantly in order to give you tighter control.




Remember that to listen for events, you just need to add a method to your view with the same name.  Here is a quick rundown of the different methods you can add to your view:




  * **mouseDown()** - Called when the mouse button is pressed while over your view.   You must return YES (i.e. true) from this method for mouseDragged() or mouseUp() to be called.


  * **mouseDragged()** - Called when the mouse is moved while the button is pressed.  This is only called if you returned YES from mouseDown().


  * **mouseUp()** - Called when the mouse button is released.  Only called if you returned YES from mouseDown().


  * **mouseOver()** - Called when the mouse enters the view's visible area.


  * **mouseOut()** - Called when the mouse leaves the view's visible area.


  * **mouseMoved()** - Called whenever the mouse is moved while over the view.



It's important to note that all of these events, except for mouseDragged() and mouseUp() are sent first to the view that is directly under the mouse pointer at the time of the event.  mouseDragged() and mouseUp() only happen after a mouseDown() event.  They are always sent first to the view that implemented mouseDown() AND returned YES (or true) from that method.




Events do bubble up your view hierarchy using something called a Responder Chain, but that will be the subject for another post.




Event handler methods are always passed an SC.Event object describing the event.  This class provides a consistent cross-platform API for accessing event info.  In general, it follows the API conventions for the built-in Event object on Firefox.


<!-- more -->


## Listening For Dragging




So, let's say we want to create a view that can be dragged around the screen.  To do this, we need to implement three of the above event handlers: mouseDown(), mouseDragged() and mouseUp().




Let's start with mouseDown().  The primary purpose of this method is to setup any information we need to save to handle dragging and, of course, to return YES so that we get our other calls.  Here's some good starter code:



    
    <code>MyApp.MyDragView = SC.View.extend({
    
      mouseDown: function(evt) {
        var layout = this.get('layout');
        this._mouseDownInfo = {
          pageX: evt.pageX, // save mouse pointer loc for later use
          pageY: evt.pageY,
          left:  layout.left, // save layout info 
          top: layout.top
        };
        return YES; // so we get other events
      }
    
    });</code>




The mouseUp() handler is also pretty simple.  It just needs to do some cleanup.  Basically delete the mouseDownInfo hash and return YES to indicate that the event has been handled:



    
    <code>  mouseUp: function(evt) {
        // apply one more time to set final position
        this.mouseDragged(evt); 
        this._mouseDownInfo = null; // cleanup info
        return YES; // handled!
      }</code>




Note that this method also calls mouseDragged().  This is the same method that will be called whenever the mouse is moved with the button pressed.  The reason you want to call this method again here is to give the view one last chance to position itself with the position mouse location.  Otherwise you might find your view will occasionally "miss" your last drag just before you release the mouse.




So with mouseDown() and mouseUp() handled, we just need to add the dragging support.  This is where the magic happens.  All we do in this method is compare the current location of the mouse against the original location of the mouse at mouseDown().  We then adjust the location by this same delta from the original position.  Here's how this looks in code:



    
    <code>  mouseDragged: function(evt) {
        var info = this._mouseDownInfo,
            loc;
     
        // handle X direction
        loc = info.left + (evt.pageX - info.pageX);
        this.adjust('left', loc);
    
        // handle Y direction
        loc = info.top + (evt.pageY - info.pageY) ;
        this.adjust('top', loc);
    
        return YES ; // event was handled!
      }</code>




One interesting thing to pay attention to here is the way we calculate the new location of the view.  Most developers write dragging code for the first time by examining the current mouse location against the last time mouseDragged() was called.  Then they adjust the top/left by the delta.  This code instead saves the mouse and view location at mouseDown() and compares against that.




Note also the use of adjust().  This method is an easy way to adjust one or more layout parameters on your view without having to generate a whole new layout object.  It is very efficient for rendering.




The reason we take this approach here is because you want the offset of the mouse, relative to the view, to always remain fixed while you drag around.  Sometimes when you just look at the delta between events, this won't happen.  It is usually always better to write UI code using this kind of "instantaneous point" approach - where calling a method with the same params will always have the same results, regardless of how it was called in the past.




## Putting It All Together




So that's all there is to it.  Three methods and you've added nice professional draggable views to your UI.  To help finish this example out, I'm going to add a property called "isDragging" and update the render() method of the view to add/remove a class name when that changes.  This will allow you to draw the view highlighted.  Here's how the view looks when you put it together:



    
    <code>MyApp.MyDragView = SC.View.extend({
    
      // ..........................................................
      // DISPLAY
      // 
    
      // class name is added to the output HTML  
      classNames: 'my-drag-view',
      
      // becomes YES when a drag becomes.
      isDragging: NO,
      
      // make sure view will auto-rerender.
      displayProperties: 'isDragging'.w(),
      
      render: function(context, firstTime) {
        // add/remove class name.  Use CSS rule like this to style:
        // .sc-view.my-drag-view.dragging 
        //
        context.setClass('dragging', this.get('isDragging'));
      },
    
      // ..........................................................
      // EVENT HANDLING
      // 
      
      mouseDown: function(evt) {
      
        // indicate dragging - rerenders view
        this.set('isDraggin', YES);
        
        var layout = this.get('layout');
        this._mouseDownInfo = {
          pageX: evt.pageX, // save mouse pointer loc for later use
          pageY: evt.pageY,
          left:  layout.left, // save layout info 
          top: layout.top
        };
        return YES; // so we get other events
      },
      
      mouseUp: function(evt) {
      
        // no longer dragging - will rerender
        this.set('isDragging', NO);
        
        // apply one more time to set final position
        this.mouseDragged(evt); 
        this._mouseDownInfo = null; // cleanup info
        return YES; // handled!
      },
      
      mouseDragged: function(evt) {
        var info = this._mouseDownInfo,
            loc;
     
        // handle X direction
        loc = info.left + (evt.pageX - info.pageX);
        this.adjust('left', loc);
    
        // handle Y direction
        loc = info.top + (evt.pageY - info.pageY) ;
        this.adjust('top', loc);
    
        return YES ; // event was handled!
      }
      
    
    });</code>




Now you know how to do basic mouse event handling.  Next we're going to head into keyboard land.  Before that, however, you'll need to learn another key concept with events: the Responder Chain




--




* Note that SproutCore also has a generic facility for drag and drop called SC.Drag.  SC.Drag is better for complex operations and will eventually integrate with the browser-based drag/drop events in HTML5.  But that is a topic for another day.
