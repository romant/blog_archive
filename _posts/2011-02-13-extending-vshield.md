---
ID: 598
post_title: Extending vShield
author: Roman Tarnavski
post_date: 2011-02-13 11:45:28
post_excerpt: >
  At its core vShield Edge is a very
  lightweight appliance which underpins
  the network scalability within vCloud
  Director. Here I will show you how to
  extend its feature-set.
layout: post
permalink: >
  http://blog.romant.net/technology/extending-vshield/
published: true
dsq_thread_id:
  - "229137479"
---
<img class="aligncenter size-full wp-image-605" src="http://blog.romant.net/wp-content/uploads/2011/02/stickman_puzzle.jpg" alt="" width="500" />
<h3>What</h3>
At its core vShield Edge is a very lightweight appliance mostly based on LinuxFromScratch and the rest comes from VMware's BlueLane acquisition.
<blockquote>If you want to skip the verbosity, skip straight to "How"</blockquote>
We are hearing more about vShield recently, because it is a prerequisite component of vCloud Director. It facilitates the critical piece that makes virtual datacenters work; network connectivity. Unfortunately it is still a young product, and as such feature-poor.

In the last two posts I covered two preludes. The first is how to bake your own NAT forwarding router and use it inplace of vShield within the App Network. Second being how to get inside the vSE appliance.

… which is where we'll start today.

--
<h3>Why</h3>
The unfortunate repercussion of 'rolling-your-own' is that it simply doesn't scale, and that's what vCD + Cloud is all about. I simply can't deploy my own NAT solution with every vApp, and have it integrate with vCloud API's. So I started at the other end. Customizing vShield Edge itself.

For this piece, I wanted to add only two extra features
<ol>
	<li>DNS resolution</li>
Simply put, this will allow for local DNS resolution within each vApp/Organization. More importantly can be made to work with the currently unused DNS Suffix, when creating networks.
	<li>Dynamic DNS Registration</li>
I have a dream… that one day, when you deploy a resource, it will be able to resolve and 'see' others within the same vApp/Organization or vSE 'Network Boundary'.</ol>
<h3>How</h3>
<blockquote>SUMMARY: Get inside vShield Manager, search for vShieldEdge.ovf. Modify it until you're satisfied, and you're done.</blockquote>

<code>
-----
/common/em/components/zones/vShield.ovf
/common/em/components/ni/ovf/vshield-ni-infra.ovf
/common/em/components/edge/vShieldEdge.ovf
-----
</code>
Note that the other vShield products are also available to you.
<blockquote>Am not going to go through every command required to get this to work. If you're stuck at any point whilst attempting this, feel free to drop me a line.</blockquote>
First, lets fix the <code>dhcpd.conf</code> generating file - <code>/root/vSEdge/vse_dhcp_config.pl</code>

Search for "ad-hoc" and replace that line with:

<code>$cmd = "include \"/etc/rndc.key\";\nddns-update-style interim;\nddns-updates on;\nddns-domainname \"wcm.lab\";\nddns-rev-domainname \"in-addr.arpa\";\n";</code>

This will do several things for us:
<ul>
	<li>Setup a trust mechanism between the dhcp and named daemons via the rndc.key</li>
	<li>Set the zone names and allow dhcpd to update them</li>
</ul>
For bind/named itself - since we're dealing with LinuxFromScratch, you can get the code from the LFS <a href="http://www.linuxfromscratch.org/blfs/view/6.3/server/bind.html">project page</a>

Compiling <code>named</code> is done via: <code>./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var --enable-threads --with-libtool --disable-shared ; make</code>

You can then find the executable in <code>./bin/named/named</code>

Unfortunately I haven't been able to figure out how to get it to work with the current libraries present within vShield, so you'll also have to copy some libs across as well.

On vShield:
$ mkdir -p /var/named /named_libs

On your compiling machine:
$ scp /lib/{ld-2.5.so,ld-linux.so.2,libc.so.6,libnsl.so.1,libpthread.so.0} root@vse:/named_libraries

Once that is all set and done, you're just left with having to configure named like on any other machine, which means you will require at the very least:
<ul>
	<li>named.conf</li>
	<li>named.ca</li>
	<li>rndc.conf + key</li>
	<li>zone files</li>
</ul>
I will be using the ones I've prepared earlier for other projects.

… and execute it using:

<code>$ /named_libs/ld-2.5.so --library-path /named_libs/ /usr/sbin/named -g -c /etc/named.conf</code>

I wrapped the above and placed it into <code>/etc/inittab</code>.

After you're done, you overwrite the vShieldEdge.ovf within the manager VM, and have vSE Manager provision your own, custom vShield Edge appliance.

--

The above is meant for those that like to get their fingers a little dirty trying to improve things, this sometimes will break expected functionality.

Some gotchas, and debugging tips:
<ul>
	<li>If for some reason vSE isn't starting, and by looking at the console, you can see that <code>ifconfig</code> doesn't return any interfaces with an IP, run <code>/root/vSEdge/edge_configure.pl</code> - this will nearly always tell you where you went wrong in your vse_ script modifications</li>
	<li>To find linked libraries for any other packages you wish to inject, use <code>export LD_DEBUG=&lt;type&gt;</code> before running a binary where the &lt;type&gt; is referring to [versions | files | libs]</li>
	<li>Don't forget to disable/modify <code>iptables</code>, otherwise you'll have trouble getting inside vSE</li>
	<li>For anything else, there's my contact page</li>
</ul>