---
ID: 368
post_title: ESX 4.x kickstart and booting from SAN
author: Roman Tarnavski
post_date: 2010-05-08 20:39:04
post_excerpt: >
  ESX 4 kickstart and considerations for
  booting from SAN
layout: post
permalink: >
  http://blog.romant.net/technology/esx-4-x-kickstart-and-booting-from-san/
published: true
dsq_thread_id:
  - "207670185"
---
Kickstarts are wonderful. Simple and effective. The ability to automate the mundane installations for *nix all about. In my case, I need to automate the installation of hosts that will be booting from SAN.

We have an admin that once installed a couple of ESX hosts atop other host's boot LUNs. It's pointless blaming the admin, as there's a basic rule that must be followed at all times that will prevent this from happening.

<blockquote>NOTE: Don't let the host see boot LUNs for any other host than itself.</blockquote>

[caption id="attachment_371" align="aligncenter" width="400" caption="ESX Dedicated Boot LUNs"]<a href="http://blog.romant.net/wp-content/uploads/2010/05/Untitled.png"><img src="http://blog.romant.net/wp-content/uploads/2010/05/Untitled.png" alt="" title="ESX Dedicated Boot LUNs" width="400" class="size-full wp-image-371" /></a>[/caption]

This can be accomplished with:
<ul>
	<li>LUN Masking (on the host HBA)</li>
	<li>SAN Zoning (on your fabric)</li>
	<li>Port Grouping (on your storage)</li>
</ul>

Horror story aside, lets have a look at a basic kickstart for the ESX. When you install ESX by hand, it creates a <code>ks.cfg</code> file in root's home. Inside you will find the host configuration at the time of install.

<blockquote>
ASSUMPTION: You have already provisioned the necessary space on your array for your host, and have mapped the host access to that LUN.
</blockquote>

After a few modifications and some cleanup, I ended up with the following
<code>
accepteula

keyboard us

auth  --enablemd5 --enableshadow

#this will work on all 'fresh' LUNs. If you want to an
#existing vmfs store, then add --overwritevmfs
clearpart --firstdisk

install cdrom

rootpw --iscrypted $1$MoIxblff$td1t5Oe4Kq8KZqyByh5Bc1

timezone --utc 'Australia/Sydney'

network --addvmportgroup=true --device=vmnic0 --bootproto=dhcp

part '/boot'  --fstype=ext3 --size=1100  --onfirstdisk
part 'none'  --fstype=vmkcore --size=110  --onfirstdisk
part 'HOSTNAME_boot'  --fstype=vmfs3 --size=9232 --grow  --onfirstdisk

virtualdisk 'esxconsole' --size=8232 --onvmfs='HOSTNAME_boot'

part 'swap'  --fstype=swap --size=1228 --onvirtualdisk='esxconsole'
part '/var/log'  --fstype=ext3 --size=2000 --onvirtualdisk='esxconsole'
part '/'  --fstype=ext3 --size=5000 --grow --onvirtualdisk='esxconsole'

%post --interpreter=bash

# ntp settings
esxcfg-firewall --enableService ntpClient
chkconfig ntpd on
cat > /etc/ntp.conf <<EOF
# ---- ntp.conf ----
restrict default kod nomodify notrap nopeer noquery
restrict -6 default kod nomodify notrap nopeer noquery

#replace with your ntp server address
server x.x.x.x

hostname HOSTNAME
sed -i -e "s/PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config

EOF
</code>

I set out to install onto the FIRST available drive. In my case, thats always LUN 0, and if by some accident there's already a VMFS on it - installation will cease (you can accomplish a force through by adding <code>--overwritevmf</code> to the <code>clearpart</code> line.
[caption id="attachment_374" align="aligncenter" width="400" caption="ESX Kickstart Installation"]<a href="http://blog.romant.net/wp-content/uploads/2010/05/Screen-shot-2010-05-08-at-8.14.24-PM.png"><img src="http://blog.romant.net/wp-content/uploads/2010/05/Screen-shot-2010-05-08-at-8.14.24-PM.png" alt="" title="ESX Kickstart Installation" width="400" class="size-full wp-image-374" /></a>[/caption]

Once the setup completes you will be greeted with a "Press <enter> to reboot" - in a normal RedHat install you can get around this by adding <code>reboot --eject</code> just before the <code>%post</code> statement. Unfortunately this doesn't seem to work for ESX. I'll update the post once I find a way.

You may notice that I keep referring to HOSTNAME - that's because the <code>ks.cfg</code> is part of another script which puts together a custom ISO for each of our blades.