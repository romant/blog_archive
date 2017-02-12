---
ID: 104
post_title: BT-1000P mini-review on a mac
author: Roman Tarnavski
post_date: 2008-06-12 14:36:53
post_excerpt: ""
layout: post
permalink: >
  http://blog.romant.net/technology/bt-1000p-mini-review-on-a-mac/
published: true
dsq_thread_id:
  - "16198401"
---
<p>Am soon going away on a little trip, over to Europe, through Tokyo. Wishing to record my trip, as well as have some data for geocoding the photos, I went on a quest to find a GPS unit that allowed me to:<br /></p>
<ul>

  <li>log data to internal memory</li>

  <li>make sure there's LOTS of memory</li>

  <li>and lots of battery</li>
</ul><br /><!--more-->
<a href="http://blog.romant.net/wp-content/uploads/2008/06/bt-1000p-4.jpg"><img class="aligncenter size-medium wp-image-112" title="bt-1000p set" src="http://blog.romant.net/wp-content/uploads/2008/06/bt-1000p-4-300x200.jpg" alt="bt-1000p pouch cd" width="300" height="200" /></a><br />
After looking at the Sony GPS-CS1, Wintec WBT-100 and GlobalSat DG-100, I concluded that the BT-1000P is by far the best unit for my needs.

