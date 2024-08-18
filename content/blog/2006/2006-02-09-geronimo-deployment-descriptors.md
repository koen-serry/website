+++
title = 'Re: Usability problems in JSF'
date = 2006-02-09
publishdate = 2006-02-09
thumbnail = "/thumbs/maximalfocus.jpg"
+++

I'd already checked out Geronimo before when it was still in Milestone stage, but since it got released I
finally got myself to actually deploy a complete earfile in it (so including an EJB module (Session,CMP and
messagedriven beans). Well I can say it's not as easy as it looks. Ok, they have a hot-deployment directory
and a nice "console" web interface, but that's where you can stop the comparison.

What I **don't** like at all is the excess of deployment descriptors. Just when everybody agrees that there
are too much DD around, just to deploy a simple war file in geronimo you need something called a 'deployment plan'.
This is ok if you want something special for a particular kind of configuration.
But what if you'd settle with the defaults...even SUN won't make that mistake twice.
