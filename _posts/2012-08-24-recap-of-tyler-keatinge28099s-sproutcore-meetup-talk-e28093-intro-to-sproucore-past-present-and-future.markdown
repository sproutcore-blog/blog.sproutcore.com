---
author: timw@appnovation.com
comments: false
date: 2012-08-24 16:57:01+00:00
layout: post
link: http://blog.sproutcore.com/recap-of-tyler-keating%e2%80%99s-sproutcore-meetup-talk-%e2%80%93-intro-to-sproucore-past-present-and-future/
slug: recap-of-tyler-keating%e2%80%99s-sproutcore-meetup-talk-%e2%80%93-intro-to-sproucore-past-present-and-future
title: Recap of Tyler Keating’s SproutCore Meetup Talk – Intro To SproutCore, Past,
  Present and Future.
wordpress_id: 2043
---

[Link to view recorded version of the meetup on Vimeo](https://vimeo.com/47726696)

**Speaker:** [Tyler Keating](http://blog.sproutcore.com/author/tkeating/) – was working as a contractor at Strobe, which got bought by Facebook. He inherited the framework and is currently the Administer of SproutCore. Tyler holds the keys to all the SproutCore assets. Today, Tyler has taken on a leadership role with SproutCore as its Project Lead.

**Background on libraries and frameworks:** Currently, there are lots of JavaScript libraries and frameworks out there right now. A library can be considered a bunch of code that can be dropped in at any point in the development process and can work with what you have already. It can work with your processes and format structure. A good example of a library would be JQuery. Frameworks, on the other hand, expect a developer to follow its guidelines, process and file structure (structure of its code). Under this definition, SproutCore is definitely defined as a framework.

With a framework like SproutCore, a developer would want to be starting from scratch building a brand new application. SproutCore comes with directories and file structures and expects those who use it for development to put things in certain places, use its bindings, use its build tools, etc.

SproutCore on the “Spectrum” of JavaScript libraries and frameworks, on the far left, you would have a library like JQuery and on the far right, a framework like SproutCore. Very few JavaScript frameworks can be found on the far right, most them fall somewhere in the middle between being a library and a framework. Usually, these middle of the road type frameworks want to provide the M or C of MVC. Many of these frameworks found in the middle and most libraries out there do not have the tight integrations found in frameworks like SproutCore. They also just provide a bit and not a “full picture” so to speak. What you see are that libraries start to group together to more tightly integrate and slowly become more of a full picture.  This happens all the time, but with SproutCore that was the end goal from the start, so the integration is more advanced.

On another spectrum, a spectrum of web applications, on the far left you would have an application like Wikipedia which is basically a page of documents and links while on the far right you would have an application like iCloud, that has animations, very ambitious user experience, loads of data, multiple browsers, etc.  When developers want to design an application, provide localization in multiple languages, SproutCore has this directly built in as well as things like infinite scrolling lists. One could try coupling a bunch of libraries together, but this would become a very laborious effort from the standpoint that you would have to write a bunch of code to do it.

**SproutCore:** When thinking of using SproutCore to build an app you would want to be starting from scratch. The goal of the app that you are building with Sproutcore should be native-like performance and native-like feel. You want to be able to take advantage of the multiple pieces and build tools that SproutCore offers developers. With SproutCore you can:



	
  * Combine all your JavaScript

	
  * Compress your files in a single file

	
  * Use auto-spriting for images

	
  * Properly cache so the app can be installed one time and live for a really long time

	
  * Take advantage of localization that has been built directly in the framework


SproutCore provides:

	
  * build tools

	
  * auto spriting

	
  * file structure

	
  * localization strategy

	
  * highly integrated collection views

	
  * MVC components

	
  * statecharts

	
  * client-side data store that can be queried


SproutCore gives you a lot more pieces than other frameworks or libraries while at the same time tons more  in terms of performance.

**Where SproutCore is going?** Today the framework is a very full suite with lots of features, components and tools to use. There is no plan to “dumb down” the framework and try to compete with some of the newer frameworks on the market. SproutCore has been around longer with many engineering hours already spent building it out to be better and beyond what is coming out today. The Core Team of SproutCore wants to leverage what they have and continue to build on it. The Core Team wants developers to use SproutCore for building apps that are large scale, long lived and will continue to grow.  Another advantage that SproutCore has is that it has been thoroughly tested and carries lots of support across browsers.

**Apple and others involvement:**  Apple created SproutCore 1.0 and has been the largest contributor thus far. You can tell Apple spends many many hours on the code making it cross browser compatible, localizable.  I think iCloud is available in over 100 different languages. Apple helps make the framework very professional and has been a really great resource from a testing standpoint. Facebook, as far as anyone can tell, does not have any interest in SproutCore. Eloqua is also one of the major contributors to SproutCore, in particular the excellent client side data store components.

**What has happened to SproutCore since the end of Strobe?** SproutCore was completely worked on by Apple and its creator, Charles Jolley. Charles was very adamant that it be open source and have a community of support behind it. When SproutCore was under Apple, very few people who were contributing back to the framework. Charles then left Apple and created Strobe which spent a lot of energy building and marketing SproutCore. Strobe was unable to keep going and was eventually purchased by Facebook. As far as anyone can tell, Facebook is just interested in the people behind the framework, not SproutCore itself. So SproutCore was left untended for a couple months. I, who had been working as a contractor at Strobe, then spent the time to keep SproutCore going by collecting the assets, passwords, etc.  Appnovation also stepped in to provide community support. Today, engineering work continues and the framework continues to be built out. Currently in 1.8, with 1.9 out very soon and 2.0 already having some work done on it. With Strobe gone, the marketing and promotion side of things sputtered at which point companies like Appnovation have stepped up and filled that gap.

**SproutCore 1.9:**  1.9 is essentially just about done. In the past, SproutCore has had versioning problems, so it was hard to know when to upgrade an application built with it. SproutCore 1.9 is backwards compatible with new features releases with a number of bug fixes. It is not meant to introduce any new problems in existing apps. SproutCore 1.9 has a number of styling fixes to the ACE theme so that is works in a lot more scenarios properly, it also provides the introduction of SC.Color which is object for the manipulation of colors and adds XHR2 events.

**SproutCore 2.0:** The next major release will be SproutCore 2.0 which means its not going to be completely backwards compatible. Strobe’s 2.0 that was in the works is not related to SproutCore. The project got spun off and became EmberJS.  SproutCore 2.0 is going to move to node based build tools because right now the build tools are written in Ruby. This makes it harder for the Core Team to work on the build tools because they have to know Ruby. Additionally, anyone using SproutCore has to have Ruby installed to use the framework when building an application. Thus the move to Node is happening for several reasons most notably because the Node installers are better maintained and Node makes it easier for people to contribute back to the code since they are based in JavaScript as well. The release of SproutCore 2.0 is going to bring about the clean up of the numerous of sub-frameworks (libraries), because several were not maintained well. SproutCore 2.0 is also going to place a major focus on expanding the desktop framework because right now there are number of tablet and phone specific views to be added and we want to add more layout helpers. We are expecting to re-label the desktop framework a UI framework and raise it to higher level standard.  The Core team wants to make it easier and faster and with 2.0, people will be made more aware of all the features and tools that are out there on the 2.0 release through an emphasis on better documentation, guides and tutorials that will be made available online.

**To summarize:** SproutCore will continue to grow and get easier to use. We also expect it to have a lot less of a learning curve for developers wanting to create really fast and robust applications.

[Link to view recorded version of the meetup on Vimeo](https://vimeo.com/47726696)
