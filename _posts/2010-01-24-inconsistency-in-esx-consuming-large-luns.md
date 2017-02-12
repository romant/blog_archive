---
ID: 302
post_title: >
  Inconsistency in ESX consuming large
  LUNs
author: Roman Tarnavski
post_date: 2010-01-24 14:40:46
post_excerpt: >
  Instead of consuming the supported part
  of a presented LUN, ESX will choose the
  spill-over space instead.
layout: post
permalink: >
  http://blog.romant.net/technology/inconsistency-in-esx-consuming-large-luns/
published: true
dsq_thread_id:
  - "75453278"
---
… go with me here. 

You are going to have black caviar (highly recommended). You were provided with 50 grams; you figure you can fit at most 45 grams onto the piece of that delicious dark-rye. So what do you do? Do you disregard and thus throwout the 5 grams? … Well it's not important what YOU would do, its important what VMware does!

Mr. ESX tends to look at the excruciatingly expensive, sustenance-providing caviar, and throws out the majority that it can't handle, and opts for the remains in the hard-to-reach crevices of the jar.

What does this all mean for the geek?

There's a decrepit limit of 2TB minus 512 bytes for each LUN that you can present to ESX. Anything larger, it has no love for. So if you were to present it with a 4TB LUN, you would naïvely assume that you would get the bastardised version of 2TB and the rest would be lost in the ether. I guess that would be somewhat logical.

Lets try it:

[caption id="attachment_303" align="aligncenter" width="600" caption="Capacity vs. Available Space"]<a href="http://blog.romant.net/wp-content/uploads/2010/01/capacity_available.jpg"><img src="http://blog.romant.net/wp-content/uploads/2010/01/capacity_available-600x463.jpg" alt="" title="capacity_available" width="600" height="463" class="size-large wp-image-303" /></a>[/caption]

There you have it. Instead of actually using up as much as ESX'ly possible (~2TB) from a LUN that has been allocated, VMware chose to only pick up the left-overs (~500GB).