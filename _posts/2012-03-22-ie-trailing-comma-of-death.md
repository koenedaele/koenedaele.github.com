---
title: The IE trailing comma of death
layout: post
category : technology
tags : [internet explorer, javascript]
---
{% include JB/setup %}

It happened again. After an upgrade to our site, we got some complaints that it didn't work in Internet Explorer 6 or Internet Explorer 7 any more. We almost said: use a real browser. As the number of people visiting IE6 has been reduced to almost nothing, we could safely ignore that one. But some 5% of our users are still on IE7. Most of them part of government services that have a very restrictive browser policy (generally because they made the error of developing website for one specific version of IE instead of the standards).

The main problem was debugging it. I do almost everything on a linux machine. I do still have a windows laptop at work, but that one runs Windows 7 and Internet Explorer 9. So do most of my colleagues.

In the end, I fired up a Virtual Box instance on my Ubuntu laptop and installed an old version of Widows XP on it.

Of course the problem turned out to be dead simple to fix. **The Internet Explorer Trailing Comma of Death**

The following bit of javascript was to blame:

    djConfig = {
        parseOnLoad: true,
        baseUrl: '/js/c/1203151109/',
    };

The problem is that comma after the baseUrl property. Firefox and Chrome have no problem with it being there. Older versions of IE do. So all I had to do was remove that comma.

See [enterprisedojo.com](http://www.enterprisedojo.com/2010/12/19/beware-the-trailing-comma-of-death/) for some more info on this problem and some ways of detecting this sooner instead of later.
