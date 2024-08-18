+++
title = 'Upgrading to Ubuntu 11.10 with Oracle 11 XE'
date = 2011-11-04
publishdate = 2011-11-04
thumbnail = '/oracle.jpg'
+++

Well it's been **very** busy times since the last time I've posted something here. Anyways, I've installed Oracle XE 11
pretty much the day it came out (4/sep/2011) and I've been pretty happy with it since then. Since it was running on
ubuntu 11.04 and Ubuntu released a newer version (11.10), I thought let's upgrade since it's pretty much a no brainer
with ubuntu (do-release-upgrade and you're good to go). But then things went south...

When restaring the VM oracle didn't seem to be there. Yes the listener was there, but that was about it. 
Where did the database go?

hmm let's see

Connecting on the machine itself with an sql*plus

```
ORA-01034: ORACLE not available
ORA-27101: shared memory realm does not exist
Linux-x86_64 Error: 2: No such
file or directory
Process ID: 0
Session ID: 0 Serial number: 0
```

Ok, maybe it just
didn't autostart for some reason.

```shell
> su -l oracle 
> sqlplus / as sysdba

SQL*Plus:
Release 11.2.0.2.0 Production on Thu Nov 3 21:42:28 2011

Copyright (c) 1982, 2011, Oracle. All rights
reserved.

Connected to an idle instance.

SQL> startup
ORA-00845: MEMORY_TARGET not supported on this system
```

heh?

Memory_target is the new (well since oracle 11) way to handle it's memory. 
Instead of defining your PGA and SGA separately you just tell oracle that it can use so much memory and it'll
try to determine for itself what the correct ratio for your instance should be. Except now...

Apparently one of the big changes for ubuntu 11.10 was that <a href="https://wiki.ubuntu.com/OneiricOcelot/ReleaseNotes">they've moved</a>
away from the /var/run, /var/lock and /dev/shm which oracle used for determining how much shared memory you had. So
now you've got 0 bytes of (shared) memory as far as oracle is concerned...

Currently there are 2 workarounds for it:

* modify the binary oracle executable (I'd rather not, thank you)
* tell oracle what ratio to use instead of letting it figure it out for itself.

So latter approach seemed fit.

Ok here we go:

```shell
> sqlplus / as sysdba
> create pfile='koen.ini' from spfile;

File created.
```

opening up product/11.2.0/xe/dbs/<db>.ini

remove the memory_target entry and replace it by 

```text
pga_aggregate_target=200540160
sga_target=601620480
```

and restart

```shell
> sqlplus / as sysdba
>
startup pfile=/u01/app/oracle/product/11.2.0/xe/dbs/koen.ini

ORACLE instance started.

Total System
Global Area 601272320 bytes
Fixed Size 2228848 bytes
Variable Size 180358544 bytes
Database Buffers
415236096 bytes
Redo Buffers 3448832 bytes
Database mounted.
Database opened.

```

Et voila..

Hope this helps someone having the same issue..
