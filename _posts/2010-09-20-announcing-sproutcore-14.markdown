---
author: admin
comments: true
date: 2010-09-20 13:45:00+00:00
layout: post
link: http://blog.sproutcore.com/announcing-sproutcore-14/
slug: announcing-sproutcore-14
title: Announcing SproutCore 1.4!
wordpress_id: 34
post_format:
- Aside
tags:
- Release
---




Those of you who have been following SproutCore may have noticed the appearance of a series of Release Candidate gems for version 1.4. Today, we'd like to offically announce the release of version 1.4! Why the jump from 1.0? We're going on a year since the first release of 1.0 and almost exactly eight months since 1.0.1046 and a whole lot has happened since then. This release has over 1000 new commits and around 20 new contributors.




Thankfully, you won't have to deal with long release cycles in the future. SproutCore 1.5 is already coming along nicely. We hope to release it before the end of the year. We'll continue to maintain SproutCore 1.4 as we move forward with bugfixes. If you're interested, you can follow that work on the 1-4-stable branch on [Github](http://github.com/sproutcore/sproutcore). Apple has done quite a bit of work that they plan to contribute back to the project soon. After that, we will merge the work that we've done so far on SproutCore 1.5 (code name Quilmes) with the parallel work we've done on SproutCore 1.4.




From here on out, we'll be releasing pre-release gems regularly as well as patch releases for bug fixes. You can get the most recent SproutCore pre-release by running `gem install sproutcore --pre` and the most recent stable release by running `gem install sproutcore`. No more eight month waits!




Along with the release of 1.4 we're also moving the SproutCore repos over to [github.com/sproutcore](http://github.com/sproutcore). To update your current repositories:



    
    <code>git remote rm origin
    git remote add origin git://github.com/sproutcore/sproutcore.git
    </code>




We're also starting to make plans for SproutCore 2.0 which will bring some awesome new improvements. As we design and develop 2.0, we'll keep you up-to-date with the changes we are planning and give you previews of the new features. One of the most exciting changes in the releases ahead is the ability to package up and share SproutCore components (even with dependencies!) as easily as the best facilities in other languages. Stay tuned for more details!


<!-- more -->


Along with these new releases also come some major SproutCore personnel changes. As you may have heard, Charles Jolley has left Apple and started a new company around SproutCore called Strobe Inc. Long time SproutCore contributors Peter Wagenet and Colin Campbell have both joined Charles at Strobe. As you may have already heard, Yehuda Katz and Carl Lerche of Rails 3 fame have also come on board as Strobe employees and will be major contributors going forward!




## 




## What's New




By now you're probably wondering, "Well, what is new in 1.4?" As I said earlier we had over 1,000 commits so this is just a brief overview.




**Touch Support**




