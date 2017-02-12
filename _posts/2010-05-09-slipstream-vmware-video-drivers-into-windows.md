---
ID: 380
post_title: >
  Slipstream VMware Video Drivers into
  Windows
author: Roman Tarnavski
post_date: 2010-05-09 18:21:45
post_excerpt: >
  Where to find and how to slipstream just
  the video drivers from VMware Tools into
  Windows.
layout: post
permalink: >
  http://blog.romant.net/technology/slipstream-vmware-video-drivers-into-windows/
published: true
dsq_thread_id:
  - ""
---
Am currently working on automating WebSphere Portal install on Windows. I do not want Windows restarting the first time it comes up, whether its for installing VMware Tools, or any of its drivers. 

What I require is to add the VMware Video drivers to the base Windows installation. This will work for XP/Windows 2003. You can easily integrate the drivers once you've found them with the use of nLite. The trick is in finding them.

First thing you'll need is the <a href="http://blog.romant.net/vmware/where-to-find-http://blog.romant.net/vmware-tools-on-the-esx-host/">VMware Tools ISO</a> that we discovered a couple posts back. 

[caption id="attachment_381" align="aligncenter" width="500" caption="Exploded VMware Tools ISO"]<a href="http://blog.romant.net/wp-content/uploads/2010/05/exploded_iso.png"><img src="http://blog.romant.net/wp-content/uploads/2010/05/exploded_iso.png" alt="" title="Exploded VMware Tools ISO" width="500"class="size-full wp-image-381" /></a>[/caption]

<blockquote><strong>NOTE</strong>: I rename 'VMware Tools[64].msi to vtools[64].msi' </blockquote>

The next step is to extract the <code>vtools64.msi</code> which you can accomplish with:
<code>msiexec /a vtools64.msi /qb TARGETDIR=c:\driver\</code>

[caption id="attachment_382" align="aligncenter" width="500" caption="Extracting VMware Tools"]<a href="http://blog.romant.net/wp-content/uploads/2010/05/Screen-shot-2010-05-09-at-5.50.52-PM.png"><img src="http://blog.romant.net/wp-content/uploads/2010/05/Screen-shot-2010-05-09-at-5.50.52-PM.png" alt="" title="Extracting VMware Tools" width="500" class="size-full wp-image-382" /></a>[/caption]

After a few seconds, you're done. By navigating to the Common64\VMware\Drivers\Video folder, you will find the vmx_svga.inf that you need for nLite as well as the vmx_svga.sys which is the driver. When it comes to nLite - just point it to the directory.

<blockquote><strong>VMware video directory listing</strong>
	vmwogl32.dll
	vmwogl64.dll
	vmx_fb.dll
	vmx_mode.dll
	vmx_svga.cat
	vmx_svga.inf
	vmx_svga.sys
</blockquote>