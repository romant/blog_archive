---
ID: 403
post_title: >
  VSI_NODE_net_tcpip_plumb when adding
  Ports
author: Roman Tarnavski
post_date: 2010-06-05 08:50:32
post_excerpt: >
  A simple solution to being unable to add
  another interface to a vSwitch due to a
  SysinfoException.
layout: post
permalink: >
  http://blog.romant.net/technology/vsi_node_net_tcpip_plumb-when-adding-ports/
published: true
dsq_thread_id:
  - ""
---
[caption id="attachment_404" align="aligncenter" width="600" caption="Exception when adding a network - click to enlarge"]<a href="http://blog.romant.net/wp-content/uploads/2010/06/VSI_NODE_net_tcpip_plumb.png"><img src="http://blog.romant.net/wp-content/uploads/2010/06/VSI_NODE_net_tcpip_plumb.png" alt="" title="VSI_NODE_net_tcpip_plumb" width="600" class="size-full wp-image-404" /></a>[/caption]

Adding a new port (i.e. a vMotion interface) to a vSwitch on vSphere/ESX leads to this lovely error message. If you check your <code>vpxd.log</code> you'll see something the image verbalised.

<blockquote>[2010-06-04 15:30:52.411 03152 info 'App'] [VpxLRO] -- ERROR task-54417 -- host-36589 -- vim.host.NetworkSystem.updateNetworkConfig: vim.fault.PlatformConfigFault:
(vim.fault.PlatformConfigFault) {
   dynamicType = <unset>,
   faultCause = (vmodl.MethodFault) null,
   text = "SysinfoException: Node (VSI_NODE_net_tcpip_plumb) ; Status(bad0017)= Out of resources; Message= Instance(0): Input(4) if=0 portset=VMkernel macaddr=00:50:56:76:16:67 tsomss=65535 ",
   msg = "Error during the configuration of the host: SysinfoException: Node (VSI_NODE_net_tcpip_plumb) ; Status(bad0017)= Out of resources; Message= Instance(0): Input(4) if=0 portset=VMkernel macaddr=00:50:56:76:16:67 tsomss=65535 ",
}
</blockquote>

Key here is the <code>Out of resources;</code>  message. The reason for this is none other than the default number of ports for the vSwitch on ESX is 24, and if you have VM's or other interfaces using up ports (such as AppSpeed probes), you will quickly run out. Switch this easily by going to Configuration -> Networking -> Properties [for the vSwitch in question] and up the value up to and including your growth requirements for the future.

<a href="http://blog.romant.net/wp-content/uploads/2010/06/step1_2-1.png"><img src="http://blog.romant.net/wp-content/uploads/2010/06/step1_2-1.png" alt="" title="step1_2" width="600" class="aligncenter size-full wp-image-408" /></a>
<a href="http://blog.romant.net/wp-content/uploads/2010/06/step3_4.png"><img src="http://blog.romant.net/wp-content/uploads/2010/06/step3_4.png" alt="" title="step3_4" width="600" class="aligncenter size-full wp-image-409" /></a>
<a href="http://blog.romant.net/wp-content/uploads/2010/06/step_final.png"><img src="http://blog.romant.net/wp-content/uploads/2010/06/step_final.png" alt="" title="step_final" width="535" class="aligncenter size-full wp-image-410" /></a>


<blockquote>
<strong>NOTE:</strong> After you setup a new host, set it to more ports than you require, as you'll need to restart the host for the ports to be provisioned; best to do this immediately after installation.
</blockquote>

I think a better message would be to explicitly say "Out of available ports on vSwitch - [blah]"; instead of the semi-cryptic one presented.