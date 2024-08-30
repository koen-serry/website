+++
title = 'How automotic proxy discovery works...'
date = 2005-01-31
publishdate = 2005-01-31
thumbnail = "/thumbs/maximalfocus.jpg"
+++

Always found it intriguing how browsers have this new feature called Auto-detect proxy settings for this network. Now I
just found how easy it actually is to implement.

The only thing you have to do is:

1. add an A record called wpad and let it point to a webserver running on port 80
1. On the root of that webserver you locate a file that contains actually the same thing as the well-known proxy.pac file.

That's it. Your network is configured!!