---
ID: 205
post_title: >
  VMWare Converter fails to publish a
  split-sparse image to ESX
author: Roman Tarnavski
post_date: 2009-04-20 14:38:05
post_excerpt: |
  Converting a VMWare image results in "FAILED: The object or item referred to could not be found". Included are the steps that will enable the conversion to complete successfully.
layout: post
permalink: >
  http://blog.romant.net/technology/vmware-converter-fails-to-publish-a-split-sparse-image-to-esx/
published: true
dsq_thread_id:
  - "75453331"
---
"FAILED: The object or item referred to could not be found" is the extremely helpful message that VMWare converter displays when it fails.
<img class="img.alignleft" title="vmware_conversion_status.png" src="http://blog.romant.net/wp-content/uploads/2009/04/vmware-conversion-status.jpg" alt="vmware_conversion_status.png" />

Digging deeper, within the logs we can see that there are multiple instances of
<blockquote>"Warning: failed to create directory" and "Warning: failed to clone directory tree".</blockquote>
The simple work-around is to convert the vmdk disk to a monolithic-sparse.

You can do this by issuing:

<code>$ vmware-vdiskmanager -r original.vmdk -t 0 destination.vmdk</code>

This will clone the disk image as well as modify it from being composed of 2GB files for the entirety of your VM to a single vmdk referred to as a 'monolithic-sparse' (merely referring to the fact that it will increase in size automatically to encompass the the VM partition).

After completing the cloning process, you should have no problems in restarting the conversion process, and it should complete as advertised.