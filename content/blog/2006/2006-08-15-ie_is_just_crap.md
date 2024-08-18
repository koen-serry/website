+++
title = 'IE is killing me'
date = 2006-08-15
publishdate = 2006-08-15
thumbnail = "/craft_header.jpg"
+++

As happy as I was that I was using AJAX in my latest webapp (http://www.proco.be) as disappointed I was that the
prototype library (Ajax.Update in particular) didn't seem to work on larger datasets in IE since its header has a
certain limit. As usual IE just swallows the error.

Since webwork is using dojo internally I was given a choice, but I found prototype easier to use, so now I was forced using dojo. 
OK modifying, debugging couple of hours later...  <b>system error -1072896748 in IE's usual javascript error box</b> WTF??

Googling a bit pointed me to some weird error in the MSXML parser that couldn't handle UTF-8 (mind the dash). 
OK fixed, another error in IE, what's next...

Well got an even nicer one.. Seems if you take an element and give it id="description" and try setting the innerHtml 
of it it won't work. Setting it to whatever magically fixes the stuff. Why is following the standards so hard?