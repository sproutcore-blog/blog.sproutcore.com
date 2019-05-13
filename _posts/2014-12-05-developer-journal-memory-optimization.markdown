---
author: tkeating
comments: false
date: 2014-12-05 04:10:37+00:00
layout: post
link: http://blog.sproutcore.com/developer-journal-memory-optimization/
slug: developer-journal-memory-optimization
title: 'Developer Journal: Memory Optimization'
wordpress_id: 2352
---

The next release candidate for 1.11.0 will be out very shortly, but I thought it best to post a brief update on the past week's work as this week saw a concentrated effort on core optimization.

First we took another look at the use of `arguments` lists throughout the framework and found several more occurrences of it being accessed in an inefficient manner. Depending on the browser, accessing `arguments` in such a way that causes it to be allocated can be up to 80% slower and so it's really good to have these all fixed.

The other piece of optimization work undertaken has been much more difficult. We've been looking into high frequency event handling, such as during touch dragging or mouse moving, with an eye towards managing memory better. Since SproutCore already does as much as possible to avoid touching the DOM, the largest issue that affects the "fluidity" of the user interface is JavaScript garbage collection. If the heap is filling up rapidly with unreferenced objects, the JavaScript engine will be forced to collect them more frequently and the act of collecting them will take longer. Since we have no control over when garbage collection occurs, for example we can't prevent it from happening in the middle of a transition, the best we can do is to reduce its impact. So essentially, our goal is to not allocate any additional memory during high frequency events and our primary means to that goal is through shared Object re-use.

As I mentioned, this has been very difficult, but we've been steadily identifying and replacing Objects (hashes) and Arrays with single shared versions wherever possible. This includes some key high touch areas in SC.View's layout code and SC.Event's architecture. In fact, a major refactor of SC.Event was completed in order to re-use a single shared normalized event instance per event type. This means that whereas previously each event (e.g. `touchmove`) would allocate a new normalized SC.Event each time, it now re-uses just the one. The affect of all of this work is a slightly flatter memory profile with fewer and smaller saw-tooth garbage collection drops in it. It's not perfect yet and it's likely impossible to not allocate a bit of memory on each event, but some exciting progress is being made.

Lastly, a bit more internal debugging code was moved into debug-mode only. This means that the code will not be included in production builds, thus reducing the overall size of the production JavaScript by a tiny bit. A minor optimization, but one none-the-less.
