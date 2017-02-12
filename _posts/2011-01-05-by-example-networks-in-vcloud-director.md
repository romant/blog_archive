---
ID: 535
post_title: 'By Example &#8211; Networks in vCloud Director'
author: Roman Tarnavski
post_date: 2011-01-05 17:31:08
post_excerpt: "In order to demonstrate to some customers, partners and colleagues that haven't had a chance to enjoy vCloud Director yet, I've recently prepared some videos which demonstrate how you go setup a network within vCD."
layout: post
permalink: >
  http://blog.romant.net/technology/by-example-networks-in-vcloud-director/
published: true
dsq_thread_id:
  - "203104345"
---
In order to demonstrate to some customers, partners and colleagues that haven't had a chance to enjoy vCloud Director yet, I've recently prepared some videos which demonstrate how you setup a network within an Organization on top of vCD. They're designed to be completely self-sufficient, so the 'intro' is re-used.
<h4>Direct Network</h4>
This is by far the most … straight forward way of providing your VM's with an outside connection. <iframe src="http://player.vimeo.com/video/18452797" width="480" height="385" frameborder="0"><a href="http://vimeo.com/18452797">vCloud Director Networking : Part 1 : Direct External</a>

</iframe> <a href="http://vimeo.com/18452797">vCloud Director Networking : Part 1 : Direct External</a>
<h4>Routed Network</h4>
The elegance of vShield Edge allows you to configure DHCP, Firewall, and NAT IP Mapping through an easy to click-through UI. Be it for your Organization or vApp. Here I'll show you how to setup a NAT-Routed vShield backed internal network. <iframe src="http://player.vimeo.com/video/18452976?byline=0&amp;portrait=0" width="480" height="385" frameborder="0"></iframe> <a href="http://vimeo.com/18452976">vCloud Director Networking : Part 2 : NAT-Routed</a>
<h4>Custom'ish vApp Network</h4>
There are environments that have already invested a lot in customizing their own DHCP server rules, Dynamic DNS registrations, reverse lookups, firewalls… the list goes on. In essence, here I can show you how you can re-use your current soft-router, and have it used within the vCloud realm. <iframe src="http://player.vimeo.com/video/18453095?byline=0&amp;portrait=0" width="480" height="385" frameborder="0"></iframe> <a href="http://vimeo.com/18453095">vCloud Director Networking : Part 3 : Custom Routing Appliance in a vApp</a>