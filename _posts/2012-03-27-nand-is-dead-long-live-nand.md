---
ID: 1063
post_title: NAND is dead, long live NAND
author: Roman Tarnavski
post_date: 2012-03-27 23:05:43
post_excerpt: ""
layout: post
permalink: >
  http://blog.romant.net/technology/nand-is-dead-long-live-nand/
published: true
dsq_thread_id:
  - "639221366"
---
A question was raised internally the other night, specifically looking at the balance between performance and reliability of NAND devices; asked as a result of a paper titled "The Bleak Future of NAND Flash Memory". I must admit, sensationalism and geek link-bait executed to perfection.

[caption id="attachment_1103" align="aligncenter" width="500"]<a href="http://blog.romant.net/wp-content/uploads/2012/03/endurance-performance-ftl.png"><img class="size-full wp-image-1103" title="endurance-performance-ftl" src="http://blog.romant.net/wp-content/uploads/2012/03/endurance-performance-ftl.png" alt="" width="500" /></a> • Endurance vs Performance vs FTL Capability[/caption]

The paper, written by Laura M. Grupp, John D. Davis and Steven Swanson does make some very valid points, and more importantly it is backed with <!--more-->empirical data - which I adore.
<h4>in summary</h4>
The <strong>latency</strong> will be affected by the diminishing size of the manufactured die, and as we approach 12nm, the performance as measured in read response time will increase from being ~20µs to ~25µs, or have a delta of 0.005ms.

Most significant write <strong>throughput</strong> decrease has already occurred between the NAND addressable capacity increasing to 256GB. When you start looking at 1TB to 4TB transition, we're losing less than 250MB/s. Easily alleviated with multiple smaller cards.

Most evident sentence which should be used to ground the academic nature of the article is:
<blockquote>fastest hard drives can sustain no more than 200 IOPs, and the slowest SSD configuration we consider achieves over 32,000 IOPs</blockquote>
So if I were to lose say 15/20 or even 30% of that performance in IOPS per addressable card, and the response time was a hideous 30µs even … am not sure that's quite such a bad trade-off for a 4TB of NAND love.
<h4>clusters to the rescue</h4>
The gloom was very well painted at the beginning of the paper, but as you get beyond prophetic statements and consider the generational shifts that have appeared between tape, myriad of rotating disk, and now Flash for primary storage; you start to realise a single constant. Flash technology is not here to replace spinning disk, but to augmented the delivery of application IO.

As an application stands today, it still hasn't changed its consumption model of the underlying block IO, so for the time-being, fundamental principles of smaller, purpose-chosen storage-devices working as part of a larger RAID-set will continue to result in a significant performance uplift. There are a number of Flash drive and array manufacturers today already designing clusters at not only intra-device at the chip-level, but also across multiple cards in the OS. Each with its own benefits, and each surpassing the metrics Laura et. al claim will slow the adoption of Flash.

For those that read The Innovator's Dilemma may remember that "performance oversupply is an important factor driving the transition" - which we're flooded with on a monthly basis with IOPS records. Only difference now, with excess idle computational capability within the arrays, coupled with smarts around Hierarchical Storage Management (HSM), we can deliver that IO faster than ever before with Flash, but also tap the blended sets of primary storage based on <em>old</em> variations of spinning disk. All provided to the application as a single, seamless stream of superfast bytes.

Lets not split hairs, Flash is here to stay, and in its current incarnation will continue to evolve, reduce latency to microseconds, and drive throughput beyond what a practical amount of duct-taped-together spinning disk can amass.
<h5>References</h5>
1. The Bleak Future of NAND Flash Memory - <a href="http://cseweb.ucsd.edu/users/swanson/papers/FAST2012BleakFlash.pdf">link</a>