---
author: gmoeck
comments: true
date: 2011-04-06 12:03:00+00:00
layout: post
link: http://blog.sproutcore.com/dispatches-from-the-edge-part-1-template-views/
slug: dispatches-from-the-edge-part-1-template-views
title: 'Dispatches from the Edge: Part 1, Template Views'
wordpress_id: 9
post_format:
- Aside
tags:
- Dispatch
- Video
---

More and more developers are adopting SproutCore every day, and the need for great documentation and tutorials just keeps growing. The Core Team is also making rapid progress on the _new_ parts of SproutCore—the so-called sexy Edge. We've got the fantastic new [SproutCore Guides](http://guides.sproutcore.com/) to tackle the mainstream parts of SproutCore, and now, I'm aiming to tackle the new and exciting Edge parts. 




Every other week I'll be posting what I'll call _Dispatches from the Edge_. Each Dispatch will highlight a feature from the most recent release of SproutCore, explain how to use it, and wax on about why it's so darn cool. Dispatches will _also_ be where the team posts announcements about upcoming SproutCore-related events. Online, offline, we've pretty much got it covered :)




I'd like for this to be as helpful and interesting as possible, so if there's something you want to know about, do let me know. Comment, tweet, email—I'll be listening!




* * *

There's been a lot going on in the world of template views lately, making it an optimal first topic for the Dispatch. One new feature stands out as being particularly exciting... so I'll start there :)




When you create a template for a view, that template is really specifying what the display should look like all the time. Since that's the case, when one of the properties of the view changes, it would be nice if the view would automatically redraw that section of its display to accomodate the changes in the data. The new template view does just that.




Let's look at an example:







[Dispatches from the Edge Part 1a](http://vimeo.com/22146781) from [SproutCore](http://vimeo.com/sproutcore) on [Vimeo](http://vimeo.com).


<!-- more -->


  
Templates, however, do more than merely specify a set of attributes that get displayed on the screen. They often contain helpers like _if_, _unless_, or _each_ to adequately describe how to display the state of the application. It would be nice if those helpers also could know automatically when they need to redraw themselves, so that developers need only specify once how the page should look, and then let the framework do the rest.




With the new template view, you can now use the normal Handlebars helpers ({{with}}, {{if}}, {{unless}}, and {{each}}), and if the properties they reference change, SproutCore will automatically update the DOM.




Let's look at another example:







[Dispatch from the Edge Part 1b](http://vimeo.com/22146745) from [SproutCore](http://vimeo.com/sproutcore) on [Vimeo](http://vimeo.com).




  
The key point is that when we can make our templates declarative, the framework can in large part keep track of keeping the view up to date without any boilerplate code.  
  
 




* * *

  
**Announcements:**




April's looking busy for SproutCore meetups across the country:







  * [New York City](http://www.meetup.com/Sproutcore-NYC/events/17144270/): Wednesday, 4/20


  * [San Francisco:](http://www.meetup.com/sproutcore/events/17193896/) Tuesday, 4/26


  * [Boston (co-hosted with jQuery)](http://www.meetup.com/SproutCore-Boston/events/17185888/) : Thursday, 4/28



Core Team Member Yehuda Katz will also be speaking at the 4/14 [Silicon Valley Ruby Meetup](http://www.meetup.com/silicon-valley-ruby/), as well as on Wednesday, 4/27 at [Philadelphia's Emerging Technologies for the Enterprise](http://phillyemergingtech.com/2011). 




Don't see something up here that you think should be? [Let us know!](mailto:community@sproutcore.com)


