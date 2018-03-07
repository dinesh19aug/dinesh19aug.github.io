---
title: How To Share Any Folder On Mac Via Built-in Web Server
author: Dinesh
type: post
date: 2012-07-13T02:43:59+00:00
url: /2012/07/13/share-any-folder-on-mac-via-built-in-web-server/
reddit:
  - 'a:2:{s:5:"count";s:1:"0";s:4:"time";s:10:"1342155190";}'
  - 'a:2:{s:5:"count";s:1:"0";s:4:"time";s:10:"1342155190";}'
dsq_thread_id:
  - 5292097465
  - 5292097465
categories:
  - Tech Notes

---
So what&#8217;s new here? Well I was playing around with [Phonegap][1] to build a small android and ios app. I was able to build a small weather app using Yahoo weather [api][2] but then I came across [Sencha Touch][3] 2.

I wanted to build the same app in [Sencha Touch][3] and compare the two platforms for developing mobile apps and as ap part of its [get started tutorial][4] I had to drop the  [Sencha Touch][3] in a web server. Now as it always happens with me the most simplest of things don&#8217;t work properly for me. I turned on apache server on my mac and added my directory on /etc/apache2/httpd.conf along with and Alias but that did not work out. I constantly ran in forbidden 403 error and tried everything described in various forums but nothing worked and then I came across a post which showed me an alternative way to run a webserver and access my folder without the hassle of apache2 httpd.conf file changes.

It&#8217;s really simple, all you need to do is figure out which folder you want to get access to on web server. In my case I wanted to share **/Users/dinesharora/Desktop/Mydocument/softwares/sencha-touch-2**

so here are the steps:

1. Open the terminal

2. cd /Users/dinesharora/Desktop/Mydocument/softwares/sencha-touch-2

3. type **python -m SimpleHTTPServer**

4. Hit enter

You will see a message &#8211; **Serving HTTP on 0.0.0.0 port 8000 &#8230;**

Now if for some reason you are a stickler and like the old-fashioned 8080 port then just type **<tt>python -m SimpleHTTPServer 8080.</tt>**

That&#8217;s it. Now access your folder via **http://localhost:8000/. **If you want to get access to this over another machine then just type http://.local:8080, so for example in my case it would be http://dinesharora.local:8080.

Now you know how to fly a plane, but do you know how to do a safe landing?? Just hit control +c to shut down the server. Dumb!!

Cheers!!

** **

 [1]: http://www.phonegap.com
 [2]: http://developer.yahoo.com/weather/
 [3]: http://www.sencha.com/products/touch/
 [4]: http://docs.sencha.com/touch/2-0/#!/guide/getting_started