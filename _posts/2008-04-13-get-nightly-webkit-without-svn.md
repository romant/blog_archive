---
ID: 101
post_title: Get Nightly WebKit without SVN
author: Roman Tarnavski
post_date: 2008-04-13 18:59:22
post_excerpt: >
  Download Nightly WebKit build for OSX
  without SVN. Automated webkit
  downloading
layout: post
permalink: >
  http://blog.romant.net/technology/get-nightly-webkit-without-svn/
published: true
dsq_thread_id:
  - "16198399"
---
<img class="alignleft" style="float: left;" src="http://blog.romant.net/wp-content/uploads/2008/04/webkit-icon.png" alt="WebKit Icon" width="128" height="128" />

Everyone agrees that <a href="http://www.webkit.org/">WebKit</a> is the <a href="http://blogs.computerworld.com/safari_is_about_to_get_crazy_fast">faster</a> browser engine. Plus its my favourite browser/engine in OSX

Problem is that it doesn't update itself automatically - and every night there's a beautiful new build that comes out - which I simply must have.

So in order to save you time - here's a little script that I put together this afternoon that will download the latest build at the push of a button.

Initially I wrote it with wget, but realised not everyone will have it installed - hence here's a version with curl
<br/>
<code>
#!/bin/bash
 
#  getWebKit.sh - Obtain the latest WebKit build
#  
#  Created by Roman Tarnavski on 2008-04-13.
#  For an updated version head to www.romant.net
# 
# 
#  Distributed under a Creative Commons Attribution 3.0 License
#  For more details on the license: http://creativecommons.org/licenses/by/3.0/

var_dir="/var/tmp/"

echo -n "Downloading WebPage ..."
location="http://nightly.webkit.org"
curl http://nightly.webkit.org/index.html -o ${var_dir}index.html > .get_webkit.log 2>&1
nightly=`cat ${var_dir}index.html | grep ".dmg" | cut -d '"' -f 2 | uniq`
echo "Done"

filename=`echo $nightly | cut -d '/' -f 5`

echo -n "Getting WebKit ..."
curl $location$nightly -o $var_dir$filename >> .get_webkit.log 2>&1
echo "Done"

if [ $? ]; then
	echo -n "Installing WebKit ..."
	rm -rf /Applications/WebKit.app
	hdiutil attach -quiet "$var_dir$filename"
	cp -R /Volumes/WebKit/WebKit.app /Applications/
	hdiutil detach -quiet /Volumes/WebKit
	echo "Done"
	exit 0
fi

#cleanup
if (( $? )); then rm ${var_dir}index.html && rm $var_dir$filename ; fi

</code>

 <a href="http://blog.romant.net/wp-content/uploads/2008/04/getWebKit.sh">Grab it</a> and let me know how you go

 