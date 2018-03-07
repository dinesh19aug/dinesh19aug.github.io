---
title: Engineyard, Rails 3.x, NGINX, PASSENGER ASSETS NOT DISPLAYED
author: Dinesh
type: post
date: 2012-01-28T08:48:01+00:00
url: /2012/01/28/engineyard-rails-3-x-nginx-passenger-assets-not-displayed/
reddit:
  - 'a:2:{s:5:"count";s:1:"0";s:4:"time";s:10:"1342155979";}'
  - 'a:2:{s:5:"count";s:1:"0";s:4:"time";s:10:"1342155979";}'
delicious:
  - 'a:3:{s:5:"count";s:1:"0";s:9:"post_tags";s:0:"";s:4:"time";s:10:"1330453769";}'
  - 'a:3:{s:5:"count";s:1:"0";s:9:"post_tags";s:0:"";s:4:"time";s:10:"1330453769";}'
dsq_thread_id:
  - 5292097345
  - 5292097345
categories:
  - Tech Notes

---
<span style="color:#ff0000;">CAUTION: Please excuse the diction/grammar/spelling. It&#8217;s 3 AM and I am in a hurry to sleep as I need to drop my friends to airport in exactly 4 hrs</span>.

So I was trying to set up this new application for my wife. I was using [galleria plugin][1] to show a slide like image. Everything was working fine in development so I decided to see how it would look like in production environment if it was deployed in a cloud or virtual server. So I ended up choosing [engineyard][2] because it gives you 500 free hours and you do not need to have dns name. Once the application is deployed on the server, you can view the application on temporary url.

Installing a rails app on [engineyard][2] is pretty easy, however tunneling (ssh) on to the server was a nightmare. I will cover the ssh experience in some other post. The main issue was my [galleria plugin][1] css, images and javascript was not showing correctly. After spending 2 days and mailing the [engineyard][2] (They pretty responsive and quick!!) I realized that there was an issue with application configuration. So I tried to run the application on my mac in production mode and found that galleria javascripts and css files were not loaded. The [engineyard][2] support told me that they were using [passenger and Nginx][3]. So I decided to install the same on my local and experiment.

You can install passenger with Nginx or apache. I used apache version initially but had some issues so decided to use nginx instead.

On an interesting note &#8211; While I was still struggling to load galleria assets using passenger, I searched a lot &#8211; site documentation, rails sites, forums etc., but none told me how to start and stop Nginx &#8230; call me dumb but that is something I did not find on any of the sites until I decided to go through the whole Nginx documentation and there it was&#8230;  buried deep half way through the documentation :-). It should have been there on there installation page.

So this post is in two parts, the first part will walk you through [passenger and Nginx][3] installation and the second part will let you know the configuration changes in your rails app so that assets are loaded properly in production mode.

PART 1: PASSENGER AND NGINX installation

1. Install passenger: Run this in your command line &#8211;

**gem install passenger**

2. Install the Nginx: Run this in your command line

**passenger-install-nginx-module .** If you see permission errors which says that you do not have permission to install then try &#8211;  **sudo**  **passenger-install-nginx-module. **

If you still get error which says &#8211;

**Could not find RubyGem passenger (>= 0) (Gem::LoadError),**  then you probably use rvm to maintain your ruby rails version. So in this case try &#8211;

**rvmsudo passenger-install-nginx-module . **

Now when the installation starts, it will ask you some basic question like should I install some file plugins or location of installation etc., just keep saying yes or hit enter to continue. The whole process will probably take 3-4 minutes to complete.

3. Update the nginx configuration file

By default nginx will be installed in /opt/nginx folder on your mac or linux system. I don&#8217;t know what is the default location for windows. On a lighter note do people actually use windows for RAILS development??? Seriously?? No offense but I have only met people who use windows to try out rails sample apps .

Ok I am done with bashing Windows users 🙂 So to update the configuration file go to **nginx.conf** file under **/opt/nginx/conf** and update the code under **server** tag. You can find more details about nginx configuration [here][4].

