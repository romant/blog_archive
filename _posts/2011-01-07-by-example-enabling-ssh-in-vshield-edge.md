---
ID: 581
post_title: 'By Example: Enabling SSH in vShield Edge'
author: Roman Tarnavski
post_date: 2011-01-07 21:54:10
post_excerpt: >
  By default, no inbound SSH capability
  exists. In the video I show you how you
  can enable it
layout: post
permalink: >
  http://blog.romant.net/technology/by-example-enabling-ssh-in-vshield-edge/
published: true
dsq_thread_id:
  - "204585246"
---
I wanted to learn more about how vShield Edge + Manager appliance works under the covers. By default, no inbound SSH capability exists. In the video I show you how you can enable it, so that you can extract the innards of the appliance, and hack away to create something beautiful.

Initially started writing this as a static blog-post, unfortunately too many screenshots + and explanations would be required. Hence I simply recorded some of the steps.

<iframe src="http://player.vimeo.com/video/18527859?byline=0&amp;portrait=0" width="480" height="300" frameborder="0"></iframe>

<a href="http://vimeo.com/18527859">Enabling SSH in vShield Edge</a>
<h5>Caveats</h5>
<ul>
	<li>There is no possibility that this is in any way supported by our VMware friends, please don't raise SR's on a vSE that you've Roman'ed up!</li>
	<li>In the last step, I replace the <code>root</code> user password. Be sure to restore it from the backup immediately upon ssh'ing back in. As vCloud Director uses that password to interact with vSE, and will be unable to do so.</li>
</ul>