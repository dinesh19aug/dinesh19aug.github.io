---
title: Using multiple profiles in Maven + Eclipse
author: Dinesh
type: post
date: 2013-03-07T22:32:04+00:00
url: /2013/03/07/using-multiple-profiles-in-maven-eclipse/
publicize_twitter_user:
  - dinesh19aug
  - dinesh19aug
dsq_thread_id:
  - 5441312053
  - 5441312053
categories:
  - Tech Notes

---
It’s possible that many of you already knew this but if not then here’ some basic info on Maven profiles. I have been using maven for over 2 and half years now, and have been copy pasting assembly and install files. I never bothered to know how Maven figures out how to read assembly and install file names. For example- 

**PROBLEM:**

For all my projects I have been using assembly-jboss.xml to put the file/directory information and telling maven about my desired directory structure i.e. Pick files from a/b directory and put it in out directory c/d. The second file install-jboss.xml where I specify my panels, target files etc. It never occurred to me what happens if I change the file names to assembly-zzz.xml and intsall-zzz.xml. 

[<img style="display:inline;border-width:0;" title="Image 1" border="0" alt="Image 1" src="http://www.javahabit.com/wp-content/uploads/2013/03/image1_thumb.png" width="401" height="216" />][1] 

Well to cut the story short I checked out a fellow developer code on my machine and the command “mvn clean install” threw build error which said &#8211;

<font size="3" face="Ve"><strong>[1] [INFO] Searching for file location: C:Dineshworkspaceprov-ld-anin-trunkartifactssrcassemblyassembly-jboss4.xml </strong></font> 

<font size="3" face="Ve"><strong>[2] [INFO] File: C:Dineshworkspaceprov-ld-anin-trunkartifactssrcassemblyassembly-jboss4.xml does not exist. </strong></font> 

<font size="3" face="Ve"><strong>[3] [INFO] File: C:Dineshworkspaceprov-ld-anin-trunksrcassemblyassembly-jboss4.xml does not exist.</strong></font> 

&nbsp;

Now I was using IZPack plugin and always thought the assembly and install xmls are part of IZPack configuration, so for half an hour I was searching “IZPack assembly descriptor”. Needless to say I did not get any releveant search result. After scratching my head a little and doing a text search in Eclipse to figure out how am I telling maven to find the specific files (in my case the fellow developer had named them as assembly-wso2carbon40.xml and install-wso2carbon40.xml). No results.

**SOLUTION:**

In Maven you set up a profile in your .m2/settings.xml. For example my settings.xml looks like this

> <settings>  
> &nbsp;&nbsp;&nbsp; <profiles>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <profile>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <id>jboss4</id>   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <properties>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <java.home></java.home>   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <compileSource>1.5</compileSource>   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <server>jboss4</server>**&nbsp;  
>** &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </properties>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </profile>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </profiles>  
> &nbsp; </settings>

If you will notice I have specified that **<id>jboss4</id>** tag has value jboss4. When maven is building your app, it looks for two files **assemby-xxx.xml** and **install-xxx.xml**. Here xxxin assembly-xxx.xml is the profile name. So in my case it looks in the settings.xml and sees that profile is jboss, so it uses to find a file assembly-jboss.xml and install-jboss4.xml. 

So now the problem was that my developer friend had named the files as **assembly-wso2Carbon40.xml** and **install-wso2Carbon40.xml.** The first thing that came to my mind was let’s change the **<id>jboss4</id>**to ******<id>wso2</id>**, that would resolve my issue. However I had other application where the file was named **assembly-jboss.xml** and **install-jboss4.xml,** which meant that my other application will error out on maven clean install and throw error message could not locate assembly file **assembly-wso2Carbon40.xml** . 

Here’s comes the neat part, you can have multiple profiles in your settings file. So I updated my **.m2/settings.xml**

> <settings>  
> &nbsp;&nbsp;&nbsp; <profiles>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <profile>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **<id>jboss</id>**   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <properties>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <svn.username></svn.username>   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <svn.password></svn.password>   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <java.home></java.home>   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <compileSource>1.5</compileSource>   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <server>jboss4</server>   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <server.home>C:Program Filesjboss-eap-4.3</server.home>   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <server.port>80</server.port>   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </properties>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </profile>  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#ff0000"><profile><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <id>wso2</id> <br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <properties><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <compileSource>1.5</compileSource> <br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <server>wso2carbon40</server> <br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </properties><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </profile><br /></font>&nbsp;&nbsp;&nbsp; </profiles>  
> &nbsp; </settings></p> 

Now when you build the project using Eclipse, just got to Run As ==> Maven Build …&nbsp; and enter Goals = clean install and Profile = wso2

[<img style="border-bottom:0;border-left:0;display:inline;border-top:0;border-right:0;" title="Image 4" border="0" alt="Image 4" src="http://www.javahabit.com/wp-content/uploads/2013/03/image4_thumb.png" width="480" height="335" />][2]

&nbsp;

That’s it!

&nbsp;

~~Cheers!

 [1]: http://www.javahabit.com/wp-content/uploads/2013/03/image1.png
 [2]: http://www.javahabit.com/wp-content/uploads/2013/03/image4.png