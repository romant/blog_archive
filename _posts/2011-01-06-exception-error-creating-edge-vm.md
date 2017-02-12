---
ID: 561
post_title: 'Exception: Error creating Edge VM'
author: Roman Tarnavski
post_date: 2011-01-06 11:20:35
post_excerpt: >
  Upon trying to create a Routed network
  within vCD, you can be faced with a
  "Error creating Edge VM" message. If you
  look within the debug logs, the
  stack-trace will look something like
layout: post
permalink: >
  http://blog.romant.net/technology/exception-error-creating-edge-vm/
published: true
dsq_thread_id:
  - "203662266"
---
Upon trying to create a NAT-Routed network within vCD, you can be faced with a 

<blockquote>"Error creating Edge VM"</blockquote>

If you look within the debug logs, the excerpt of the stack-trace will look something like this:
<code>
com.vmware.ssdc.util.LMException: Error creating Shield network appliance.
… blah blah
at java.lang.Thread.run(Thread.java:619)
Caused by: com.vmware.ssdc.util.LMException: Error creating Edge VM.
... 17 more
Caused by: java.lang.NullPointerException
… yadda yadda
</code>

[caption id="attachment_565" align="aligncenter" width="600" caption="Click image to enlarge "]
<a href="http://blog.romant.net/wp-content/uploads/2011/01/Error-creating-Edge-VM.png">
<img src="http://blog.romant.net/wp-content/uploads/2011/01/Error-creating-Edge-VM.png" alt="" title="Error creating Edge VM" width="600" class="aligncenter size-full wp-image-565" /></a>[/caption]

The cause is a misconfigured ESX Host that is sitting in the same resource pool as other Hosts connected to the dVS against which vCD is trying to create the network group.

Solution being to either remove the host, or alternatively verify that all hosts are connected EQUALLY to the dVS. This is where Host Profiles come in very handy.

I apologise for the lack of a vCD screenshot, I fixed the problem before realising that it was one; at least there will always be logs. Once you do see this again, feel free to send in a screenie.

<h5>Related Local Files</h5>
<code>logs/vcloud-container-debug.log</code>