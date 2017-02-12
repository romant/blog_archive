---
ID: 447
post_title: Configuring NAT on ESX and ESXi
author: Roman Tarnavski
post_date: 2010-07-11 02:35:22
post_excerpt: >
  A tutorial on how to configure NAT
  within VMware ESX and ESXi
layout: post
permalink: >
  http://blog.romant.net/technology/configuring-nat-on-esx-and-esxi/
published: true
dsq_thread_id:
  - "299824306"
---
ESX doesn't have NAT inbuilt, so here's how to configure it with the help of a VMware appliance called <a href="http://www.pfsense.com/">pfSense</a> (an Open Source [free!] firewall/router).

There are three components in this setup:
<ol>
	<li>Host</li>
	<li>router/pfSense</li>
	<li>NAT Client</li>
</ol>

<h4>Host</h4>

<blockquote>A great read for beginners and those refreshing is the VMware Virtual Networking Concepts <a href="http://www.vmware.com/files/pdf/virtual_networking_concepts.pdf">whitepaper</a></blockquote>

Now lets create a network that our NAT'ed VMs will be using.

<a href="http://blog.romant.net/wp-content/uploads/2010/07/Step2.png"><img src="http://blog.romant.net/wp-content/uploads/2010/07/Step2.png" alt="" title="Step2" width="600" class="aligncenter size-full wp-image-458" /></a>

When prompted under Connection Type, select a 'VM Network', as this is for the typical traffic within the Virtual Machine (not IO or management of your machines).

Lets create a vSwitch that doesn't connect to anything, a dud, a blankie. This will be our NAT'ed environment. It's quite important that you <strong>DON'T</strong> connect a network card to this vSwitch to prevent any inadvertent DHCP leakage. Make sure you have nothing selected.

<a href="http://blog.romant.net/wp-content/uploads/2010/07/Step3_121.png"><img src="http://blog.romant.net/wp-content/uploads/2010/07/Step3_121.png" alt="" title="Step3_12" width="600" class="aligncenter size-full wp-image-466" /></a>

Give it a name to differentiate.

<a href="http://blog.romant.net/wp-content/uploads/2010/07/Step3_13.png"><img src="http://blog.romant.net/wp-content/uploads/2010/07/Step3_13.png" alt="" title="Step3_13" width="600" class="aligncenter size-full wp-image-461" /></a>

Once you're done, click finish and you will have something two network available to your VMs:

<ul>
	<li>VM Network</li>
	<li>NAT Network</li>
</ul>

<a href="http://blog.romant.net/wp-content/uploads/2010/07/Step_last_summary_2.png"><img src="http://blog.romant.net/wp-content/uploads/2010/07/Step_last_summary_2.png" alt="" title="Step_last_summary_2" width="435" class="aligncenter size-full wp-image-469" /></a>

Time to setup pfSense. Once you've downloaded and extracted it. You have the option of either copying it directly to your datastore and then adding directly to inventory, or importing via the <a href="http://www.vmware.com/products/converter/">Standalone Converter</a>. I find the latter is always faster.

<h4>router/pfSense</h4>
<blockquote>
Incase you're converting pfSense first (like I did whilst re-doing it for this post), I recommend you disable the network interfaces until you've finished setting up the host networks. We'll enable these in a later step.

[caption id="attachment_462" align="aligncenter" width="600" caption="Disabled interfaces"]<a href="http://blog.romant.net/wp-content/uploads/2010/07/pfsense_convert_precaution.png"><img src="http://blog.romant.net/wp-content/uploads/2010/07/pfsense_convert_precaution.png" alt="" title="pfsense_convert_precaution" width="400" class="size-full wp-image-462" /></a>[/caption]
</blockquote>

Once the conversion is complete, time to configure our virtual router. pfSense is provided with two NICs out of the box. One for the WAN interface (which is your internal LAN), and one for 'its' LAN - the one on which it will be servicing DHCP requests.

Mark down the last 4 digits of the MAC address, these will help to validate the following step.

[caption id="attachment_457" align="aligncenter" width="400" caption="Configuring pfSense NICs"]<a href="http://blog.romant.net/wp-content/uploads/2010/07/Step_last.png"><img src="http://blog.romant.net/wp-content/uploads/2010/07/Step_last.png" alt="" title="Step_last" width="400" class="size-full wp-image-457" /></a>[/caption]

Start the pfSense VM. You will be guided through the mapping of the interfaces, and just to make sure - check to see the MAC addresses matching to the VM Network (in my case 67:3c) and NAT Network (67:46).

<a href="http://blog.romant.net/wp-content/uploads/2010/07/pfsense_config_2.png"><img src="http://blog.romant.net/wp-content/uploads/2010/07/pfsense_config_2.png" alt="" title="pfsense_config_2" width="600"  class="aligncenter size-full wp-image-451" /></a>

Upon following the wizard, and if you've followed everything accordingly (or rather I documented the steps properly) you will be shown the interfaces within pfSense, their mapping (WAN vs LAN) and IP addresses.

<a href="http://blog.romant.net/wp-content/uploads/2010/07/pfsense_summary.png"><img src="http://blog.romant.net/wp-content/uploads/2010/07/pfsense_summary.png" alt="" title="pfsense_summary" width="600" class="aligncenter size-full wp-image-455" /></a>

<h4>NAT Client[s]</h4>
You are now ready to assign clients on this host to the NAT Network and have them pick up addresses dished out by your shiny new appliance.

<a href="http://blog.romant.net/wp-content/uploads/2010/07/client_network.png"><img src="http://blog.romant.net/wp-content/uploads/2010/07/client_network.png" alt="" title="client_network" width="600" class="aligncenter size-full wp-image-448" /></a>

The whole setup takes just under 5 minutes from start to finish to complete.