---
ID: 392
post_title: 'Creating bootable ISO : Linux, Solaris, Windows'
author: Roman Tarnavski
post_date: 2010-05-31 12:44:54
post_excerpt: >
  Making a bootable ISO with mkisofs for
  Linux, Solaris and Windows
layout: post
permalink: >
  http://blog.romant.net/technology/creating-bootable-iso-linux-solaris-windows/
published: true
dsq_thread_id:
  - ""
---
Whenever you're automating OS deployments, you will at one point require to build a custom ISO, with your own kickstart, jumpstart or an OEM folder with apps and instructions to boot.

Here are three <code>mkisofs</code> commands that you can use for each OS, and to ease your search a little.

<blockquote><strong>NOTE:</strong> 
<ol>
	<li>You will require to be in the <code>root</code> of each ISO directory</li>
	<li>Remember the lone period "." at end of each statement</li>
</ol>
</blockquote>

<strong>Linux</strong>
<code>
mkisofs -q -V VOLUME_NAME -b isolinux.bin -c boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table -R -J -T -o /LinuxISO.iso .
</code>

<strong>Solaris</strong>
<code>
mkisofs -b boot/grub/stage2_eltorito -c .catalog -no-emul-boot -boot-load-size 4 -boot-info-table -relaxed-filenames -l -ldots -r -N -d -D -V VOLUME_NAME -o /SolarisISO.iso .
</code>

<strong>Windows</strong>
<blockquote>The <code>Bootable_NoEmulation.img</code> normally lives in the [BOOT] folder. I tend to move it.</blockquote>
<code>
mkisofs -q -b Bootable_NoEmulation.img -no-emul-boot -boot-load-seg 1984 -boot-load-size 4 -iso-level 2 -J -joliet-long -l -D -relaxed-filenames -N -V VOLUME_NAME -o /WindowsISO.iso .
</code>