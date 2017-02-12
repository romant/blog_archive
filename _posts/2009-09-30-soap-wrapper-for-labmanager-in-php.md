---
ID: 268
post_title: >
  SOAP wrapper for LabManager written in
  PHP
author: Roman Tarnavski
post_date: 2009-09-30 23:49:30
post_excerpt: >
  SOAP wrapper for LabManager written in
  PHP
layout: post
permalink: >
  http://blog.romant.net/technology/soap-wrapper-for-labmanager-in-php/
published: true
dsq_thread_id:
  - "75453296"
---
LabManager is a great product for when you have to deal with provisioning of images in a hands-off fashion from the IT team. If you're already a vSphere shop, users don't need access to a vSphere client and can manage the lifecycle of their machines through the browser (Windows only though for the console).

For what I'm building, I needed access to the API provided by VMware, and unfortunately, it is only provided as a SOAP interface. The documentation is a given, although it is of quite a poor standard. Since case-sensitivity is a must, not to mention <a href="http://twitter.com/romant/status/4496796125">correct parameters</a>.

So how do we go about creating an easy to use PHP page which would consume the .NET WebService?

<code>&lt;?php

$namespace = "http://vmware.com/labmanager";

$soap_dat["username"] = "user";
$soap_dat["password"] = "password";
$soap_dat["organizationname"] = "org";
$soap_dat["workspacename"] = "cake";

$client = new SoapClient("https://server_name/LabManager/SOAP/LabManager.asmx?wsdl");

$header = new SOAPHeader($namespace, 'AuthenticationHeader', $soap_dat);

$client-&gt;__setSoapHeaders($header);

$config["configurationType"] = "1";

$result = $client-&gt;ListConfigurations($config);

</code>

<code>print_r($result);</code>

?&gt;

After using some of the methods, I decided to write a wrapper for the LabManager's API, so I could use it within other applications we develop inhouse. You can then call this directly from the command line, and integrate it with your bash/perl - and not have to re-invent the wheel.

As such - I present to you <a href="http://code.google.com/p/phlabmanager">phLabManager</a> - "Simple, lightweight wrapper for LabManager 4.0 SOAP API" written in PHP.

Once you've grabbed the labmanager.php, you can write quite succinct calls directly to the methods, without worrying about the implementation. There's an <a href="http://code.google.com/p/phlabmanager/wiki/HowTo">example</a> on usage available.

I haven't finished implementing all the methods, and in the coming days will endeavour to do so, alternatively - you can do it, and commit into the tree. It would be great to get some help in optimizing my rough implementation.