---
ID: 502
post_title: First week as a vSpecialist
author: Roman Tarnavski
post_date: 2010-08-20 22:01:40
post_excerpt: "The timing couldn't have been better. My first three days on the job, I spent in Vblock training with personnel across the VCE alliance."
layout: post
permalink: >
  http://blog.romant.net/reflection/first-week-as-a-vspecialist/
published: true
dsq_thread_id:
  - "131617270"
---
<h4>Vblock Training</h4>
The timing couldn't have been better. My first three days on the job, I spent in Vblock training with personnel across the VCE alliance. My background not being in networking, and having heard great things about those with CCIE certs, it was a pleasure to witness these guys in action.

[caption id="attachment_507" align="aligncenter" width="512" caption="•"]<img src="http://blog.romant.net/wp-content/uploads/2010/08/bike.png" alt="" title="" width="512" height="445" class="size-full wp-image-507" />[/caption]

<h4>Cisco UCS</h4>
The first time I saw one was at vForum 2009 in Sydney, an ugly piece of semi-gray/teal enclosure with several blades packed to the rafters full of RAM. Dismissed it immediately because it seemed like an immature solution for a company that didn't have the pedigree of building servers.
On my second day of training we started an overview of the chassis, fabrics, blades themselves… something clicked (no, not just <a href="http://twitter.com/romant/status/21410459242">kool-aid</a>). Problem is, when procuring hardware and you have a choice of vendor, you decide on the 'immediate bang for buck', hence inevitably look at Memory + CPU configuration before all else, without giving much consideration to something just as important if not more, 'ease of management' and deployment 'at scale'. Thus is the racking + stacking of a single blade in a single chassis as simple as doing it across  40 chassis and 320 blades?

There are some stunning features within UCS Manager for scalability. Most notably service profiles, which capture things like SAN+LAN connectivity as well as BIOS+Firmware levels into a quasi-template. Simply put, you can define a policy filter for a certain workload that is to be performed by the blade, and UCS Manager will tell you which blades comply in Memory, Connectivity, CPU and IO-Cards and which can be easily configured to the profile with the push of a button. Some great videos which distill some of the configuration + management benefits are <a href="http://www.youtube.com/watch?v=amLXLWn2qOQ">here</a>.

After those initial three days in training on EMC Storage such as CLARiiON + Symmetrix families, UCS and VMware to see how it all fits within the Vblock offering, I only had two days in the office. In that time I attempted to digest the email firehose of Vblock configurations, customer requests and explanations. My manager promptly and kindly offered my services to help break down some vSphere 4.1 features around core-mapping. As any new starter, then had to spend time on setting up phones, VPNs, cards and travel - have you heard about this VMworld thing? *fingers crossed*

<blockquote>• adapted from flickr user  <a href="http://www.flickr.com/photos/striatic">striatic</a></blockquote>