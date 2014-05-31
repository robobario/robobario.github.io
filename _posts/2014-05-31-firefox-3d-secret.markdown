---
layout: post
title:  "Drawing Heiroglyphs in Firefox 3d View"
date:   2014-05-31 19:30:35
categories: firefox
---

When Firefox 3d view was released it got a typical reaction at the office. We had a look at the strange towers created by our css hacks and then never used it again. My teammate thought it would be funny to hide pictures that are only visible to the 3d viewer. So what else am I going to do on a long weekend?

I was unsure if you could create gaps between bricks but it wasn't a problem. To do this you create a stack of 0x0 divs with a sized div at the top.

In the end it looks like this
![Firefox hieroglyphs](/assets/ff3d.png)

And I've chucked the code here:

[Firefox Hieroglyph Js](https://gist.github.com/robobario/bbc08647f347b3d9ac8b)

