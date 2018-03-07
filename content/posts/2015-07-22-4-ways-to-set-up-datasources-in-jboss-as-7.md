---
title: 4 ways to set up datasources in Jboss AS 7
author: Dinesh
type: post
date: 2015-07-22T04:44:20+00:00
url: /2015/07/22/4-ways-to-set-up-datasources-in-jboss-as-7/
snap_MYURL:
  -
  -
snapEdIT:
  - 1
  - 1
snapFB:
  - 's:326:"a:1:{i:0;a:11:{s:4:"doFB";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:8:"postType";s:1:"I";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:11:"isPrePosted";s:1:"1";s:2:"do";s:1:"1";}}";'
  - 's:326:"a:1:{i:0;a:11:{s:4:"doFB";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:8:"postType";s:1:"I";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:11:"isPrePosted";s:1:"1";s:2:"do";s:1:"1";}}";'
snapLI:
  - 's:387:"a:1:{i:0;a:12:{s:4:"doLI";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0li";s:8:"postType";s:1:"A";s:10:"SNAPformat";s:41:"New post has been published on %SITENAME%";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:11:"isPrePosted";s:1:"1";s:12:"liMsgFormatT";s:18:"New Post - %TITLE%";s:2:"do";s:1:"1";}}";'
  - 's:387:"a:1:{i:0;a:12:{s:4:"doLI";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0li";s:8:"postType";s:1:"A";s:10:"SNAPformat";s:41:"New post has been published on %SITENAME%";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:11:"isPrePosted";s:1:"1";s:12:"liMsgFormatT";s:18:"New Post - %TITLE%";s:2:"do";s:1:"1";}}";'
snap_isAutoPosted:
  - 1
  - 1
snapIP:
  - 's:269:"a:1:{i:0;a:9:{s:4:"doIP";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0ip";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:9:"613752927";s:5:"pDate";s:19:"2015-07-22 04:44:31";s:2:"do";s:1:"1";}}";'
  - 's:269:"a:1:{i:0;a:9:{s:4:"doIP";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0ip";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:9:"613752927";s:5:"pDate";s:19:"2015-07-22 04:44:31";s:2:"do";s:1:"1";}}";'
snapDI:
  - 's:228:"a:1:{i:0;a:8:{s:4:"doDI";s:1:"1";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:2:"DI";s:5:"pDate";s:19:"2015-07-22 04:44:31";s:2:"do";s:1:"1";}}";'
  - 's:228:"a:1:{i:0;a:8:{s:4:"doDI";s:1:"1";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:2:"DI";s:5:"pDate";s:19:"2015-07-22 04:44:31";s:2:"do";s:1:"1";}}";'
snapDL:
  - 's:293:"a:1:{i:0;a:9:{s:4:"doDL";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0dl";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:32:"32172558dda772888ec77f337f7efe25";s:5:"pDate";s:19:"2016-04-09 00:17:40";s:2:"do";s:1:"1";}}";'
  - 's:293:"a:1:{i:0;a:9:{s:4:"doDL";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0dl";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:32:"32172558dda772888ec77f337f7efe25";s:5:"pDate";s:19:"2016-04-09 00:17:40";s:2:"do";s:1:"1";}}";'
snapTW:
  - 's:162:"a:1:{i:0;a:6:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"1";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:2:"do";s:1:"1";}}";'
  - 's:162:"a:1:{i:0;a:6:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"1";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:2:"do";s:1:"1";}}";'
dsq_thread_id:
  - 5451553281
  - 5451553281
categories:
  - Tech Notes

---
Last year my company decided to move from JBoss 4.x/5.x to Jboss AS 7. We use Maven and IZPack plugin to create automated deployment to Jboss 4. As a part of IZPack plugin, we would write the install.xmls for various environment, which would help us deploy war files, log.xml, jars, properties file in respective folders. So the advantage was that Jboss-4 allows you to deploy several xxx-ds.xml files in deploy folder and you can have multiple apps deployed in same Jboss and each app uses it&#8217;s respective xxx-ds.xml file.

When we started with Jboss AS 7 we learnt that all datasource setting had to be done in **standalone.xml** file. **Jboss 7.0 ** got rid of **xxx-ds.xml** file concept.  The problem with this approach was that we could not use **IZPack** plugin to replace the environment variable if we were deploying multiple apps in the Jboss because every IZPack installation would overwrite the previous **standalone.xml** setting for datasource section. So our deployment engineer had to manually go and configure each datasource in **standalone.xml.** God forbid when we have to update expiring passwords for database every few months, then changing all these passwords would have created a havoc.

As a result, we abandoned or let&#8217;s say delayed the Jboss4 to Jboss AS 7 upgrade. I was not involved in this first attempt however last week I had some time on hand so I started looking into the issue. It turns out the newer version of Jboss AS 7.1.1-FINAL had re-introduced the concept of deployable datasources.

&nbsp;

Let me walk you through <span style="text-decoration: underline;"><em><strong>4 ways</strong></em></span> of configuring the datasources in Jboss AS 7.1.1-FINAL.

**METHOD 1: Standard way. Setting up datasource using standalone.xml(**Not preferred if you have multiple apps in the deployments folder). In this example let&#8217;s assume we are using **Oracle database.**

**Step 1: **Add the Ojdbc14.x.x  jar file in the folder

