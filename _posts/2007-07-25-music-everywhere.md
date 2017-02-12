---
ID: 46
post_title: Music Everywhere
author: Roman Tarnavski
post_date: 2007-07-25 00:54:31
post_excerpt: ""
layout: post
permalink: >
  http://blog.romant.net/technology/music-everywhere/
published: true
dsq_thread_id:
  - "16198296"
---
As with everything, it's always about the amount of time and money you're willing to put in, in order to get what you want.
I like music, and as someone that has a few computers around the house, coupled with a Vista Media Centre - I want to be able to have access to mood altering music throughout.

My music application of choice happens to be iTunes™. Understandably it isn't everyone's favourite, and I must admit - it does seem very sluggish on Windows™ compared to its OSX™ counterpart.

The point of this post is to setup streaming of music to iTunes™ utilising mt-daapd [aka <a href="http://www.fireflymediaserver.org/" title="Firefly">Firefly</a>], <a href="http://www.ubuntu.com" title="Ubuntu">Ubuntu</a>,<a href="http://www.vmware.com" title="VMWare"> VMWare</a> and obviously the mp3's themselves - hosted on a Windows™ share.

Many people will have a 'server' of some sort, be it for the hundred of gigabytes of family photos and videos, a common repository for house mates to exchange files or simply in my case - all of the above.

I have a server that runs Windows™ 2003 Server. My laptop synchronizes with it every time I dock it, thus providing me with a cheap NAS-like solution for my photos, university lectures and assignments.

Also, since Internet radio is something else I like to dabble in, and my ISP providing me a <a href="http://www.internode.on.net/radio/" title="nice list">nice list</a> free from bandwidth charges - and ultimately wishing to purchase a Wi-Fi enabled radio streamer, I decided to enable streaming of music across my house.

You might be asking your self - why am I running a VMWare Server + Linux in order to just stream music held on a Windows™ share? Well there are alternatives, and apps such as Tangerine that will run quite happily on Windows™ itself and serve music - but I do not want to run anything that isn't necessary on the server itself - I prefer to leave it to virtual machines, as it allows for a much quicker re-deployment, coupled with the fact that I need a few other services to run on the VM for the network.

So here's a guide on how to get streaming mp3's with the use of  mt-daapd, linux and about 30 minutes of spare time.

I will use names for usernames and server configurations that I have used, change as needed.

On the Windows™ box:
<ul>
	<li>Create a username "buntu" [assign a password]</li>
	<li>Create a directory which will host the root of your music. So if it's present in H:\Backup\Files\Personal\Music, then share and make sure you share Music, thus it will be accessible via \\quack\music [quack is the name of the server]
<ul>
	<li>Make sure the security as well as the sharing settings allow for "buntu" to have 'read-only' access</li>
</ul>
</li>
</ul>
<ol>
	<li>Download + Install <a href="http://www.vmware.com/download/server/">VMware Server</a></li>
	<li>Download Ubuntu <a href="http://releases.ubuntu.com/7.04/">Desktop/Server</a>  [or a distro of your choice - I will only run through Ubuntu, as it's based on my farourite Debian, only prettier + more user friendly]
<ul>
	<li>I recommend you download the *alternate* ISO, <em>ubuntu-7.04-alternate-i386.iso</em> as with VMWare server, you can get a "no screens found" error, and the <em>alternate</em> install will merely remove the GUI whilst installing Ubuntu.</li>
</ul>
</li>
</ol>
If you're creating the VM - 2 things.
<ol>
	<li>When you're going through the 'New Virtual Machine Wizard' - make sure you select "Use Bridge Networking", as that way you're making it easier for your new virtual machine to have access to the current network and thus the network shares on another computer.
<p style="text-align: center"><img src="http://blog.romant.net/wp-content/uploads/2007/07/bridge.jpg" title="Use Bridge Network - Screenshot" alt="Use Bridge Network - Screenshot" /></p>
</li>
	<li>Hard drive space allocation - if you're going to be using this for something <em>other</em> than just streaming, and have other services in mind for this VM - such as perhaps a dedicated development environment, you might consider giving it more than the default 8Gb.</li>
</ol>
On with it.

Assign the ISO you download as the CD drive.

As I mentioned above,

Proceed through the menus and install Ubuntu, for most - just accept the defaults.
<p style="text-align: center"><img src="http://blog.romant.net/wp-content/uploads/2007/07/installing.jpg" title="Installing Ubuntu - Screenshot" alt="Installing Ubuntu - Screenshot" height="153" width="434" /></p>
Optional:

In order to have the VM start when the  host boots up, select the appropriate options after going to the VM Settings and under the Options tab - you will see - "Startup/Shutdown", with the respective options being now open to you on the right hand side.

Then:
<code>
# apt-get install smbfs
# mkdir /music
# mount -t smbfs -o username=buntu //quack/music /music
# password:</code>
<ul>
	<li>The above should go through, if you have all the permissions set up correctly.</li>
	<li>Now you have to make sure it is mounted on boot. Edit the /etc/fstab and append the following:</li>
</ul>
<small>Please note the space between the source and the mount point</small>
<code>
//quack/music /music cifs username=buntu,password=music,user 0 0
</code>
Then just a quick check:

<code>
# mount /music
# ls /music
</code>
Should return no errors, and you will now have /music mounted each boot.

Time to set up the streaming.

<code>
# apt-get install mt-daapd
# /etc/init.d/mt-daapd start
</code>

Now if you installed something with X, launch your browser of choice [firefox], and point to: http://localhost:3689 (Default username:password --&gt; admin:mt-daapd)

or

alternatively modify the /etc/mt-daapd.conf manually

Here you are able to specify any parameters as well as monitor who's leeching [scratch] listening to your music.

At the very least, I recommend you modify (under Configuration on the site):
<ul>
	<li> Server Name [as per the file itself - 'the stuff that comes up in iTunes']</li>
	<li>Admin password [used to log into the the site]</li>
	<li>Music Folder, set it to '/music'</li>
	<li>Hit 'Save'</li>
</ul>
Now on the status page, hit 'Start Scan' - and you'll see the little counter for 'served' increase quite rapidly. Any iTunes™ instance on the network, will be able to see Quack under shared music.
<p style="text-align: center"><img src="http://blog.romant.net/wp-content/uploads/2007/07/itunes.jpg" title="ITunes Screenshot" alt="ITunes Screenshot" height="317" width="152" /></p>