---
author: tkeating
comments: true
date: 2011-09-15 18:41:10+00:00
layout: post
link: http://blog.sproutcore.com/hubbub-%e2%9d%a4-sproutcore-socket-io-modular-loading/
slug: hubbub-%e2%9d%a4-sproutcore-socket-io-modular-loading
title: Hubbub ❤ SproutCore - Socket.IO & Modular Loading
wordpress_id: 1837
tags:
- Tutorial
---

As promised in my last post, I'll go into more detail on some of the technical aspects of [Hubbub](https://hubbubapp.com). And since there was only a single request to talk about Socket.IO integration with SproutCore, that's the topic for today. In order to keep these posts down to a nice bite-sized length, today will strictly be about how Hubbub uses SproutCore's modular loading to include Socket.IO.



## Socket.IO! I Choose You.



There is actually some nice stuff that happens in Hubbub in real time if you have the app open. For example, if someone sends you a message, signs out an item to you, makes a new item available, or any number of other events occur, then the application updates instantly without requiring a page reload. Sure it's not new, but with Socket.IO and SproutCore it's also not a difficult-to-implement kludge.

So for those that haven't yet tried it, Socket.IO is available [here](http://socket.io/). There are really good instructions on using Socket.IO on their site, but it's so simple I will include my entire setup here.



### My Setup - Server Side



Hubbub's app server is written with [Node](http://nodejs.org/) and [Express](http://expressjs.com/). So after installing Socket.IO, there's nothing more to getting it working server-side than:


    
    app = require('express').createServer({key: …, cert: …, ca: …});
    io = require('socket.io').listen(app);
    app.listen(3443);



Note: I use port 3443 locally with TLS/SSL encryption, which is not strictly necessary.<!-- more -->



### My Setup - Client Side



On the client side, you need to first retrieve the Socket.IO JS from the server. Initially, I added the Socket.IO script to my copy of `index.rhtml` directly above the `javascripts_for_client` statement. This simply pulls the JavaScript from the server on page load like the Socket.IO default examples show and if you want to do the same and aren't using a custom `index.rhtml`, then the instructions for copying `index.rhtml` are listed at the top of the original [file](https://github.com/sproutcore/sproutcore/blob/master/lib/index.rhtml).

However, I'm just not satisfied with Hubbub being anything less than the best application it can be, and the first improvement I made to reduce loading times was to load Socket.IO dynamically. Without getting into the details of how I use Statecharts, the application begins basically like this:

[caption id="attachment_1839" align="aligncenter" width="245" caption="Initial States Diagram"][![](http://blog.sproutcore.com/wp-content/uploads/2011/09/hubbub-initial-states-diagram-2-245x300.png)](http://blog.sproutcore.com/wp-content/uploads/2011/09/hubbub-initial-states-diagram-2.png)[/caption]

Notice that I don't load Socket.IO until the application reaches the Ready state. The following details describe exactly how I've done this.



## 1. Directory Structure



To make Socket.IO available to all the apps in my Hubbub project, I wanted it to be its own framework. The relevant directory structure I used is this:


    
    hubbub/
       frameworks/
          socket.io/
             modules/
                io/
             resources/



I then copied `socket.io.min.js` and `WebSocketMain.swf` from `./node_modules/socket.io/node_modules/socket.io-client/` into my project like so:


    
    hubbub/
       frameworks/
          socket.io/
             modules/
                io/
                   socket.io.min.js
             resources/
                WebSocketMain.swf





## 2. Buildfile



The files are now where I want them, but SproutCore's build tools won't load anything in the `frameworks` or `modules` directories unless told to do so, plus I still need to proxy the Socket.IO traffic to my local development server. Here is the relevant part of my Buildfile:


    
    config :hubbub,
       :required => [
          :'socket.io'
       ],
       :deferred_modules => [
          :'socket.io/io'
       ]
    
    proxy '/socket.io',
       :to => 'localhost:3443',
       :secure => true, # Hubbub is entirely over HTTPS
       :timeout => 25 # A longer timeout for polling transports



I've required `:'socket.io'` here as an example, which isn't strictly necessary. The reason you may want to do this is so that `frameworks/socket.io/resources/` will be included in the builds, and therefore if you were to use `flashsocket` as a transport mechanism, you would be able to set `WEB_SOCKET_SWF_LOCATION = sc_static('WebSocketMain.swf');` (see the Socket.IO FAQ).

Also notice that the `socket.io/io` module is deferred. Therefore it won't be fetched until we tell SC.Module to do so. That way, we can pass through our initial application states without any background loading interfering with the more important task of getting people into the app as quickly as possible.



## 3. Load the Code



Finally, to load Socket.IO I added the following to Hubbub's READY state:


    
    enterState: function() {
    
          // Load Socket.IO and initialize it when it is ready
          SC.Module.loadModule('socket.io/io', this, this.initializeSocketIO);
    
        },
    
        initializeSocketIO: function() {
    
          socket = io.connect('https://localhost:3443');
    
          socket.on('connect', function() {
            // ... for a later post





### Cool Beans



At this point, I see the following in my development console after reaching the READY state:


    
    SC.Module: Attempting to load 'socket.io/io'
    SC.Module: Module 'socket.io/io' is not loaded, loading now.
    SC.Module: Loading JavaScript file in 'socket.io/io’ -> '/static/socket.io/io/en-ca/current/javascript.js?1315847166'
    SC.Module: Module 'socket.io/io' finished loading.
    SC.Module: Evaluating and invoking callbacks for 'socket.io/io'.
    SC.Module: Module 'socket.io/io' has completed loading, invoking callbacks.
    RTM: Welcome to Hubbub Real Time Messaging



And that my friends, is that! An extra 42KB of data and processing that does not detract from the application start up. See it in action at [https://hubbubapp.com](https://hubbubapp.com) . You'll need to get one of your **Borrowers** online at the same time as you.