> `Jboss/modules/com/oracle/jdbc/main`

Keep in mind that the folder structure is really important.

**Step 2:** Create a file **module.xml** and it along with for jdbc jar file. Add the below xml in the module.xml file.

<p id="rPkluam">
  <img class="alignnone size-full wp-image-830 " src="http://javahabit.com/wp-content/uploads/2015/07/img_55af119e4110d.png" alt="" />
</p>

So in the above file, we are defining the location of the jar file in <**resource-root> **tag. You can actually put the jar file in some other folder as well and define the path here but that is not an advisable approach as you will have to provide the full path of the jar file which will cause issues if you have to move the Jboss folder to some other server location.

**Step 3: **Open the **standalone.xml** file under jboss-as-7.1.0.Final\standalone\configuration folder. In the datasources section define datasources. EX:

<p id="YfbyjeY">
  <img class="alignnone size-full wp-image-832 " src="http://javahabit.com/wp-content/uploads/2015/07/img_55af14ad4001c.png" alt="" />
</p>

That&#8217;s it. But this is the standard way of adding the datasource. The next time I want to deploy another application in the same Jboss which uses MySQl, I would have to manually update the **standalone.xml **so that I do not change mess up the datasource set up for Oracle.

&nbsp;

**Method 2: Deploy datasource in stanadalone jar.** Assume we are configuring for Oracle datasource.

**Step 1: **Copy  ojdbc14.xx.jar in the Jboss/standalone/deployments folder.

> **`cp ojdbc14.10.1.05.jar /usr/jboss-as-7.1.1.Final/standalone/deployments`**

**Step 3:** Start the Jboss server to see if the jar file is successfully deployed.

`<strong>09:32:10,400 INFO [org.jboss.as.server] (DeploymentScanner-threads - 2) JBAS018559:<br />
Deployed "mysql-connector-java-5.1.18-bin.jar"</strong>`

**Step 4:** Deploy the datasource file

Just fill in an xml file which ends (as we used to do) in -ds.xml, for example this is a oracle-ds.xml which is suitable for Oracle database. ** **

<p id="tWWAqtZ">
  <img class="alignnone size-full wp-image-835 " src="http://javahabit.com/wp-content/uploads/2015/07/img_55af199091f99.png" alt="" />
</p>

**Step 5:** Deploy your web app and you are good to go.

**At this point you might wonder if there is any pitfall when using the older -ds.xml approach ? well actually if you &#8220;bypass&#8221; the management interface and deploy the datasource in the old way, you will not be able to manage it through the CLI or Web admin interface. As you can see from this snapshot, our datasource is not enlisted through the manageable resources of the Web interface.**

&nbsp;

**METHOD 3: Deploying the datasource along with your application**

You can actually deploy your datasource along with your application, just you used to do in the past.

Here&#8217;s a sample Web application Structure which ships with a datasource (in the WEB-INF folder). For other a JAR archive you would rather need copying the datasource in the META-INF folder:

<p id="AlrPDRU">
  <img class="alignnone size-full wp-image-836 " src="http://javahabit.com/wp-content/uploads/2015/07/img_55af1b7284aa8.png" alt="" />
</p>

**Method 4: Hybrid approach using *-ds.xml + standalone.xml**

I found this approach to be the best because I do not like put jar files inside a WAR applcation which is written in MAVEN. I also do not like to drop JDBC jar files in deployments folder as it I consider it a sacred place for WAR files only. So I figured out a hybrid approach.

**Step 1: **Add the Ojdbc14.x.x  jar file in the folder

> `Jboss/modules/com/oracle/jdbc/main`

Keep in mind that the folder structure is really important.

**Step 2:** Create a file **module.xml** and it along with for jdbc jar file. Add the below xml in the module.xml file.

<p id="rPkluam">
  <img class="alignnone size-full wp-image-830 " src="http://javahabit.com/wp-content/uploads/2015/07/img_55af119e4110d.png" alt="" />
</p>

So in the above file, we are defining the location of the jar file in <**resource-root> **tag. You can actually put the jar file in some other folder as well and define the path here but that is not an advisable approach as you will have to provide the full path of the jar file which will cause issues if you have to move the Jboss folder to some other server location.

**Step 3: **Open the **standalone.xml** file under jboss-as-7.1.0.Final\standalone\configuration folder. In the datasources section define datasources. Here you only define the drivers in the datasources section.

<p id="oWTMQmR">
  <img class="alignnone size-full wp-image-837 " src="http://javahabit.com/wp-content/uploads/2015/07/img_55af1cb4962dc.png" alt="" />
</p>

Notice that I have defined 2 drivers and have named them as &#8220;**mssql**&#8221; and &#8220;**oracle**&#8220;. Also notice the module, this is suppose to be exactly like the folder structure of jar file under **jboss/modules ** section.

**Step 4: **Create a **xx-ds.xml **file and drop it in deployments folder.

<p id="QTrNkpa">
  <img class="alignnone size-full wp-image-838 " src="http://javahabit.com/wp-content/uploads/2015/07/img_55af1dc878ffc.png" alt="" />
</p>

Notice that I have commented out the **<drivers> section. **The way Jboss figures out the driver is by looking at tag name **<driver>oracle</driver> **in my **xx-ds.xml.**

&nbsp;

That&#8217;s it.

~Ciao
