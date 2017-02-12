---
ID: 1090
post_title: Cloud Bursting, a reality check
author: Roman Tarnavski
post_date: 2012-04-18 13:52:17
post_excerpt: ""
layout: post
permalink: >
  http://blog.romant.net/technology/cloud-bursting-a-reality-check/
published: true
dsq_thread_id:
  - "654670948"
---
Working with a heavily enterprise-led customer base, I was excited to see an article looking specifically at how large corporates can extend their workloads into the cloud, within the industry this is commonly referred to as cloud bursting and unicorn spotting.

Last night I read a post by Aditya over at Savvis that looks at "horizontal application scaling into the cloud", and what such a <a href="http://blog.savvis.com/2012/04/cloud-burst-three-steps-for-enterprise-scaling.html">solution</a> will encompass.

I take an issue not with the article, but the concept itself in the current incarnation when its applied to the area of enterprise applications.

<hr />

&nbsp;

In order for a workload to be able to 'burst', and as helped by the dictionary it must be able to "break open or apart suddenly and violently". When was the last time you've seen the tightly-coupled layers of any application be able to be broken apart without induced downtime? There are interdependencies not only surrounding applications but the infrastructure supporting them.

The utopia that seems to dominate the cool-aid drinking cloud echo-chamber is an all-public consumption model, where public-only / single-provider is the method for all IT service delivery. Reality is, in privacy, process and control-centric government and enterprise environments <em>some</em> data will always remain in a highly controlled and self-managed environments.

For me, CB's most realistic use-case is going from logical-local or private premises to an external provider, what Forrester terms 'virtual-private'.

In order for CB to be possible, I see two camps developing:

1. The interface between infrastructure, management and monitoring must be very clearly defined to allow for tight integration between all components and thus provide a higher awareness of actions being carried out. Such as performance re-balancing, or disaster mitigation process instantiation
<ul>
	<li>This is where over the last 2 years we've seen companies playing the converged infrastructure card, and spend copious $'s on R&amp;D, integration, testing and product delivery</li>
</ul>
2. Applications must be designed with an "expect-to fail" approach - a discussion which if memory serves right was between <a href="http://twitter.com/reillyusa">@reillyusa</a> and <a href="http://twitter.com/mreferre" target="_blank">@mreferre</a>. In summary, by taking care of failure at a higher layer, specific to the knowledge of your application, it's cheaper than having to design an extensive-feature-rich, all use-case covering container
<div>
<ul>
	<li>Single most potent poster-child of this is Netflix with their Chaos Monkey, and continual &amp; purposeful destruction of systems to test, and thus prevent un-expected failures</li>
</ul>
</div>
Both have their merits in todays market, and for shops which are not tech-savvy and have extensive legacy baggage or who's main purpose isn't IT differentiation, the first choice is a step in the right direction. On the other hand, if you are developing applications for the new world, creating scalable services and are full of zeal to produce the best possible architecture in your niche, then the latter choice is IMO a good approach.

Whatever the correct choice for your bussiness, one constant remains, you need to begin at the application.
<blockquote class="twitter-tweet">Not saying it's impossible, but uploading, converting, VMDK/ OVF/AMIs, starting them, adding IP's to loadbalancers… brr - is a joke at best.

— Roman Tarnavski (@romant) <a href="https://twitter.com/romant/status/192191309010833408" data-datetime="2012-04-17T10:02:33+00:00">April 17, 2012</a></blockquote>
&nbsp;