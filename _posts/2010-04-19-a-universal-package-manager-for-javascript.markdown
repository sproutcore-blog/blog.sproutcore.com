---
author: admin
comments: true
date: 2010-04-19 18:11:29+00:00
layout: post
link: http://blog.sproutcore.com/a-universal-package-manager-for-javascript/
slug: a-universal-package-manager-for-javascript
title: A Universal Package Manager for JavaScript
wordpress_id: 49
post_format:
- Aside
---

Thought of as a “toy language” for too long, JavaScript is coming into its own.  Today JavaScript is used in major duty applications in both the client and server environments.




The problem is, compared to our power-scripting brethren, our tooling support has never caught up.




Running small JavaScripts in the browser is reasonably easy today, but anything beyond that goes downhill fast.  A lot of basic things that other scripting environments take for granted simply do not exist for us.




**Don’t Get Me Started**




Take for example, packages.  Both Ruby and Python make it insanely easy to create a library and share it with other people.  For most Rubyists or Pythonistas, building a new product or feature usually begins with a search of their package system for a library that gets them close.  Once found, one command will install the library to make it ready to use.




JavaScript?  No such luck.




First, search Github.  If not found there, search Google.  Should you find a library, then you need to figure out how to integrate it into your own JS system.  Sometimes it is just a script you can drop in.  If it is bigger than that, you may need to get a build tool (which is probably written in Ruby or Python anyway) and use that to generate the file.




Once you have the script, of course, tracking updates is just as hard.  Usually it involves visiting a website periodically just to look for updates then going through the integration process all over again.




Even just running a JavaScript from the command-line is a total nightmare these days.  For most languages, it’s as simple as:



    
    <code>#!/usr/bin/env ruby
    </code>




And you’re off to the races.  The full power of the standard Ruby or Python libraries are at your disposal.  If you don’t like those libraries, no problem!  A quick search and install from the package manager and you’ll have something new in no time.


<!-- more -->


Meanwhile in JavaScript land…first you need to pick a JS runtime.  Usually you’ll end up repurposing a JavaScript server like narwhal or node.js. Each has a totally different API, by the way.  Whichever runtime you choose will stick you for the life of the project without major transition pains.




What a mess.




**Where Giants Fall**




Now, to be fair, some really smart folks have been working on some projects that at least partially solve this problem for some time now.




The CommonJS standard has a great module pattern that is a key building block to solving these problems.  It also has a concept of packages that is going in the right direction but each project seems to interpret it so differently we can't rely on it globally.




There are, in fact, several implementations of CommonJS available, including node.js and Narwhal among many others.  They even have some package managers designed for their respective platforms.




Easily sharing code isn't a primary purpose of this project, however.  They come with a bunch of added (different) APIs and subtle incompatibilities as well.  When these things break your code, no one is generally in a hurry to fix it.




Which is totally fine, by the way.  That’s how open source works.  You scratch your personal itch.  If someone wants to do something with your project that isn’t part of your personal charter, you don’t do it.




**A Call To Arms**




The point is that for JavaScript to have a universal set of tools for sharing and executing code, it needs a project dedicated to that purpose.  Specifically it needs to have the following goals:




  1. 


Provide a CommonJS runtime environment that works in both the browser and  multiple JS “runtimes”.





  2. 


Be as flexible as necessary to help you adapt older JavaScript code to  work with CommonJS while maintaining compatibility.





  3. 


Make it insanely easy to create, share, install, update, and fork  JavaScript libraries for both the server and the client.





  4. 


Keep the API as focused on sharing code as possible.  All other APIs (file  io, browsers, etc.) should be exposed as packages that can be dynamically  swapped out.






Basically, we want a tool that is focused on making it easy to adapt and share new and existing code to run in browser, server, and from the command line. It should not take a position on other APIs (such as sync vs async).  It  should be small, focused, and simple as possible.  Ideally it should run on any JavaScript runtime, not just one or the other.




**Seed.js**




From my perspective, this project does not yet exist.  I think it is important though, so over the last few months I built one.  It’s called seed.js.




Seed.js is a flexible package manager for CommonJS modules.  (A CommonJS module is a single JavaScript file, a package is a group of one or more related modules that you install together.)  It implements three things:




  1. 


A package-aware CommonJS module runtime that works in both the web browser and most “server-side” runtimes (such as node.js or narwhal).  This allows you to write your CommonJS modules to a single standard.





  2. 


A command-line tool (called “seed”) that can install, update, remove, and fork packages.





  3. 


A JavaScript-runner that will execute JavaScript using a chosen runtime (e.g. narwhal, node.js), automatically loading seed on top of it.






Virtually every aspect of both the CommonJS runtime (called “tiki”) and the seed command line tool itself is configurable via simple API’s.  The idea is to give you lots of ways to enhance the Seed environment itself when adapting existing code so you can make the code run without having to break backwards compatibility.




The point is that seed’s purpose is to be focused and flexible - to adapt to the needs of the community so that we can have one universal packaging  system for use across the board.




**Current Status**




Right now, seed is usable but not finished. We showed seed.js for the first time publicly yesterday at jsconf 2010.  It is  available now for you to play with at seedjs.org.  To get things rolling we have pre-loaded the seed server with a dozen or so packages.




Currently, seed runs on node.js and stores packages on a JavaScript-based server hosted at seedjs.org. When forking packages, seed uses `git`. But these were just our starting points. All our platform dependencies are kept in a single place so porting from node.js to another runtime should be straightforward. You can target different server backends just by writing a plugin. Ditto for adding support for new SCMs.




As far a projects go - both the Mozilla Bespin team and SproutCore have been using the Seed CommonJS runtime (aka “tiki”) for several months now and we’re really happy with it.  In fact, both SproutCore’s ‘runtime’ and ‘datastore’ frameworks have been converted to CommonJS and will soon be available as  packages in the seed repository.





...





If you would like JavaScript to become as easy to use as Ruby or Python,  please go give seed a try today.  Install some packages, write some code.  Create a seed of your own and publish it. Then, join the mailing list or join us on the IRC channel at #seed.js on freenode.net and give us your feedback.





Right now seed is new so just about anything can change.  The goal is to end  up with a universal set of tools that makes JavaScript a better platform to  work with - in the browser, in the server, and direct from the command line. If you want this future too, download seed and let me know what you think.