server {

**listen 80;**

**server_name  localhost;**

**root /Users/dinesharora/Desktop/Mydocument/ruby-proj/album;**

**passenger_enabled on;**

**passenger\_base\_uri /Users/xxxxx/Desktop/Mydocument/ruby-proj/album;**

…..

After saving the file. Stop the Nginx server

**Stop nginx by going into /opt/nginx/sbin. Then run this command &#8211; **

**sudo ./nginx -s stop**

To start just run **./ngnix**

4. Start your passenger or application.

Go to your rails app folder and run this command in the terminal &#8211; **passenger start** (To stop ctrl+c)

Now by default passenger should start in **production mode,** but mine did not. It started in development mode. The documentation said that it will start in production mode by default but id did not. After racking my brains and going through the whole documentation, I did not find anything. Guess what &#8230;&#8230;. the documentation is outdated on the site. I almost gave up on Rails development and was thinking about going back to Java/Spring/Grails or GWT, but decided to stick a little longer. Anyway too much blabbering about what I did and whined &#8230;. here&#8217;s how to check if your passenger is running in production or development mode.

When you run you **passenger start,** you will in 3rd or fourth line something like this &#8211;

**Log file: /Users/dinesharora/Desktop/Mydocument/ruby-proj/album/log/passenger.3000.log**
  
**Environment: <span style="text-decoration:underline;">development</span>**
  
**Accessible via: http://0.0.0.0:3000/**

If it is running in development mode, the you need to start your application using this command.

**passenger start -e production.**

It goes without saying that if you run into permission issues, run it using **sudo** or **rvmsudo.**

So that&#8217;s it. Your app is running and can be accessed via **http://0.0.0.0:3000/.** I mapped 0.0.0.0 to localhost :-). Anyway I was happy that my installation was successful(I struggled for 4-5 days), without any solutions.

PART 2: ASSETS CONFIGURATION

Well my happiness was short lived because my [galleria][1] plugin was not working. I initially thought it was an issue with [galleria][1] plugin so I switched it with other jquery image slide show plugin, but each had same issue, they all worked fine in development but were not loaded in production mode. I kept seeing this error in the production logs &#8211; Routing error &#8211; [get] /assets/javascripts/galleria/xxxx.js not found 404 error.

Every site said that &#8211; Just set **config.assets.compile = true** and it will start showing up. Well I believed that statement for 4 more days to no avail. I tried playing around with application.js (Sprockets gem &#8211; built in Rails 3.x) bit it did not work. I included the galleria folder as well in the application.js but still no images.

So I had placed my galleria plugin **/app/assets/javascripts/galleria** and I had to access

&#8211; js file

&#8211; galleria/plugins/*.css files etc

&#8211; galleria/plugins/images etc.

I tried placing them in app/assets, lib/assets, vendor/assets but nothing will work. Here are steps if you have the same issue.

&#8211; Open production.rb and make sure you have added or uncommented the following &#8211;

1.

\# Code is not reloaded between requests
  
**config.cache_classes = true**

\# Full error reports are disabled and caching is turned on
  
**config.consider\_all\_requests_local = false**
  
 **config.action\_controller.perform\_caching = true**

**\# Disable Rails&#8217;s static asset server (Apache or nginx will already do this)**
  
 **config.serve\_static\_assets = false**

\# Compress JavaScripts and CSS
  
**config.assets.compress = true**

**\# Don&#8217;t fallback to assets pipeline if a precompiled asset is missed**
  
 **config.assets.compile = true**

**\# Generate digests for assets URLs**
  
 **config.assets.digest = true**

**config.i18n.fallbacks = true**

**\# Send deprecation notices to registered listeners**
  
 **config.active_support.deprecation = :notify**

\# config.assets.initialize\_on\_precompile = false
  
**config.assets.precompile += [&#8220;\*.js&#8221;, &#8220;\*.css&#8221;] <span style="color:#ff0000;">&#8212;&#8212;&#8211; This HAS TO BE ADDED and was the key. Unless you add this line galleria images or any other images which are sub folders in assets or controller specific or personal folder under app, vendor lib will not loaded.</span>**

After you have made the above changes in production.rb file, Rails needs to compile js and css and put them in **public/assets** folder. Now in development environment Rails does it for you but when you are in production, you need to generate assets. So while you are in you rails application folder run this command &#8211;

**rake assets:precompile OR bundle exec rake assets:precompile**. This will attach fingerprint to all the images, css and js files and put them in public/assets folder. Read Rails [documentation][5].

Now start your application in production mode using

**&#8211; passenger start -e production.** 

&#8211; Open the application url.

Voila!!! All the images show up.

&#8211;Cheers

 [1]: http://galleria.io/download/
 [2]: http://www.engineyard.com/
 [3]: http://www.modrails.com/
 [4]: http://www.modrails.com/documentation/Users%20guide%20Nginx.html
 [5]: http://guides.rubyonrails.org/asset_pipeline.html