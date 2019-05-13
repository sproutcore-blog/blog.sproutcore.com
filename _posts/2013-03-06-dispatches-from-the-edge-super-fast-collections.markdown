---
author: tkeating
comments: false
date: 2013-03-06 23:45:48+00:00
layout: post
link: http://blog.sproutcore.com/dispatches-from-the-edge-super-fast-collections/
slug: dispatches-from-the-edge-super-fast-collections
title: 'Dispatches From the Edge: Super Fast Collections'
wordpress_id: 2104
tags:
- Dispatch
- Performance
---

One of the most advanced changes coming in 1.10 is the formalization of a major enhancement to SproutCore's collection views.  Some of you may have heard of, used or tried to use the SC.CollectionFastPath mixin which gives SproutCore's collection views, namely SC.ListView and SC.GridView, a massive performance boost.  The performance boost comes from pooling the item view objects, pooling item view layers (i.e. elements) and re-positioning layers using layout styles without modifying the DOM tree.  By re-using objects and elements, we can increase the speed that our collections can update, making gigantic lists perform like butter, even on mobile.

However, using SC.CollectionFastPath was unwieldy and difficult to get working correctly.  Turning it on was not enough, you also had to provide a couple properties on your item view class that were totally undocumented.   Due to the fact that SC.CollectionView is already optimized to create item view objects and layers only for the visible portion of the collection, it could be hard to even be sure that the fast path code was active or not.  This is all changing in 1.10.

We believe that every SproutCore view should be as fast as possible out-of-the-box on every platform and so we're making these improvements a part of SC.CollectionView directly.  This means that by default, SC.ListView and SC.GridView will be fully optimized without any further configuration.  That said, when creating custom item views, you should properly support render **and update**.  Since view performance is so important, you should already know how to do this and if you need a good example, check out the custom item views in the new demo in the[ SproutCore Showcase](http://showcase.sproutcore.com/#demos/Big%20Data).  This demo was created to debug this new technology as well as to demonstrate working with gigantic lists.

For now, the feature is still being tested and fine-tuned and any additional real-world feedback is appreciated.  So please check it out on the SproutCore master branch and bring any issues forward so that they can be addressed before release.

Thanks!



For discussion, please use sproutcore@googlegroups.com or #sproutcore on IRC.

Note:  Whereas, before you needed to set properties to turn this on, you have to set properties to turn it off right now.  If for whatever reason, you don't want to pool elements, you can set **isLayerReusable** to false on your custom item view and if you don't want to pool views, you can set **isReusable** to false as well.
