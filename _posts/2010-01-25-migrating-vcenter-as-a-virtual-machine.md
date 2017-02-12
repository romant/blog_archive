---
ID: 311
post_title: Migrating vCenter as a Virtual Machine
author: Roman Tarnavski
post_date: 2010-01-25 21:40:57
post_excerpt: >
  What to expect and what actually happens
  when running and migrating a virtual
  vCenter
layout: post
permalink: >
  http://blog.romant.net/technology/migrating-vcenter-as-a-virtual-machine/
published: true
dsq_thread_id:
  - "75453372"
---
The caveats of running vCenter within a VM has been written about to death. So I will mention only what I never found in those posts that is relevant to the environment within which I work:
<h5>greater virtual performance over physical</h5>
Not every environment is large enough to dedicate a whole 8/12/40/96 GB of RAM Blade to a vCenter. Its simply a waste; the premise on which people dive into virtualisation is that green feeling, saving the environment or the saving the USD.
So businesses tend to 'donate' a physical box that will be the nucleus of their virtual offering. Yet this tends to be an underpowered, not-far from decommission door stopper.
As a Virtual Machine, you're able to utilize the benefit of prompt resizing of the hardware, and at the ability to easily place it on higher-powered machines.

That's the benefit, although what REALLY happens when you decide to move your vCenter around?

vMotion Mission Statement:
<blockquote>... Storage VMotion lets you relocate virtual machine disk files between and across shared storage locations while maintaining <strong>continuous service availability</strong> and complete transaction integrity.</blockquote>
To me, that reads - "stuff will happen while we move your data".

Unfortunately that isn't always the case. Here's the scenario.

Host
- DS1
- DS2
- DS3

vCenter was living on DS1 (slow-LUN), and I wanted to put it across to DS2. Since vCenter is very important, it's continuous service availability is crucial. Read: {perfect candidate for svMotion}.

[caption id="attachment_317" align="aligncenter" width="417"]<a href="http://blog.romant.net/wp-content/uploads/2010/01/vsphere_reconnecting.jpg"><img class="size-full wp-image-317" title="vSphere Reconnecting" src="http://blog.romant.net/wp-content/uploads/2010/01/vsphere_reconnecting.jpg" alt="" width="417" height="295" /></a> The message that never went away[/caption]

What happened next is counterintuitive to the credo. The vSphere client freezes, and no new connections can be made to vCenter. If you start monitoring the datastores (kudos to VMware) the VM is actually being transferred.

Once the migration completed, the first time I had to reconnect the vSphere Client; I wasn't happy with this outcome. So I attempted a DS2-&gt;DS3 (both fast-LUNs). Not only did my connection to vCenter not drop this time, but the whole process was seamless and worked as advertised.

[caption id="attachment_313" align="aligncenter" width="1155"]<img class="wp-image-313 size-full" title="vCenter Migration" src="http://blog.romant.net/wp-content/uploads/2010/01/Screen-shot-2010-01-25-at-9.21.31-PM.png" alt="" width="1155" height="228" /> vCenter Migration[/caption]

I ended up moving the VM in which I house SQL Server (vCenterDB) in the same fashion to the faster LUNS, and everything proceeded to operate as designed.

Lesson learnt: get decent storage.