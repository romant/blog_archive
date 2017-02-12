---
ID: 623
post_title: PGP WDE vs. Lion Disk Encryption
author: Roman Tarnavski
post_date: 2011-03-05 20:54:19
post_excerpt: >
  Lion Disk Encryption more than twice as
  fast as PGP WDE.
layout: post
permalink: >
  http://blog.romant.net/technology/pgp-wde-vs-lion-disk-encryption/
published: true
dsq_thread_id:
  - "246061897"
---
Beyond the veil of security, and sense of calm I get when leaving my laptop in the car or airport lobbies; the next most important thing to me is performance (after all, running my VMware lab on a laptop with a single drive isn't exactly cheap). Thus mid last year I invested in a 240 GB OCZ Vertex 2 SSD drive, to run inside my i7 MBP. Encrypting your drive absolutely kills performance, so I did some very un-scientific tests today upon my upgrade to Lion that I wish to share. Below are several Xbench results for HDD performance only, covering 'fresh' HDD, and encrypted. Within Snow Leopard (10.6) with PGP WDE, and in Lion (10.7) with the inbuilt Disk Encryption. <img class="aligncenter wp-image-625 size-full" title="Disk Performance without Encryption" src="http://blog.romant.net/wp-content/uploads/2011/03/p_fresh.png" alt="" width="1516" height="810" /> <img class="aligncenter wp-image-629 size-full" title="Disk Performance with Encryption" src="http://blog.romant.net/wp-content/uploads/2011/03/p_enc.png" alt="" width="1516" height="810" /> First up as you can see we have the fresh install, and nicely enough, with just an OS upgrade, there's an increase in the disk throughput. More importantly though, is the encrypted performance. Averaging out PGP vs Lion, we witness a doubling of the MB/s capability within the latter. On the one hand, its a shame I have a license for PGP that I spent ~$175AUD, on the other, it served its purpose, and is now going to be replaced by something that comes free with the OS, and performs better. Symantec has a talent for buying dying horses.