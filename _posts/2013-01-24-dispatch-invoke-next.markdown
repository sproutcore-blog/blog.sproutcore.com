---
author: tkeating
comments: false
date: 2013-01-24 22:21:34+00:00
layout: post
link: http://blog.sproutcore.com/dispatch-invoke-next/
slug: dispatch-invoke-next
title: 'Dispatches From the Edge: Invoking "Next" '
wordpress_id: 2079
tags:
- Dispatch
- Performance
- Run Loop
- sproutcore
---

As the 1.10 release nears completion, I thought I'd better start writing about some of the many improvements now, lest the final release blog post would take me two days to write.  A lot of the changes, including today's topic, were the result of working on big feature additions and discovering that more support was needed closer to the core.  Which brings me to the topic of this post:  SC.RunLoop.prototype.invokeNext.<!-- more -->

On the surface, I thought invokeNext worked as is.  According to the documentation, a function passed into invokeNext would be run at the beginning of the _next_ run of the run loop.  This differs slightly from using invokeLast, which would run the function at the end of the _current_ run of the run loop.  This slight difference between invokeLast and invokeNext can be incredibly important though.  By using invokeNext, the current execution block can complete, giving the browser a chance to process queued events and timers and to repaint and reflow.  This break in execution is what makes invokeNext the best way to defer expensive DOM operations or in my case, the best way to ensure that an element's style is up-to-date before modifying it (more on this in a later post).

There was just one little problem though and that was that nothing actually guaranteed that another run of the run loop would occur.  If no event arrived or timer fired, the invokeNext functions would not get called.  And when another run did occur it might be 10 milliseconds or 10 seconds after the previous run completed.  And so after some thought, I decided that invokeNext should do just that, run immediately _next_ to the current run of the run loop.


<blockquote>Just a note to those that may have tried to get the same effect using invokeLater with a small time interval like 1ms.  A word of caution, you should **_only_****__** use invokeLater if you want something to occur later and anything less than 100ms is not really "later".  With such a small interval, the invokeLater timer will likely expire before the current run of the run loop even completes meaning that the functions passed to invokeLater will actually get wrapped up within the _current_ execution block.  Attempting to guess an interval long enough for the current execution to complete, but not too long to annoy the user, say an interval of 50 or 100ms, is a fool's game.</blockquote>


What you'll find on master is that using invokeNext now allows the current run of the run loop (i.e.  JavaScript execution) to complete _before immediately_ starting _one additional run_.  If another run of the run loop was already scheduled to occur at the same time via an expiring SC.Timer, still only one more run would occur.  So no worries there.

So apologies for the low-level nature of this update, I promise that the next ones will be more interesting.  For what it's worth, now that invokeNext fills the hole between invokeLast and invokeLater properly, I'm extremely excited about what else I can do with it.

Cheers!



For discussion, please use sproutcore@googlegroups.com or #sproutcore on IRC.
