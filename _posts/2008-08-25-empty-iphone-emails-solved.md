---
ID: 184
post_title: 'Empty iPhone Emails &#8211; Solved'
author: Roman Tarnavski
post_date: 2008-08-25 21:51:28
post_excerpt: ""
layout: post
permalink: >
  http://blog.romant.net/technology/empty-iphone-emails-solved/
published: true
dsq_thread_id:
  - "16198411"
---
<blockquote>NOTE: iPhones Firmware update 2.1, seems to have gotten rid of the problem. If now only Apple would fix the damn <a href="http://twitter.com/romant/statuses/918985782">calendar bug</a></blockquote>
Have you recently sent an email from your beloved iPhone and have it delivered - empty? Then when you look at the sent on your phone you get the lovely: "This message has no content".<!--more-->

<img class="centered" src="http://blog.romant.net/wp-content/uploads/2008/08/img-0007.png" border="0" alt="IMG_0007.PNG" width="320" height="480" />

For me - it was simple - the problem was my signature. Which constituted of a simple '•'. An elevated full-stop, also known as bullet-point.

There appears to be a bug in the iPhone that is as follows:
<ul>
	<li>If you send an email with a • as the LAST character, your sending bar at the bottom of Mail.app will continually say 'Sending', and the email will not even show up in your sent</li>
	<li>If you send an email with words, then • and then some more words - not a problem - it will be delivered</li>
</ul>
If I didn't know better, I'd say that upon Unicode conversion upon sending, the email becomes corrupt through a rogue parser.

Quite an oversight on Apple's behalf, and has only appeared since the 2.0.2 update.

Moral of the story - don't have a bullet point as the last character in your emails, let alone your signature.

Have you noticed any strangeness in your iPhones behaviour?

•