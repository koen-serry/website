+++
title = '.Net collections and the need for speed...'
date = 2006-03-23
publishdate = 2006-03-23
thumbnail = "/thumbs/maximalfocus.jpg"
+++

A few comments from 'The Other Side' I've been reading your blog since I'm doing
occasionally stuff in .net, even though java is where my heart is. This entry gave me the creeps so I couldn't resist
commenting on this blog entry of <a href="http://community.bartdesmet.net/blogs/bart/archive/2006/03/22/3831.aspx">Bart Desmet</a>.

If you're using JDK5 (and it seems you did) you may have noticed that new ArrayList().add(1)
actually works. So boxing and unboxing has made it into Java too (Although I'm not sure this is a good thing).

Second the collections framework in java is imho far better than .net, first of all there is no common interface for (
non-)generic collections in .Net. So System.Collection.Arraylist doesn't implement System.Collection.Collection or
whatever, like they do in java. This would actually allow components to be written that take collections as an
interface, regardless of how they're implemented. Or to have open source alternatives, that could turn out to be
faster/lighter.

On the backwards compatibility, while it's true SUN could have opted for putting them in a separate
package, they didn't. And quite frankly iIt doesn't even bother me that the compiler warns me about it, since I can
either disable them or use generics. What this has to do with versioning hell is a big question mark for me. Java hasn't
suffered from versioning hell like .net does. We do however have our own issues like ClassNotFoundExceptions,
ClassLoaders and stuff. 

Although things have improved since the 'COM' days, I don't know about something like
class loaders in .net that allows usage of separate versions of the same package in the same program. And then we didn't
discuss about the backwards compatibility between .Net2.0 and 1.(0|1) which is if you ask me questionable.

As far as startup time is concerned, well the statement that .net is 2,2 times faster than java based on a simple program like
that, where the JVM has the disadvantage of not being partially loaded into memory already, I'll leave that to
you.