---
ID: 225
post_title: >
  CLI Wizard for WebSphere Portal
  CumulativeFix Management
author: Roman Tarnavski
post_date: 2009-08-08 22:40:00
post_excerpt: ""
layout: post
permalink: >
  http://blog.romant.net/technology/cli-wizard-for-websphere-portal-cumulativefix-installs/
published: true
dsq_thread_id:
  - "75453423"
---
The unfortunate side-effect of any enterprise-grade software is that it is difficult to manage. There are at least two reasons that I see for this:
<ol>
	<li>Training + certification revenue</li>
	<li>Tools that are clobbered together over years of being driven by big-customer requests/demands, and not a defined architectural vision.</li>
</ol>
One such example is installing and uninstalling cumulative fixes for WebSphere. My first step was to download the PUI, followed by its extraction and then I had to load the extremely cumbersome and slow Java GUI. Then to use it, I either dropped into X11 forwarding the session from my Mac, or for my unfortunate colleagues - they have to start a VNC session first and then use the client. Stupid (not the colleagues).

So I came up with something that wrapped the <code>updatePortal.sh</code> in between a purpose built interface, accessible from the command line. I bring you, the CLI Wizard for Portal CF's.

Lets disassemble the necessary steps first, and start with uninstalling.

Portal places all the CF definitions into <code>PortalServer/version/PK{number}.efix</code>, these are just xml files which describe the PK. What we need is the PK number and the description.

After a few lines of bash, on a server with several CF's installed the output will look similar to this:

<a href="http://blog.romant.net/wp-content/uploads/2009/07/PK_list_installed.png"><img class="aligncenter size-full wp-image-232" title="PK_list_installed" src="http://blog.romant.net/wp-content/uploads/2009/07/PK_list_installed.png" alt="PK_list_installed" /></a>

Not very useful though, yet. So we now allow for actually selecting one of the CF's through the great bash <code>select</code> statement.

Having the PK number, we are easily able to cut/awk and pass this to the trusty <code>updatePortal.sh</code> to do its uninstalling deed.

The installation is much the same, although you must first obtain the PK jar. In the office we have a build server that spits them out in (in zips with the readme). So the script first of all gives a listing of available CF's to install, and then when you choose the appropriate zip, it will download it and install.

You can <a href="http://blog.romant.net/wp-content/uploads/2009/08/cf_install.sh">download the complete script</a>, and let me know if you have any issues. I thought of distributing this on Google Code, so others that deal with Portal can extend it, as Portal's Java GUI leaves much to be desired.