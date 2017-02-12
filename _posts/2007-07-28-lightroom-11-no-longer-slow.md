---
ID: 48
post_title: 'Lightroom 1.1 &#8211; No longer slow'
author: Roman Tarnavski
post_date: 2007-07-28 15:41:17
post_excerpt: ""
layout: post
permalink: >
  http://blog.romant.net/photography/lightroom-11-no-longer-slow/
published: true
dsq_thread_id:
  - "16198298"
---
After I updated Lightroom to 1.1, I had mixed reaction. At first I was very pleased with the added features such as spraying meta tags onto photos. Although I was very unhappy with the fact that the update rendered my Lightroom, simply unworkable - it was way too slow.
<ul>
	<li> The browsing of photos would stagger once you go from one end of the library to the other</li>
	<li>Previewing of photos was nearly impossible at full resolution, as it would just sit the with the infamous 'Loading' bar at the bottom</li>
</ul>
I'm using this on my laptop [Core Duo T60 2500, with 1.5GB RAM] - and with nearly 5000 photos, Lightroom 1.0 screamed through any task. You'd imagine that 1.1 would be an improvement.

I was convinced it wasn't only my problem, even after numerous posts on DPreview, Adobe's Lightroom Forums - everyone who had a MUCH better machine to play with - reported no problem.

The good news is that there's a light at the end of the tunnel and you can get your speed back.

Two methods [both covered]
<ol>
	<li>Optimize the catalog - doesn't work for everyone, namely myself.</li>
	<li>Re-export your catalog, and let Lightroom rebuild</li>
</ol>
<hr /> So here are the steps
<ol>
	<li>File -&gt; Catalog Settings...</li>
	<li>Under the General tab - click 'Relaunch and Optimize' | for a lot of people, this will do the trick, otherwise continue</li>
	<li>After Lightroom opens back up:
<ol>
	<li>Under Library foldout on the left, select 'All Photographs', to make sure your whole library catalog is being exported.</li>
	<li>File -&gt; Export as Catalog <img src="http://blog.romant.net/wp-content/uploads/2007/07/file%20dialog.jpg" alt="File Dialog" border="0" /></li>
</ol>
</li>
	<li>Pick a new directory not far from where your current Lightroom library exists, this will save you time later on moving it.</li>
	<li><strong>NOTE</strong>: When the dialog opens up, make sure you don't have 'Export negative files'  selected, otherwise depending on how many photos you have, it will take a VERY long time, plus it is completely unnecessary
<img src="http://blog.romant.net/wp-content/uploads/2007/07/export%20catalog.jpg" title="Lightroom export catalog" alt="Lightroom export catalog" height="163" width="348" /></li>
	<li>Click 'Save'</li>
	<li>Once it has finished exporting the library, the previews and is 'done', go and run the new library - you should notice a MUCH snappier response on all actions, and it is now as Lightroom 1.1 should have been.</li>
</ol>