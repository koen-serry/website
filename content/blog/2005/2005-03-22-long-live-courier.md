+++
title = 'Long live courier'
date = 2005-03-22
publishdate = 2005-03-22
thumbnail = "/thumbs/maximalfocus.jpg"
+++

Phew, turned kind of hot yesterday as I was upgrading my mail server (Courier .47 to .49). After a recursive configure
and make, things got messy when I started to optimise permissions (and hence increasing security). Issues I've
encountered so far:

* Public folders need the sticky bit, otherwise it's difficult to keep track who's done what.
* Personal folders can remain under 1 account provided they have permissions 0700.(so no sticky bit there)
* If you've tried your own email account long enough bashing it to pieces, Courier marks it as Temporarily Unavailable.
Only thing to do then is just go into /var/track/ and remove your account in there.
* The file respawnlo, can be modified to restart once every x days (finally found that) 
* maildirshared contains the public folders for everybody

besides those discoveries, I've never had a mailserver that good. I've tried qmail/courier-imap and sendmail/wu-imap and
hopefully I don't start a religious war here but much too difficult to install and to administer.
 