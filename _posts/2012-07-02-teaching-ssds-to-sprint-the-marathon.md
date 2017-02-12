---
ID: 1102
post_title: 'How AWS taught SSD&#8217;s to sprint the marathon with DynamoDB'
author: Roman Tarnavski
post_date: 2012-07-02 19:18:45
post_excerpt: ""
layout: post
permalink: >
  http://blog.romant.net/technology/teaching-ssds-to-sprint-the-marathon/
published: true
dsq_thread_id:
  - "747991963"
---
<a href="https://twitter.com/bortoelnino">Graham</a> spends a lot of his time tuning and finding the cause of performance issues on some of the largest WebSphere Portal installations. Inevitably during our recent conversation we turned the topic to SSD's, and performance considerations of database workloads atop.

Interestingly the most visible SSD proponent and database service is none other than Amazons AWS service DynamoDB. Launched earlier this year, a database service which can be scaled at the turn of the knob, whilst offering performance, availability and the NoSQL feature-set. Considering the whole premature klonking-out with small-block, highly-randomised IO that hits the SSD controllers, you'd think a very ambitious undertaking.

<hr />

SSD's are great, but not a panacea for all workloads, <em>in their raw state</em>; especially for write-skewed database workloads. One of the largest causes of headaches for SSD Controller manufacturers and those looking to optimize workloads on SSD's is Write Amplification, otherwise known as the variable amount of operations or re-writes of the original size that have to occur before a write is actually processed / stored by the disk.

The conversation reminded me of a post by <a href="http://highscalability.com/blog/2012/5/14/dynamodb-talk-notes-and-the-ssd-hot-s3-cold-pattern.html">Todd Hoff</a> who attended an AWS session of "DynamoDB for Developers", and wrote an interesting line:

<code>Initially they ran into performance problems due to SSD garbage collections cycles</code>

This is inevitable. In my <a href="http://www.slideshare.net/tarnavski/ssd-101">VMUG talk</a> from last week, I refer to the Controller, and rather its FTL (Flash Translation Layer) as the black box of the device, where all the secret sauce of the unit lives. This isn't by mistake, as all the IP around the type of algorithms to use for wear levelling, garbage collection or any internal process resides within.

[caption id="attachment_1107" align="aligncenter" width="1786"]<img class="wp-image-1107 size-full" title="flash-controller" src="http://blog.romant.net/wp-content/uploads/2012/07/flash-controller.png" alt="" width="1786" height="837" /> • SSD controller[/caption]

A single SSD within a single host, can cope with a lot of write-abuse, as given even a few minutes of 'idle' time, can effectively "defragment" its block + page layouts, and thus provide a buffer for the next onslaught. Although en-masse, where AWS operates, this simply will not work. As you will have many thousands of users and transactions in the hundreds of millions (+speculation), the drive will not have time to rest and carry out the vital to its survival, levelling and Garbage Collection.

As the folk over at Tintri have shown, when SSD's are pummelled to a point of saturation OR effectively outside the boundary of when the internal algorithms perform cleanup, the performance or rather the predictability of said performance is significantly diminished. Below you can see latencies of nearly 300ms for an SSD device.

[caption id="attachment_1112" align="aligncenter" width="600"]<img class="wp-image-1112 size-full" title="tintri latency" src="http://blog.romant.net/wp-content/uploads/2012/07/tintri.png" alt="" width="600" height="371" /> • source: tintri blog •[/caption]

When you're operating a on a significant scale, you can't have "unknown" hold you back, so that's why (+speculative mode) Amazon worked directly with the manufactures of their SSD suppliers to have a say in:
<ul>
	<li>When and how GC kicks in</li>
	<li>RAID design across individual cells (similar to vRAID within Violin)</li>
	<li>Granularity of block mapping
<ul>
	<li>How blocks are read+cached+written, and aligned DIRECTLY for DynamoDB's block-sized, in order to not necessarily alleviate, but minimise re-writes</li>
</ul>
</li>
	<li>Locality of writes</li>
</ul>
The last being most interesting, and I believe an absolute <em>must</em> for the future of SSD to have an enduring life in the enterprise. Applications, or rather file-systems and thus API's should allow for the ability to direct or at least specify the inter-relationship of data being written. Simply dumping blocks and forgetting about them is simple, but has dire consequences for the life of the storage medium in this case. Surrounding writes, or data operations with meta about them allows for solutions such as DynamoDB to exist and flourish. This requires a very tight integration between the software and hardware. There's a reason Apple is one of the largest NAND / SSD suppliers (direct to consumer) out there, and why they bought Anobit, the Flash-controller firm last year. Go ponder.