We now have extensive support for touch events. All SproutCore controls now support touch events natively. This means that with minimal effort, you can get your SproutCore apps running on the iPhone, iPad, and other mobile devices! More touch controls are coming in 1.5 but the foundation is here now. For more info read the original [blog post](http://blog.sproutcore.com/post/531215199/introducing-sproutcore-touch).




**Faster Build Tools**




One of the first contributions by Yehuda has been to speed up Abbot. Importantly, reloading your application after making a change will take one or two seconds, rather than the 10 to 20 seconds it took in SproutCore 1.0. That makes a huge difference to your ability to make small changes and see them reflected immediately in the browser.




There are a few changes you should be aware of:




  * The SproutCore 1.4 build tools expect your files to be saved in UTF-8. This is almost always true, but you may have some files saved in a different encoding. The build tools will give you an exception if this happens, and you will need to resave the files in UTF-8. If you use Textmate, you can use the Save As dialog to [change the encoding](http://img.skitch.com/20100918-b9qr78ah1wkm2ccdpa61p7gm2j.png).


  * You may be used to using the build tools directly from Github. In the future, you'll want to use the prerelease gems (using gem install sproutcore --pre), and only use the tools from Github if you are actively hacking on the tools themselves.


  * If you want to use a different version of SproutCore than those that ship with the build tools, copy or symlink it to the frameworks directory in your app.



**Bug Fixes and Stabilizations**




Many of the commits in 1.4 also dealt with bug fixes and stabilization improvements. SproutCore should overall provide a better, more solid experience. We've also put in some additional browser compatibility improvements so you should have a better cross-browser experience as well.




**Universal Error Handling**




Previously when fatal errors occured, your app would just stop working, often without warning. We've now introduced a new error handler called SC.ExceptionHandler. The default error handler is very basic so you may want to provide your own version. Just overwrite SC.ExceptionHandler with an object that has a function called handleException. This function will be called with the exception as the single argument. Alternatively, you can overwrite only the handleException function as such:



    
    <code>SC.ExceptionHandler.handleException = function(exception) {
      // default
      if (this.isShowingErrorDialog) return;
      this._displayErrorDialog(exception);
    
      // you can use any error handling code here
    }
    </code>




**Animation Support**




Though this feature was actually present in 1.0.1046, it was never officially announced and has largely flown under the radar. SC.Animatable supports both traditional timer-based animations and hardware accelerated animations using the same API. This means that you can build animated SproutCore applications that look gorgeous on iPhones and modern browsers with hardware acceleration support. For more information see the [README](http://github.com/sproutcore/sproutcore/blob/master/frameworks/animation/README.md). Oh yeah, we'll also be bringing even more animation support in 1.5.




## Experimental Features




In addition to these production ready features we also have some new experimental features as well thanks to the great work of the SproutCore community.




**Greenhouse**




A full-fledged interface builder for SproutCore written in SproutCore! While not quite ready for production use, we're continuing to work on this and are working hard to bring you a way to build your web apps in a web browser. We think this is the future of SproutCore view development, so keep an eye out for a lot more in the coming months. Find out more in the announcement [blog post](http://blog.sproutcore.com/post/535950751/introducing-greenhouse).




**TableView**




A long asked for feature, a preliminary version of SC.TableView is now in 1.4. While it has some issues, it does work and if you're feeling adventurous you may want to try using it in your apps. If you make improvements please contribute them back to SproutCore. Other people like you might even pick up the ball and run with it. See the[ blog post](http://blog.sproutcore.com/post/395119002/yay-sc-tableview-is-coming-to-sproutcore-the).




**CollectionView Fast Path**




Make your CollectionViews much faster—and make them scroll with much better performance on tocuh devices—with SC.CollectionViewFastPath. This is somewhat experimental and is not yet thoroughly documented, but should be mostly ready for production use. Consider it beta level.




## Community Contributions




Not only has interesting stuff being going on in core, but a lot of interesting community projects have been going on as well.




**SCXIB**




In addition to Greenhouse there is now an alternative way to develop your app interface. SCXIB will load your XCode Interface Builder .xib files and turn them into SC views on the fly while you edit the interface in Interface Builder and reload your app. It even supports custom SproutCore classes! So you now have three options: Greenhouse, SCXIB, or the way you've already been doing it.  
[Github](http://github.com/robiculous/scxib)




**SproutCore UDS**




A universal data source for SproutCore that includes support for backends like Rails and CouchDB. Also supports common public APIs like Twitter, with planned support for Amazon, Facebook and Github. And if that wasn't enough, it also supports local storage! Expect to see a lot more work on drop-in, flexible data stores for SproutCore 1.5 and 2.0. [Github](http://github.com/etgryphon/sproutcore-uds)




**Sai**




A SproutCore vector graphics library that supports all major browsers.  
[Github](http://github.com/etgryphon/sai)




**Ki**




Statecharts for SproutCore. That pretty much says it all :)  
[Github](http://github.com/FrozenCanuck/Ki)




## Get Involved




**Code Contributions and Bug Fixes**




As always, SproutCore relies on your contributions. If you find a bug or want a new feature, consider helping us out with it.




All you have to do is fork the repo on Github and send us a pull request. We really love Github's new pull request feature, and it lets us process your patches quickly and efficiently. Just please do us a favor and send a separate pull request for each major issue that you're addressing. Learn more about the new pull requests in the announcement [blog post](http://github.com/blog/712-pull-requests-2-0)




If you run into an issue but can't figure out how to fix it, please submit a ticket at either [http://github.com/sproutcore/sproutcore/issues](http://github.com/sproutcore/sproutcore/issues) for the framework or at [http://github.com/sproutcore/abbot/issues](http://github.com/sproutcore/abbot/issues) for the build tools. We're keeping a close eye on the issues and closed quite a few during the release candidate.





**Documentation**




SproutCore's Achilles' heel has always been its documentation. No longer! We've started a major push to improve the documentation, and have been doing some interesting experiments with documentation (you might have noticed that the Touch documentation is in a beautiful new documentation engine codenamed Hedwig). If you're interested in being a part of this let us know and get in on the discussion in [sproutcore-dev@googlegroups.com](mailto:sproutcore-dev@googlegroups.com).




## Appendix




**New Committers since 1.0.1046**




  * Alex Johnson


  * Andrew Dupont


  * Brian Moore


  * Brian Noguchi


  * Bruz Marzolf


  * Eric Kidd


  * Joshua Holt


  * Julian Viereck


  * Luke Burton


  * Matthew Grantham


  * Matthias Loitsch


  * Michal Kurgan


  * Mitchell Rivera


  * Nathan Baxter


  * Patrick Walton


  * Richard Klancer


  * Robert Buchholz


  * Ryan Nielsen


  * Yehuda Katz



(Some may be missing from this list. Sorry!)




**1.4 ChangeLog**




Check out the massive (and incomplete) [list](http://github.com/sproutcore/sproutcore/blob/master/CHANGELOG.md#commit).




* * *

**Post by Peter Wagenet with help from Yehuda Katz and Devin Torres**
