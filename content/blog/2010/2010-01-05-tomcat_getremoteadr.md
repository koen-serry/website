+++
title = 'Tomcat 6.0.20 finally supports proxied getRemoteAdr()'
date = 2010-01-05
publishdate = 2010-01-05
thumbnail = "/thumbs/connected.png"
hidePageThumbnail = true
+++

I've encountered <a href="https://issues.apache.org/bugzilla/show_bug.cgi?id=47330">this bug</a> recently as I wanted to
find relate sessions with their originator on a load-balanced tomcat in front of an nginx acting as a proxy. Until now I
always had to put <a href="https://github.com/publicissapient-france/xebia-servlet-extras/blob/b263636fc78f8794dde57d92b835edb5e95ce379/src/main/java/fr/xebia/servlet/filter/XForwardedFilter.java">this</a>
in the lib folder of a tomcat installation. Now the guys from apache finally integrated it into their codebase (6.0.20)
and it works right out of the box. Whoohoo!!
