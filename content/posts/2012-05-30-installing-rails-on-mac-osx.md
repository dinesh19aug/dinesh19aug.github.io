---
title: Installing Rails on Mac OSX
author: Dinesh
type: post
date: 2012-05-30T03:12:21+00:00
url: /2012/05/30/installing-rails-on-mac-osx/
tagazine-media:
  - 'a:7:{s:7:"primary";s:0:"";s:6:"images";a:0:{}s:6:"videos";a:0:{}s:11:"image_count";s:1:"0";s:6:"author";s:8:"11764957";s:7:"blog_id";s:8:"11449681";s:9:"mod_stamp";s:19:"2012-05-30 03:12:21";}'
  - 'a:7:{s:7:"primary";s:0:"";s:6:"images";a:0:{}s:6:"videos";a:0:{}s:11:"image_count";s:1:"0";s:6:"author";s:8:"11764957";s:7:"blog_id";s:8:"11449681";s:9:"mod_stamp";s:19:"2012-05-30 03:12:21";}'
delicious:
  - 'a:3:{s:5:"count";s:1:"0";s:9:"post_tags";s:0:"";s:4:"time";s:10:"1338380509";}'
  - 'a:3:{s:5:"count";s:1:"0";s:9:"post_tags";s:0:"";s:4:"time";s:10:"1338380509";}'
reddit:
  - 'a:2:{s:5:"count";i:0;s:4:"time";i:1364811721;}'
  - 'a:2:{s:5:"count";i:0;s:4:"time";i:1364811721;}'
dsq_thread_id:
  - 5460351426
  - 5460351426
categories:
  - Tech Notes

---
I struggled a lot doing this on my mac. I prepared steps and notes while I was upgrading. here are the steps for mac osx. This works for Mac OSX 10.6+

============ Section 1 =================  
Install and update Ruby 1.9 on MAC OSX Snow leopard 10.6.5

1. Install RVM  
Installation instruction: <http://rvm.beginrescueend.com/rvm/install/>

&#8211; In Treminal Run the following command:  
bash < <( curl [http://rvm.beginrescueend.com/releases/ … all-latest][1] )

&#8211; type in terminal: version=$(curl [http://rvm.beginrescueend.com/releases/ … sion.txt);][2]

&#8211; type in terminal:  
mkdir -p ~/.rvm/src/ && cd ~/.rvm/src/ && curl -O [http://rvm.beginrescueend.com/releases/ … on}.tar.gz][3] | tar zxf &#8211; && cd rvm-${version} && ./install

&#8211; The first time you install RVM, you must put the following line into your ~/.bash_profile at the very end, after all path loads etc:  
(If you do not have .bash_profile then open terminal.   
Start up Terminal  
•    Type &#8220;cd ~/&#8221; to go to your home folder  
•    Type &#8220;touch .bash_profile&#8221; to create your new file.  
•    Edit .bash\_profile with your favorite editor (or you can just type &#8220;open -e .bash\_profile&#8221; to open it in TextEdit.  
•    Type &#8220;. .bashrc&#8221; to reload .bashrc and update any functions you add.   
)

&#8211; Update the .bash_profile and add this text.  
[[ -s &#8220;$HOME/.rvm/scripts/rvm&#8221; ]] && . &#8220;$HOME/.rvm/scripts/rvm&#8221;  # This loads RVM into a shell session.

&#8211; Close the terminal and open a new terminal.  
&#8211; Check if rvm is installed correctly by typing  
type rvm | head -1  
This should show result : “rvm is a function ”  
&#8211; type : source ~/.rvm/scripts/rvm  
&#8211; type: rvm notes  
&#8211;

=========== Section 2: After you have done section 1 above ======

II Upgrade to ruby 1.9

&#8211; Make sure that you installed rvm  
Instruction URL- <http://asciicasts.com/episodes/200-rails-3-beta-and-rvm>

&#8211; type: rvm install 1.9.2

&#8211; Check which version of ruby is installed so far by typing “rvm list”.

&#8211; The new version of ruby will be active only until the terminal is open. To make ruby 1.9.2 as default version. Type: rvm  1.9.2 –default

&#8211; If we want to return to previous version of the system. Then type: rvm system –default

III INSTALL RAILS 3  
&#8211; Type: gem install rails

IV INSTALL FRESH COPY OF MYSQL  
&#8211; INSTRUCTION URL: [http://weblog.rubyonrails.org/2009/8/30 … ow-leopard][4]

&#8211; First Stop the mysql server if it is running :   
sudo /opt/local/share/mysql5/mysql/mysql.server stop

&#8211; Now download a fresh copy from this URL:  
[http://weblog.rubyonrails.org/2009/8/30 … ow-leopard][4]

&#8211; Next Install the mysql.pkg → Next install MySQLStartupItem.pkg -→ Install MySQL.prefPane

&#8211; The Mac OS X PKG of MySQL installs itself into  
\`/usr/local/mysql-VERSION&#8217; and also installs a symbolic link,  
\`/usr/local/mysql&#8217;, that points to the new location. If a directory  
named \`/usr/local/mysql&#8217; exists, it is renamed to  
\`/usr/local/mysql.bak&#8217; first. Additionally, the installer creates the  
grant tables in the \`mysql&#8217; database by executing \`mysql\_install\_db&#8217;.

&#8211; Start the MySql server from the System Prefernce pane and make sure that it runs.

&#8211;  Go to /usr/local/mysql/bin and type: ./mysql, This should start start the MYSQL prompt and you can execute the SQl statements.

&#8211; Let us now secure the database by giving it a user id and password.   
In the same package type: ./mysqladmin –u root password <your password>

ISSUES:  
Access Denied for local host after you have set root and password then you need to reset the password..

1. Stop the Server from preference pane.  
2. From /usr/local/mysql/bin folder type the following the terminal:  
  sudo ./mysqld_safe &#8212; &#8211;skip-grant-tables . This will start the server.  
3. Type : ./mysql -u root mysql  
4. type: UPDATE user SET Password=PASSWORD(‘admin&#8217;) where USER=&#8217;root&#8217;;  &#8212; This will set the password as admin.  
5. Restart the server from prefernce pane.

Hope this helps. I used the exact same steps to upgrade to Rails 3.0.3 and ruby 1.9.2

&#8212;Cheers!!!

<div>
  <div>
    <p>
      <a href="http://railsforum.com/viewforum.php?id=3">Go to forum</a> <a title="Permanent link to this topic" href="http://railsforum.com/viewtopic.php?id=42234" rel="bookmark">Go to topic</a> <a title="Permanent link to this post" href="http://railsforum.com/viewtopic.php?pid=134862#p134862" rel="bookmark">Go to post</a>
    </p>
  </div>
</div>

### 14 **dinesh19aug**

 [1]: http://rvm.beginrescueend.com/releases/rvm-install-latest
 [2]: http://rvm.beginrescueend.com/releases/stable-version.txt%29;
 [3]: http://rvm.beginrescueend.com/releases/rvm-$%7Bversion%7D.tar.gz
 [4]: http://weblog.rubyonrails.org/2009/8/30/upgrading-to-snow-leopard