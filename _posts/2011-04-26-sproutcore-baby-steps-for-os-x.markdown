---
author: tkeating
comments: true
date: 2011-04-26 15:21:00+00:00
layout: post
link: http://blog.sproutcore.com/sproutcore-baby-steps-for-os-x/
slug: sproutcore-baby-steps-for-os-x
title: SproutCore Baby Steps for OS X
wordpress_id: 5
post_format:
- Aside
tags:
- Tutorial
---

With the recent release of SproutCore 1.5, it seems like the perfect time for a "Getting Started With SproutCore" refresher. Whether you're tired of trying to get the benefits of client-side code execution into your server-side apps, or whether you're tired of trying to get the benefits of multiple platform support into your _client_-side apps, there's no better time to give SproutCore a try.




This post will walk you through the very first steps you need to get up and running. It assumes you're using OS X and have at least _some_ basic familiarity with the command line (come on, it's not so bad!).




## Installation




Installation has been getting simpler and simpler, and the team is working on making this _even_ simpler in the coming releases of SproutCore. Subscribe to the RSS feed to be notified of new posts on the blog; I'll be sure to post an update once things change.




So let's get into it; I'll work my way from the bottom layers on up.




### Step 1. Install the Xcode Developer Tools




You'll need the Xcode Developer Tools to compile some of the RubyGems that the build tools depend on. The appropriate version of Xcode for your current version of OS X should have been included in your install DVD.  If not, or if you've long-since lost the packaging from your machine, you can get a free copy of Xcode 3.2.6 by [signing up for an Apple Developer account](http://developer.apple.com/programs/register/). Alternatively, you can buy Xcode from the [Mac App Store](http://itunes.apple.com/us/app/xcode/id422352214?mt=12&ls=1#) for $4.99.




Follow the instructions for whichever install path you choose, and report back here when you're done.


<!-- more -->


### Step 2. Update RubyGems




To update RubyGems, you just need to run one quick command. Open the Terminal and type the following:



    
    <code>sudo gem update --system</code>




### Step 3. Install SproutCore




Then, in the Terminal, type this:



    
    <code>gem install sproutcore</code>




Congratulations! You are officially set up with SproutCore. 




You'll likely want to jump right into your first app:



    
    <code>sc-init HelloWorld
    cd hello_world
    sc-server</code>




Once the server starts, you can visit http://localhost:4020 in your browser to see your apps.  You'll also want to visit the new [SproutCore Guides](http://guides.sproutcore.com/), which have a ton of new information on getting started, with more being added every day.




So that's it for now. As I said, things are going to be getting simpler and easier over the next few weeks/months/releases, so check back for updates!




### Addendum: Performance Boost!




There's a noticeable performance benefit to upgrading the preinstalled version of Ruby (1.8.7 as of OS 10.6) to Ruby 1.9.2. The SproutCore Team recommends that you install a newer version of Ruby to take advantage of those performance improvements.




The easiest way to install a new version of Ruby is to use the Ruby Version Manager, RVM. There are a [few ways to install RVM](https://rvm.beginrescueend.com/rvm/install/), but the recommended method _if you have git installed_ is to open the Terminal and run the following command:



    
    <code>bash < <(curl -s https://rvm.beginrescueend.com/install/rvm)</code>




This will install the very latest version of RVM straight from the github repository. If you don't have git installed then run this command:



    
    <code>curl -s https://rvm.beginrescueend.com/install/rvm -o rvm-installer     
    chmod +x rvm-installer     
    ./rvm-install latest</code>




Afterwards, to have RVM properly loaded into your Terminal shell, add the following line to the _end_ of your ``~/.bash_profile`` file:



    
    <code>[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # This loads RVM into a shell session </code>




RVM will now load properly into new shells, but is not available in your current shell, so open a new shell and install Ruby 1.9.2:



    
    <code>rvm install ruby-1.9.2</code>




Then, to use Ruby 1.9.2 in a shell you only need to type the following:



    
    <code>rvm use 1.9.2</code>




If you want all new shells to use Ruby 1.9.2, type this:



    
    <code>rvm --default use 1.9.2</code>




Finally, if you run into any trouble installing RVM and Ruby, please refer to the [RVM documentation](https://rvm.beginrescueend.com/rvm/install/) for more help.




Like I said, this is a recommended performance boost. You'll be just fine with the current version of Ruby as well.




— Tyler Keating