<ul>

  <li>First of all, the GPS chip supports up to 51-channels, with sensitivity down to -158dBm, which allows me to get a satellite lock even at the university concrete monstrosity of a car-park.</li>

  <li>It has integrated bluetooth, so I can use it as a replacement for my ageing Holux-236.</li>

  <li>Most importantly, it can log around 200,000 points, with my current configuration of strings, only 122,398 (@5 second intervals, that's 7 days of 24 hour logging before I have to clear it!)</li>
</ul>What pushed me to purchasing after looking at the specifications though is the battery.

<ul>

  <li>The same as you find in most Nokia phones [BL-5C], which can be picked up cheaply off eBay</li>

  <li>Delivers a claimed 32 hrs of logging, although I was able to get 26 hours without any problems, before the little red battery starts to flash. Mind you - I didn't fully charge it, and just started running it soon after receiving it in the post.</li>
</ul>Now I needed the unit to work on a mac, which the BT-1000P doesn't do out of the box. The good news is that there's a project called <a href="http://bt747.wiki.sourceforge.net/">bt747</a> that lets you interact with the BT-1000P.<br />
<br />
<br />
<br />
<br />
<br />
<br />
<table border="0">
  <tbody>
    <tr>
      <td><a href="http://blog.romant.net/wp-content/uploads/2008/06/bt-1000p-3.jpg"><img class="alignnone size-thumbnail wp-image-109" title="bt-1000p-3" src="http://blog.romant.net/wp-content/uploads/2008/06/bt-1000p-3-150x150.jpg" alt="" width="150" height="150" /></a></td>

      <td><a href="http://blog.romant.net/wp-content/uploads/2008/06/bt-1000p-5.jpg"><img class="alignnone size-thumbnail wp-image-108" title="bt-1000p" src="http://blog.romant.net/wp-content/uploads/2008/06/bt-1000p-5-150x150.jpg" alt="bt-1000p apple keyboard" width="150" height="150" /></a></td>

      <td><a href="http://blog.romant.net/wp-content/uploads/2008/06/bt-1000p-2.jpg"><img class="alignnone size-thumbnail wp-image-110" title="bt-1000p-2" src="http://blog.romant.net/wp-content/uploads/2008/06/bt-1000p-2-150x150.jpg" alt="" width="150" height="150" /></a></td>
    </tr>
  </tbody>
</table>Upon connecting the unit via USB the rest of the steps are quite simple:

<ol>

  <li>Download and install the USB-&gt;Serial <a href="http://www.silabs.com/tgwWebApp/public/web_content/products/Microcontrollers/USB/en/mcu_vcp.htm">driver</a></li>

  <li>Download <a href="http://bt747.wiki.sourceforge.net/">bt747</a></li>

  <li>Switch the BT-1000P to 'LOG' mode</li>

  <li>Copy <code>RXTXcomm.jar</code> and <code>librxtxSerial.jnilib</code> into <code>/Library/Java/Extensions</code></li>

  <li>Run <code>run_rxtx.sh</code></li>
</ol>You should get an extremely ugly GUI<br />
<br />
<br />
<br />
<br />
<br />
<table border="0">
  <tbody>
    <tr>
      <td><a href="http://blog.romant.net/wp-content/uploads/2008/06/bt747.jpg"><img class="alignnone size-medium wp-image-105" title="bt747 main window" src="http://blog.romant.net/wp-content/uploads/2008/06/bt747-284x300.jpg" alt="bt747 osx" width="284" height="300" /></a></td>

      <td><a href="http://blog.romant.net/wp-content/uploads/2008/06/bt747_connected.jpg"><img class="alignnone size-medium wp-image-106" title="bt747 connected" src="http://blog.romant.net/wp-content/uploads/2008/06/bt747_connected-284x300.jpg" alt="bt747 osx" width="284" height="300" /></a></td>
    </tr>
  </tbody>
</table>Just hit 'Connect Port Nbr' and you're ready to go. You should get something similar to: After this, all you have to do, is run around the block a few times with your unit in LOG mode. Come back home, run the app again then: Under the 'File' tab, set the Output directory to a location that has world write access, then hit 'Apply &amp; Set the above values' Alternatively create a directory in your <code>/var</code> and <code>sudo chmod 777 &lt;directory&gt;</code>.

<ol>

  <li>Now -&gt; 'Log' tab</li>

  <li>Hit 'Get Log' button {this might take a while, depending on how long your jog was}</li>

  <li>After its complete, feel free to select the output format, either CSV, GPX or KML.</li>
</ol><a href="http://blog.romant.net/wp-content/uploads/2008/06/bt747_getting_log.jpg"></a><a href="http://blog.romant.net/wp-content/uploads/2008/06/bt747_getting_log.jpg"><img class="aligncenter size-medium wp-image-107" title="bt747_getting_log" src="http://blog.romant.net/wp-content/uploads/2008/06/bt747_getting_log-284x300.jpg" alt="bt747 osx" width="284" height="300" /></a><br />
If you chose to export a KML, and you have Google Earth installed, you should get a nice looking track. Unfortunately it is evident that the BT-1000P doesn't filter its points prior to writing them out, resulting in data that isn't representative being recorded, hence you can observe the spike.<br />
<a href="http://blog.romant.net/wp-content/uploads/2008/06/picture-3.jpg"><img class="aligncenter size-medium wp-image-113" title="BT-1000P Google Earth" src="http://blog.romant.net/wp-content/uploads/2008/06/picture-3-300x187.jpg" alt="" width="300" height="187" /></a>
<p>Now to get ready for my last exam tomorrow morning, and then to start packing for the trip. Once I'm back, will report on how the unit goes in the field, and I'll include some geocoded images.<br /></p>
<h3>UPDATE</h3><br />
<a href="http://blog.romant.net/wp-content/uploads/2008/06/bt-1000p.jpg"></a><a href="http://blog.romant.net/wp-content/uploads/2008/06/bt-1000p-1.jpg"><img class="aligncenter size-medium wp-image-115" title="bt-1000p" src="http://blog.romant.net/wp-content/uploads/2008/06/bt-1000p-1-300x300.jpg" alt="bt-1000p POI indicator" width="300" height="300" /></a><br />
<br />
Upon the comment below by Benn, I remembered a feature that this unit has, that every time you take a photo on your camera - you can also hit the big red button on the tom of the unit. This marks the POI in the data stream. Merely allows you to come back for any manual intervention and find interesting parts easier.<br />