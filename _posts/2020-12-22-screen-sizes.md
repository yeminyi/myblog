---
layout: post
title: Responsive breakpoints - screen sizes
categories: css 
tags: [css,responsive]
---
## Responsive breakpoints

Mobile First? (min vs max)
First thing to decide is in which direction you want your media queries to work.

By this I mean whether you want to set max-width or min-width breakpoints.

You can of course use a mixture of both, but here we’re all about making things more straightforward, so I would avoid ‘crossing the streams’ and stick to one strategy.



![sizes]({{site.baseurl}}/assets/img/2020-12-22-screen-sizes/screen-sizes.png)


### Max Width 
Everything from zero or the last, narrower breakpoint, up to ‘this width’
Used mostly in ‘Desktop First’ and ‘Retro Fitted Mobile’ builds.

@media (max-width: @screen-xs-max) { // < 768px (xsmall phone)

@media (max-width: @screen-sm-max) { // < 992px (small tablet)

@media (max-width: @screen-md-max) { // < 1200px (medium laptop)


### Min Width 
Everything above ‘this width’ to infinity, or until overridden by another, wider breakpoint.
Used mostly in modern ‘Mobile First’ builds.

@media (min-width: @screen-sm-min) // >= 768px (small tablet)

@media (min-width: @screen-md-min) // >= 992px (medium laptop)

@media (min-width: @screen-lg-min) // >= 1200px (large desktop)
