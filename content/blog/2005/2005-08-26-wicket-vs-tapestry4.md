+++
title = 'Wicket vs. Tapestry4'
date = 2005-08-26
publishdate = 2005-08-26
thumbnail = "/thumbs/maximalfocus.jpg"
+++

Last couple of days I've been tossed between Tapestry 4b3 and Wicket 1.1b3. Both of which integration with Spring is
quite problematic.

Things I like about Tapestry(4):

* Full control over pages/components
* Once Spring is integrated, full IOC is possible.
* Nice components available (eg. Tacos)

Things I don't like about Tapestry:

* Quite a lot of dependencies (Here less is beter)
* Hivemind.. (way to beta to do some actual work). Try integrating it with hibernate for example..
* Directory structure. HTML pages float around in the classpath without the possibility to have them

But comparing them with Wicket...

Good things:

* Strongly typed
* Real components (class+html) possible (just drag a jar in the lib folder)
* Good I18n possibilities
* Good templating possibilities (both HTML and class)
* very few dependencies
* Spring can be integrated by encapsulating it in the Application class

Things I don't like about Wicket

* Everything needs to be defined in java, no pull possible
* Getting the HTML right is hell, tags aren't replaced they are filled
* Components require the right tags
* No real IOC
