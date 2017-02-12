---
ID: 81
post_title: Google Apps and Domains semi-Integration
author: Roman Tarnavski
post_date: 2008-01-29 17:33:38
post_excerpt: ""
layout: post
permalink: >
  http://blog.romant.net/technology/google-apps-and-domains-semi-integration/
published: true
dsq_thread_id:
  - "16198336"
---
Gmail/Gcal and Google Reader, my most used  webapps within Google Apps. Although if you’re a dedicated geek or merely wish to exhibit more control over your email experience, you’d be well accustomed with Google Apps For Your Domain [GAFYD]. Where-by you’d have Google look after your e-mail needs at the very least.<!--more-->
<table border="0">
<tbody>
<tr>
<td><img src="http://blog.romant.net/wp-content/uploads/2008/01/google-apps-logo.gif" alt="Google Apps Logo" />vs.</td>
<td><img src="http://blog.romant.net/wp-content/uploads/2008/01/gmail_logo.gif" alt="GMail Logo" /></td>
</tr>
</tbody></table>
Unfortunately until <a href="http://googlesystem.blogspot.com/2008/01/associate-email-addresses-with-google.html">recently</a> - you had to maintain two accounts in order to utilize the above-mentioned applications. One for your ‘Google Account’ [you@gmail.com] – and your domain account [you@yourdomain.com]. Zoli has written <a href="http://www.zoliblog.com/2008/01/20/google-apps-and-account-chaos-almost-fixed/">a post</a> which in great detail explains the process. For those brave enough - a summary of the steps follows.

So how do you pseudo-integrate the two accounts together? Quite simple as it turns out [check the warning below]
<blockquote>
<ol>
	<li>Log into your Google account and go to <a title="Manage Account" href="https://www.google.com/accounts/ManageAccount">Manage Account</a></li>
	<li>Under 'My Services' - Click <a title="Edit Services" href="https://www.google.com/accounts/EditServices">Edit</a> Services</li>
	<li>Delete Gmail
<ul>
	<li>IMPORTANT: Specify your domain account email as your new login account. [you@yourdomain.com]</li>
You’ll have a few verification stages – follow the instructions.</ul>
</li>
</ol>
</blockquote>
That's it - you’re done

The password for your Google Account remains the same, and chances that it is different to your domain password [unless you use a 1 password fits all policy].

You can now utilize your iGoogle page, Google Reader and any other pages you’re accustomed to that poor integration required two usernames to utilize.

I mentioned the fact that this is pseudo-integration due to the fact that as far as Google is concerned – they [your Google account and your Domain account] are two complete separate accounts; this is shown by the fact that it still requires you to log into your domain when checking email, and the mere fact that there are two password for seemingly the same account.

The expectation is that one day Google will truly provide a seamless, single-sign-on solution. Hopefully soon. At least now you can participate with Groups and Reader as a domain account.
<h3>Warning</h3>
· All your Gmail data will be deleted within 2 days. So make sure you migrate your data first if you wish to keep it.