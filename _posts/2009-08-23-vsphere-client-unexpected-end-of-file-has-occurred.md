---
ID: 259
post_title: 'vSphere Client &#8211; Unexpected end of file has occurred'
author: Roman Tarnavski
post_date: 2009-08-23 17:10:17
post_excerpt: >
  A vSphere Client error Unexpected end of
  file has occurred. The following
  elements are not closed.
layout: post
permalink: >
  http://blog.romant.net/technology/vsphere-client-unexpected-end-of-file-has-occurred/
published: true
dsq_thread_id:
  - "75453404"
---
In the unfortunate scenario that the machine you use to run your vSphere client ever crashes (unfortunately VMware doesn't make an OSX Client), you may wish to start up the client, and click the performance tab. You may be greeted with the following when selecting the "Performance" tab:

[caption id="attachment_260" align="aligncenter" width="600" caption="Unexpected end of file has occurred. The following elements are not closed"]<a href="http://blog.romant.net/wp-content/uploads/2009/08/vSphereClient_Unexpected.png"><img class="size-large wp-image-260" title="vSphereClient_Unexpected" src="http://blog.romant.net/wp-content/uploads/2009/08/vSphereClient_Unexpected-600x95.png" alt="Unexpected end of file has occurred. The following elements are not closed" width="600" height="95" /></a>[/caption]

This is due to a file which hosts all the chart settings (an XML-based key value pair collection) becomes corrupt, and is actually cut off.

Its quite easily found at : <code>c:\Documents and Settings\user_name\Application Data\VMware\server_name-charts.xml</code>

From here, you have several choices:
<ul>
	<li>revert to a backup</li>
	<li>delete it</li>
	<li>clear it (just place <code>&lt;ChartSettings /&gt;</code> inside of it)</li>
</ul>
That's all there is to it. Happy vSphere'ing