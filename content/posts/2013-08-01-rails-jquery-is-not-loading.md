---
title: 'Rails: Jquery is not loading'
author: Dinesh
type: post
date: 2013-08-01T03:53:51+00:00
url: /2013/08/01/rails-jquery-is-not-loading/
geo_public:
  - 0
  - 0
publicize_reach:
  - 'a:2:{s:7:"twitter";a:1:{i:305128;i:56;}s:2:"wp";a:1:{i:0;i:1;}}'
  - 'a:2:{s:7:"twitter";a:1:{i:305128;i:56;}s:2:"wp";a:1:{i:0;i:1;}}'
publicize_twitter_user:
  - dinesh19aug
  - dinesh19aug
dsq_thread_id:
  - 5454316205
  - 5454316205
categories:
  - Tech Notes

---
It&#8217;s been a while I have posted anything. I have been extremly busy and have been working on an extremely critical project where we were asked to become PCI 2.0 compliant. I worked on some interesting problems however today I will be discussing on something trivial and discuss my frustration about Rails. I have to admit that a number of times I thought I should just give up and start learning Python or stick to my forte i.e. Java. BUT Ruby/Rails has been a love hate relationship for me. Every few months I pick up Rails again and struggle fixing the set up before I can start working on my website.

So a couple of months back my wife complained that she is not using her website to update client&#8217;s picture because there is no client login and the if she upload their album, the album is visible to everyone. So I fixed that and deployed the application. No issues.

So two months later about a week ago, I checked again with her and like all nagging wife she complained that she is still not using it because she cannot upload multiple images. So like a dutiful husband I set out to set up rails on my new mac and begin coding however my production branch was not working fine. I was seeing issue with [flexslider][1] and found that non of my images were not showing up and Rails complained that JQuery was not defined. I tried everything but I could not make it work.

So if you have been issues with JQuery make sure that you have checked these things:

1. Your gem file should have this line.

>    gem &#8216;jquery-rails&#8217;
  
> gem &#8220;flexslider&#8221;  &#8212; This if you are using flexslider

2. In your application.js, make sure that you have defined jquery and the most important thing &#8230;&#8230; notice the sequence.

//= require jquery_ujs
  
//= require jquery
  
//= require flexslider
  
//= require_tree .

My sequence was incorrect and I had defined juqery before jquery_ujs which was throwing error in my application.

Hope this post helps.

&nbsp;

&nbsp;

~Ciao

&nbsp;

 [1]: http://flexslider.woothemes.com/ "FlexSlider 2"