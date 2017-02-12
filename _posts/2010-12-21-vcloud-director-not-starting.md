---
ID: 529
post_title: vCloud Director Not Starting
author: Roman Tarnavski
post_date: 2010-12-21 14:26:23
post_excerpt: "The 'Could not bind network port' issue fixed when starting vCloud Director "
layout: post
permalink: >
  http://blog.romant.net/technology/vcloud-director-not-starting/
published: true
dsq_thread_id:
  - "194874346"
---
Attempted to bring up vCD and saw the following in <code>vcloud-container-debug.log</code>

<blockquote>| ERROR    | Start Level Event Dispatcher | StartupUtils                   | Error starting application: Could not bind network port: 80 on host address: 172.16.225.131 | 
java.net.BindException: Cannot assign requested address
	at java.net.PlainSocketImpl.socketBind(Native Method)
	at java.net.PlainSocketImpl.bind(PlainSocketImpl.java:365)
…
</blockquote>

One of these days I'll allocate some static IP's to my whole Fusion-bound vLab. Until then - I will put up with DHCP assigned IP's.

To fix, first stop vCD [ <code>vmware-vcd stop</code> ], the modify <code>cloud-director/etc/global.properties</code> to reflect the IP changes for:

<blockquote>
vcloud.cell.ip.primary
consoleproxy.host.https
vcloud.cell.ips
</blockquote>

or anywhere you have the old address[es]. Some love from sed will do the trick here.

Now back to it …