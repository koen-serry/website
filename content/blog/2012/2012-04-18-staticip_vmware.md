+++
title = 'Assigning static ip addresses in VMWare Fusion'
date = 2012-04-18
publishdate = 2012-04-18
thumbnail = "/thumbs/maximalfocus.jpg"
+++

I'm using VMWare Fusion on my laptop, even though I regret not being able to use the power
of <a href="http://vagrantup.com/">Vagrant</a> with VirtualBox, the combination with puppet allows me to
do reach something similar.

However latest releases of Fusion seemed to have dropped the boot.sh which allowed you 
to restart your vm's dhcp daemon.

Apparently the new approach is:

```shell
/Applications/VMware Fusion.app/Contents/Library/services.sh --stop
/Applications/VMware Fusion.app/Contents/Library/services.sh --start
```

and yes, just a shell script to restart your dhcpd or sending a signal would have been better, 
but the extensions need to be loaded in a certain order apparently.
