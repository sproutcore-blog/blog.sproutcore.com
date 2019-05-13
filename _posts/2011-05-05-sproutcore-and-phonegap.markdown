---
author: ccampbell
comments: true
date: 2011-05-05 12:26:57+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-and-phonegap/
slug: sproutcore-and-phonegap
title: SproutCore and PhoneGap
wordpress_id: 2
post_format:
- Aside
tags:
- PhoneGap
---

Making sure your apps work everywhere is an important part of any mobile strategy. The mobile web allows you to reach your users wherever they are, and users have grown to expect that you'll be there wherever they go.

Increasingly, users want to access applications through app stores; to reach your users, you have to be available to them as many ways as possible. PhoneGap allows you to put your web applications in a native wrapper and deliver them in the Apple App Store, Android Marketplace, and many other native app stores. It also integrates really well with SproutCore, making it the natural choice.


### Getting Started


PhoneGap provides both JavaScript and native code. First, let's deal with setting up the native side. For the purposes of this post, we'll assume you're setting up an iOS project. You can follow the [Getting Started](http://www.phonegap.com/start) docs on PhoneGap's website to get a running start.

Create your PhoneGap XCode project and save it right inside your SproutCore project's directory (the one created with you ran `sc-init`). Let's assume you've saved your PhoneGap project to '`iphone/'`.


### Integrating PhoneGap with SproutCore Projects


The JavaScript code that comes with PhoneGap allows you to communicate with the Objective-C code (in the case of iOS) running on the native side. The best way to include this JavaScript API in your SproutCore application is to create a framework and then require it in your Buildfile. In your projects directory, run the following commands:

    
    <code>mkdir -p frameworks/phonegap
    
    cp ~/Documents/PhoneGapLib/javascripts/phonegap-uncompressed.js frameworks/phonegap</code>


Then, when editing your application's Buildfile, require the PhoneGap framework you've just added:

    
    <code> config :all, :required => [:sproutcore, :phonegap] </code>


The next time you build your app, the JavaScript you've included in your framework will be built with your project. <!-- more -->


### Deploying


There's a slight catch to be aware of when you go through this process: SproutCore's build tools bundle your files assuming they're going to run in an environment that supports absolute URLs (such as a web server). Since this is not the case in a native app, there needs to be an intermediate step to ensure your application will run when its in the PhoneGap project and on the phone.

[There's a Gist](https://gist.github.com/891372) available to help with this. The script will build your application and replace instances of absolute URLs with relative ones, ensuring that your application will work on your target devices. It will also work for building and moving your app into multiple PhoneGap projects for different environments.

First, save that file to '`build_phonegap.rb'` in your project's directory. Once you've got the file locally, it will be easier if you prepare a quick script (or integrate it into your build environment) instead of running it by hand all the time. You can create a file called '`build_phone'` with the following code:

    
    <code>#!/usr/bin/env ruby
    
    system('ruby build_phonegap.rb -a your_app_name -o ./iphone/www');
    </code>


As you can see, this invokes the build script with the proper parameters. The '`build_phonegap.rb'` script will automatically run '`sc-build'` for you, as well as changing and moving the files into the specified output folder. The application name argument (`-a`) is the snake-cased version of your application (the same one as the folder name in `apps/`). From now on, when you want to build your application for use on the iPhone, you just need to run ``build_phone``.

**Note:** if you can't run ``./build_iphone``, you may need to make it executable. To do so, run ``chmod +x build_iphone`.`


### Run


You can now follow the normal PhoneGap build procedures to run your app on your phone, deploy your application to the app store, and become an app rockstar with SproutCore.

Believe it or not, it's that simple. SproutCore and PhoneGap combined make building an app-store-ready application a cinch. We'll post more in the future about building and optimizing app-store-ready apps, so keep an eye out!
