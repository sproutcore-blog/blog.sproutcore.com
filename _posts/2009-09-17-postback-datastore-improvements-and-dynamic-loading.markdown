---
author: admin
comments: true
date: 2009-09-17 05:00:00+00:00
layout: post
link: http://blog.sproutcore.com/postback-datastore-improvements-and-dynamic-loading/
slug: postback-datastore-improvements-and-dynamic-loading
title: 'Postback: DataStore Improvements and Dynamic Loading!'
wordpress_id: 103
post_format:
- Aside
---

I just pushed a big bunch of changes to the public repository tonight, including a month's worth of bug fixes and tweaks, along with a few major new changes.




I don't normally write a blog post about every change we push to the repository.  But this push includes a fairly major API change.  Since SproutCore 1.0 means we're making a commitment to our API, all changes we make need to be carefully planned and well documented.




**What Changed and Why**




So far the SproutCore 1.0 API has worked really well.  One spot that trips up everyone, however, is in the DataStore framework; in the interface between SC.Store.find()/findAll() and the fetch() method in the data source .  It was really each prior to this change to write the fetch() method in your app data source in such a way that it would break find()/findAll() entirely.  This is evil.




Here's how we fixed it:




  1. To find multiple records in the store, you must now always construct a Query object.  A Query object is how tell the store what type of records to return and any special conditions (using the [SproutCore Query Language](http://wiki.sproutcore.com/DataStore-SCQL)). 


  2. We got rid of findAll().  Now there is just SC.Store.find().  Pass a recordType/id pair to this method and it will return a single object.  Pass a Query object, and find() will return all records that match it.


  3. The return value of fetch() in your DataSource is no longer important.  Instead, you need to invoke a callback on the store telling the store when you are finished with a query.  This is the same way you handle records in a DataSource so it is actually more consistent.



Together these changes are fairly minor but they really clean up this part of the API.  The upshot is that if you update to the latest code, it will probably break your SproutCore 1.0 app until you make it work with this new API.




The good news is, this is the very last API change I know about for the SproutCore 1.0 framework.  All we have left to do now is to fix a few remaining bugs.




**And finally: Better Documentation!**




To help you along that process, I have nearly completed writing a brand new DataStore Programming Guide over on the wiki.  This guide describes the new DataStore APIs in some detail to help keep you moving.  There are a few bits in the DataStore section still missing; but I'll hopefully get that in tomorrow.




Checkout the [DataStore Programming Guide on the Wiki »](http://wiki.sproutcore.com/DataStore-Introduction)


<!-- more -->


**Other Improvements**




We did slip in some nice improvements and enhancements in this postback you will probably love.




  * SC.Record.toMany() and toOne() now fully support bi-direction relationships!  This means you can setup two properties as the inverse of the other.  When you modify one, it will automatically change the other one too.  Hurray for ORM!


  * The build tools now support Ruby 1.9.  Yay!  They also will use "Thin" if you have it installed, instead of Mongrel or Webrick.  This can make your build tools significantly faster at times.


  * The build tools and framework now also support an experimental form of dynamic framework loading.  Now instead of loading all of your app code up front, you can split your app into pieces and load some parts on-demand.  This can improve your initial load time.  In the future this will probably develop into full CommonJS SecurableModule support.



We've also added some nifty new sample apps, such as [Signup](http://demo.sproutcore.com/signup/), which demonstrates how to use Responders and statecharts to organize the overall flow of your code.




The end is in sight for SproutCore 1.0.  It's a hard drive to the finish line now.  If only my wrists hold out... :-)
