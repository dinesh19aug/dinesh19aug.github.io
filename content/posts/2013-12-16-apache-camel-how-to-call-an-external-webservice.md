---
title: 'Apache Camel : How to call  java webservice'
author: Dinesh
type: post
date: 2013-12-16T03:55:12+00:00
url: /2013/12/16/apache-camel-how-to-call-an-external-webservice/
publicize_facebook_url:
  - https://facebook.com/10152123374678698
  - https://facebook.com/10152123374678698
publicize_twitter_user:
  - dinesh19aug
  - dinesh19aug
publicize_twitter_url:
  - http://t.co/d5YszNc2eq
  - http://t.co/d5YszNc2eq
publicize_linkedin_url:
  - 'http://www.linkedin.com/updates?discuss=&scope=20656194&stype=M&topic=5818196411220512769&type=U&a=3zgu'
  - 'http://www.linkedin.com/updates?discuss=&scope=20656194&stype=M&topic=5818196411220512769&type=U&a=3zgu'
snapIP:
  - 's:252:"a:1:{i:0;a:8:{s:4:"doIP";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0ip";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:9:"574571257";s:5:"pDate";s:19:"2015-04-30 22:57:39";}}";'
  - 's:252:"a:1:{i:0;a:8:{s:4:"doIP";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0ip";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:9:"574571257";s:5:"pDate";s:19:"2015-04-30 22:57:39";}}";'
snap_MYURL:
  - 
  - 
snapEdIT:
  - 1
  - 1
snapDI:
  - 's:102:"a:1:{i:0;a:3:{s:4:"doDI";s:1:"1";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";}}";'
  - 's:102:"a:1:{i:0;a:3:{s:4:"doDI";s:1:"1";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";}}";'
snapDL:
  - 's:130:"a:1:{i:0;a:4:{s:4:"doDL";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";}}";'
  - 's:130:"a:1:{i:0;a:4:{s:4:"doDL";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";}}";'
snapFB:
  - 's:281:"a:1:{i:0;a:9:{s:4:"doFB";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:8:"postType";s:1:"I";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";}}";'
  - 's:281:"a:1:{i:0;a:9:{s:4:"doFB";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:8:"postType";s:1:"I";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";}}";'
snapLI:
  - 's:293:"a:1:{i:0;a:9:{s:4:"doLI";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:41:"New post has been published on %SITENAME%";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";}}";'
  - 's:293:"a:1:{i:0;a:9:{s:4:"doLI";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:41:"New post has been published on %SITENAME%";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";}}";'
dsq_thread_id:
  - 5292097481
  - 5292097481
categories:
  - Tech Notes

---
I have made up my mind to get rid of WSO2 ESB at my office. It is clumsy, buggy, hard to test, no body wants to work on it and the documentation is horrible. I looked at various alternative and <a title="Apache Camel" href="http://camel.apache.org/" target="_blank">Apache Camel</a> was free and easy to set up and work with me.

To cut the story short, I was able to run most of the example but was struggling with <a title="CXF" href="http://cxf.apache.org/" target="_blank">CXF</a> to call a third party service hosted at a random url. The documentation on the website is focused on exposing web service built in <a title="Apache Camel" href="http://camel.apache.org" target="_blank">Camel</a>. I was finally able to figure this out with a couple of slide show on slideshare.

Here&#8217;s the scenario: I have a third party webservice hosted on the web which gives you the the conversion rate between two currencies. I am going to call this web service and log the response.

As usual I will start from scratch. My webservice is hosted at this url &#8211;<a title="http://www.webservicex.net/CurrencyConvertor.asmx?WSDL" href="http://www.webservicex.net/CurrencyConvertor.asmx?WSDL" target="_blank">http://www.webservicex.net/CurrencyConvertor.asmx?WSDL</a>. This webservice exposes a operation called &#8211; &#8220;ConversionRate&#8221;.

I am using Fuse Ide(free &#8211; Developer version) but you can use Intellij Or Eclipse.

Prerequisites &#8211; Must have Maven.

**Step 1: **Create a new Camel-Spring project.

**Step 2: ** Add the following dependencies in your **pom.xml. &#8220;camel-cxf&#8221;**

<pre>&lt;scope><span style="color: #ff0000;">&lt;dependency&gt;</span>

<span style="color: #ff0000;">      &lt;groupId&gt;org.apache.camel&lt;/groupId&gt;</span>

<span style="color: #ff0000;">      &lt;artifactId&gt;camel-cxf&lt;/artifactId&gt;</span>

<span style="color: #ff0000;">      &lt;version&gt;2.10.0.redhat-60024&lt;/version&gt;</span>

<span style="color: #ff0000;">    &lt;/dependency&gt;</span>&lt;/scope></pre>

My pom.xml looks like this &#8211;

> <span style="color: #ff0000;"><!&#8211;?xml version=&#8221;1.0&#8243; encoding=&#8221;UTF-8&#8243;?></span>
> 
> <span style="color: #ff0000;">xmlns=&#8221;http://maven.apache.org/POM/4.0.0&#8243; xmlns:xsi=&#8221;http://www.w3.org/2001/XMLSchema-instance&#8221; xsi:schemaLocation=&#8221;http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd&#8221;></span>
> 
> <span style="color: #ff0000;"> </span>
> 
> <span style="color: #ff0000;">  <modelVersion>4.0.0</modelVersion></span>
> 
> <span style="color: #ff0000;"> </span>
> 
> <span style="color: #ff0000;">  <groupId>com.mycompany</groupId></span>
> 
> <span style="color: #ff0000;">  <artifactId>camel-spring</artifactId></span>
> 
> <span style="color: #ff0000;">  <packaging>jar</packaging></span>
> 
> <span style="color: #ff0000;">  <version>1.0.0-SNAPSHOT</version></span>
> 
> <span style="color: #ff0000;">  <name>A Camel Spring Route</name></span>
> 
> <span style="color: #ff0000;">  <url>http://www.myorganization.org</url></span>
> 
> <span style="color: #ff0000;">  <properties></span>
> 
> <span style="color: #ff0000;">    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding></span>
> 
> <span style="color: #ff0000;">    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding></span>
> 
> <span style="color: #ff0000;">  </properties></span>
> 
> <span style="color: #ff0000;">  <repositories></span>
> 
> <span style="color: #ff0000;">    <repository></span>
> 
> <span style="color: #ff0000;">      <id>release.fusesource.org</id></span>
> 
> <span style="color: #ff0000;">      FuseSource Release Repository</span>
> 
> <span style="color: #ff0000;">      <url>http://repo.fusesource.com/nexus/content/repositories/releases</url></span>
> 
> <span style="color: #ff0000;">      <snapshots></span>
> 
> <span style="color: #ff0000;">        <enabled>false</enabled></span>
> 
> <span style="color: #ff0000;">      </snapshots></span>
> 
> <span style="color: #ff0000;">      <releases></span>
> 
> <span style="color: #ff0000;">        <enabled>true</enabled></span>
> 
> <span style="color: #ff0000;">      </releases></span>
> 
> <span style="color: #ff0000;">    </repository></span>
> 
> <span style="color: #ff0000;">    <repository></span>
> 
> <span style="color: #ff0000;">      <id>snapshot.fusesource.org</id></span>
> 
> <span style="color: #ff0000;">      FuseSource Snapshot Repository</span>
> 
> <span style="color: #ff0000;">      <url>http://repo.fusesource.com/nexus/content/repositories/snapshots</url></span>
> 
> <span style="color: #ff0000;">      <snapshots></span>
> 
> <span style="color: #ff0000;">        <enabled>true</enabled></span>
> 
> <span style="color: #ff0000;">      </snapshots></span>
> 
> <span style="color: #ff0000;">      <releases></span>
> 
> <span style="color: #ff0000;">        <enabled>false</enabled></span>
> 
> <span style="color: #ff0000;">      </releases></span>
> 
> <span style="color: #ff0000;">    </repository></span>
> 
> <span style="color: #ff0000;">  </repositories></span>
> 
> <span style="color: #ff0000;">  <pluginRepositories></span>
> 
> <span style="color: #ff0000;">    <pluginRepository></span>
> 
> <span style="color: #ff0000;">      <id>release.fusesource.org</id></span>
> 
> <span style="color: #ff0000;">      FuseSource Release Repository</span>
> 
> <span style="color: #ff0000;">      <url>http://repo.fusesource.com/nexus/content/repositories/releases</url></span>
> 
> <span style="color: #ff0000;">      <snapshots></span>
> 
> <span style="color: #ff0000;">        <enabled>false</enabled></span>
> 
> <span style="color: #ff0000;">      </snapshots></span>
> 
> <span style="color: #ff0000;">      <releases></span>
> 
> <span style="color: #ff0000;">        <enabled>true</enabled></span>
> 
> <span style="color: #ff0000;">      </releases></span>
> 
> <span style="color: #ff0000;">    </pluginRepository></span>
> 
> <span style="color: #ff0000;">    <pluginRepository></span>
> 
> <span style="color: #ff0000;">      <id>snapshot.fusesource.org</id></span>
> 
> <span style="color: #ff0000;">      FuseSource Snapshot Repository</span>
> 
> <span style="color: #ff0000;">      <url>http://repo.fusesource.com/nexus/content/repositories/snapshots</url></span>
> 
> <span style="color: #ff0000;">      <snapshots></span>
> 
> <span style="color: #ff0000;">        <enabled>true</enabled></span>
> 
> <span style="color: #ff0000;">      </snapshots></span>
> 
> <span style="color: #ff0000;">      <releases></span>
> 
> <span style="color: #ff0000;">        <enabled>false</enabled></span>
> 
> <span style="color: #ff0000;">      </releases></span>
> 
> <span style="color: #ff0000;">    </pluginRepository>  </span>
> 
> <span style="color: #ff0000;">  </pluginRepositories></span>
> 
> <span style="color: #ff0000;"> </span>
> 
> <span style="color: #ff0000;">  <dependencies></span>
> 
> <span style="color: #ff0000;">    <dependency></span>
> 
> <span style="color: #ff0000;">      <groupId>org.apache.camel</groupId></span>
> 
> <span style="color: #ff0000;">      <artifactId>camel-core</artifactId></span>
> 
> <span style="color: #ff0000;">      <version>2.10.0.redhat-60024</version></span>
> 
> <span style="color: #ff0000;">    </dependency></span>
> 
> <span style="color: #ff0000;">    <dependency></span>
> 
> <span style="color: #ff0000;">      <groupId>org.apache.camel</groupId></span>
> 
> <span style="color: #ff0000;">      <artifactId>camel-spring</artifactId></span>
> 
> <span style="color: #ff0000;">      <version>2.10.0.redhat-60024</version></span>
> 
> <span style="color: #ff0000;">    </dependency></span>
> 
> <span style="color: #ff0000;">    <!&#8211; logging &#8211;></span>
> 
> <span style="color: #ff0000;">    <dependency></span>
> 
> <span style="color: #ff0000;">      <groupId>org.slf4j</groupId></span>
> 
> <span style="color: #ff0000;">      <artifactId>slf4j-api</artifactId></span>
> 
> <span style="color: #ff0000;">      <version>1.6.6</version></span>
> 
> <span style="color: #ff0000;">    </dependency></span>
> 
> <span style="color: #ff0000;">    <dependency></span>
> 
> <span style="color: #ff0000;">      <groupId>org.slf4j</groupId></span>
> 
> <span style="color: #ff0000;">      <artifactId>slf4j-log4j12</artifactId></span>
> 
> <span style="color: #ff0000;">      <version>1.6.6</version></span>
> 
> <span style="color: #ff0000;">    </dependency></span>
> 
> <span style="color: #ff0000;">    <dependency></span>
> 
> <span style="color: #ff0000;">      <groupId>log4j</groupId></span>
> 
> <span style="color: #ff0000;">      <artifactId>log4j</artifactId></span>
> 
> <span style="color: #ff0000;">      <version>1.2.17</version></span>
> 
> <span style="color: #ff0000;">    </dependency></span>
> 
> <span style="color: #ff0000;">    <!&#8211; testing &#8211;></span>
> 
> <span style="color: #ff0000;">    <dependency></span>
> 
> <span style="color: #ff0000;">      <groupId>org.apache.camel</groupId></span>
> 
> <span style="color: #ff0000;">      <artifactId>camel-test-spring</artifactId></span>
> 
> <span style="color: #ff0000;">      <version>2.10.0.redhat-60024</version></span>
> 
> <span style="color: #ff0000;">      <scope>test</scope></span>
> 
> <span style="color: #ff0000;">    </dependency></span>
> 
> <span style="color: #ff0000;"><dependency></span>
> 
> <span style="color: #ff0000;">      <groupId>org.apache.camel</groupId></span>
> 
> <span style="color: #ff0000;">      <artifactId>camel-cxf</artifactId></span>
> 
> <span style="color: #ff0000;">      <version>2.10.0.redhat-60024</version></span>
> 
> <span style="color: #ff0000;">    </dependency></span>
> 
> <span style="color: #ff0000;">  </dependencies></span>
> 
> <span style="color: #ff0000;">  <build></span>
> 
> <span style="color: #ff0000;">    <defaultGoal>install</defaultGoal></span>
> 
> <span style="color: #ff0000;">    <plugins></span>
> 
> <span style="color: #ff0000;">      <plugin></span>
> 
> <span style="color: #ff0000;">        <groupId>org.apache.maven.plugins</groupId></span>
> 
> <span style="color: #ff0000;">        <artifactId>maven-compiler-plugin</artifactId></span>
> 
> <span style="color: #ff0000;">        <version>2.5.1</version></span>
> 
> <span style="color: #ff0000;">        <configuration></span>
> 
> <span style="color: #ff0000;">          <source>1.6</source></span>
> 
> <span style="color: #ff0000;">          <target>1.6</target></span>
> 
> <span style="color: #ff0000;">        </configuration></span>
> 
> <span style="color: #ff0000;">      </plugin></span>
> 
> <span style="color: #ff0000;">      <plugin></span>
> 
> <span style="color: #ff0000;">        <groupId>org.apache.maven.plugins</groupId></span>
> 
> <span style="color: #ff0000;">        <artifactId>maven-resources-plugin</artifactId></span>
> 
> <span style="color: #ff0000;">        <version>2.4.3</version></span>
> 
> <span style="color: #ff0000;">        <configuration></span>
> 
> <span style="color: #ff0000;">          <encoding>UTF-8</encoding></span>
> 
> <span style="color: #ff0000;">        </configuration></span>
> 
> <span style="color: #ff0000;">      </plugin></span>
> 
> <span style="color: #ff0000;">      <!&#8211; allows the route <span class="hiddenGrammarError">to be</span> ran via &#8216;mvn camel:run&#8217; &#8211;></span>
> 
> <span style="color: #ff0000;">      <plugin></span>
> 
> <span style="color: #ff0000;">        <groupId>org.apache.camel</groupId></span>
> 
> <span style="color: #ff0000;">        <artifactId>camel-maven-plugin</artifactId></span>
> 
> <span style="color: #ff0000;">        <version>2.10.0.redhat-60024</version></span>
> 
> <span style="color: #ff0000;">      </plugin></span>
> 
> <span style="color: #ff0000;">    </plugins></span>
> 
> <span style="color: #ff0000;">  </build></span>
> 
> <span style="color: #ff0000;"></project></span>

**Step 2: **Under src/main.resources/META-INF folder(if not there then create one) create file called **camel-context.xml. ** Your camel file should like this &#8211;

> <span style="color: #ff0000;"><?xml version=&#8221;1.0&#8243; encoding=&#8221;UTF-8&#8243;?></span>
> 
> <span style="line-height: 1.5; color: #ff0000;">xmlns=&#8221;http://www.springframework.org/schema/beans&#8221;</span>
> 
> <span style="color: #ff0000;">        xmlns:xsi=&#8221;http://www.w3.org/2001/XMLSchema-instance&#8221;</span>
> 
> <span style="color: #ff0000;">        xmlns:cxf=&#8221;http://camel.apache.org/schema/cxf&#8221;</span>
> 
> <span style="color: #ff0000;">        xsi:schemaLocation=&#8221;</span>
> 
> <span style="color: #ff0000;">        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd</span>
> 
> <span style="color: #ff0000;">        http://camel.apache.org/schema/cxf http://camel.apache.org/schema/cxf/camel-cxf.xsd</span>
> 
> <span style="color: #ff0000;">        http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd&#8221;></span>
> 
> <span style="color: #ff0000;"> <span style="line-height: 1.5;"> <cxf:<span class="hiddenSpellError">cxfEndpoint id=&#8221;wsdlEndpoint&#8221;</span></span></span>
> 
> <span style="color: #ff0000;">                     address=&#8221;http://www.webservicex.net/CurrencyConvertor.asmx&#8221;</span>
> 
> <span style="color: #ff0000;">                     endpointName=&#8221;c:SOAPOverHTTP&#8221;</span>
> 
> <span style="color: #ff0000;">                     serviceName=&#8221;c:CurrencyConvertor&#8221;</span>
> 
> <span style="color: #ff0000;">                     xmlns:s=&#8221;http://www.webserviceX.NET&#8221;/></span>
> 
> <span style="color: #ff0000;">  </span>
> 
> <span style="color: #ff0000;">  <camelContext xmlns=&#8221;http://camel.apache.org/schema/spring&#8221;></span>
> 
> <span style="color: #ff0000;">  <route></span>
> 
> <span style="color: #ff0000;">        here is a sample which processes the input files</span>
> 
> <span style="color: #ff0000;">         (leaving them in place &#8211; see the &#8216;noop&#8217; flag)</span>
> 
> <span style="color: #ff0000;">         then performs content based routing on the message using XPath</description></span>
> 
> <span style="color: #ff0000;">        src/data/order?noop=true&#8221;/></span>
> 
> <span style="color: #ff0000;">        <log message=&#8221;${body}&#8221;/></span>
> 
> <span style="color: #ff0000;">        wsdl&serviceName={http://www.webserviceX.NET/}CurrencyConvertor&portName={http://www.webserviceX.NET/}CurrencyConvertorSoap&dataFormat=MESSAGE&#8221;/></span>
> 
> <span style="color: #ff0000;">         <log message=&#8221;${body}&#8221;/></span>
> 
> <span style="color: #ff0000;">    </route></span>
> 
> <span style="color: #ff0000;"></camelContext></span>
> 
> <span style="color: #ff0000;"> </span>
> 
> <span style="color: #ff0000;"></beans></span>

**Step 4: **Place the payload or input data xml in src/data/input/order.xml. The **order.xml **should like this &#8211;

> <span style="color: #ff0000;"><soapenv:Envelope xmlns:soapenv=&#8221;http://schemas.xmlsoap.org/soap/envelope/&#8221; xmlns:web=&#8221;http://www.webserviceX.NET/&#8221;></span>
> 
> <span style="color: #ff0000;">   <soapenv:Header/></span>
> 
> <span style="color: #ff0000;">   <soapenv:Body></span>
> 
> <span style="color: #ff0000;">      <web:ConversionRate></span>
> 
> <span style="color: #ff0000;">         <web:FromCurrency>AUD</web:FromCurrency></span>
> 
> <span style="color: #ff0000;">         <web:ToCurrency>USD</web:ToCurrency></span>
> 
> <span style="color: #ff0000;">      </web:ConversionRate></span>
> 
> <span style="color: #ff0000;">   <!&#8211;<span class="hiddenSpellError">soapenv</span>:Body>&#8211;></span>
> 
> <span style="color: #ff0000;"><!&#8211;<span class="hiddenSpellError">soapenv</span>:Envelope>&#8211;></span>

That&#8217;s it!!!!

<span style="color: #000000;">The interesting part is all in the camel-context.xml. Here&#8217;s what is happening in this file</span>

**src/data/order?noop=true&#8221;/>**

This line reads the file order.xml. The option noop=true makes the file to be read again and again. By default this values is false. If this value is false, then after one read, camel marks it as read and when you run the example for second time, it will not read this file.

**<log message=&#8221;${body}&#8221;/>**

This line will simply log the contents of **order.xml.**

**serviceName={http://www.webserviceX.NET/}CurrencyConvertor&portName={http://www.webserviceX.NET/}CurrencyConvertorSoap&dataFormat=MESSAGE&#8221;/>**

** **This line tells **cxf **component that it needs to call the webservice &#8211;  **http://www.webservicex.net/CurrencyConvertor.asmx?wsdl**

-URL &#8211; is the url of the wsdl **http://www.webservicex.net/CurrencyConvertor.asmx?wsdl**

  * serviceName &#8211; is the name of the service. Remember it is the name of teh service not the oepration!! The value between {} is the namespace. If you do not want to write {http://&#8230;.} then add another tag **xmlns   **&#8211; **{http://www.webserviceX.NET/}CurrencyConvertor. **
  * portName &#8211; is the name of the port.

**portName={http://www.webserviceX.NET/}CurrencyConvertorSoap. **This is again preceded by {http://&#8230;} which is the namespace value. This value is defined in the wsdl as &#8211;**<wsdl:port name=&#8221;CurrencyConvertorSoap&#8221; binding=&#8221;tns:CurrencyConvertorSoap&#8221;>**

The last piece is **dataFormat ** &#8211; **dataFormat=MESSAGE. **This tells that the body is of type message.

**Part 2** &#8211; In production you would want to avoid writing cxf in the above format as it is prone to error because the string value is very long and difficult to test independently and cannot be reused if you want to call the service in another route. So the best way is to define this as cxf endpoint. All you need to do is slighly modify the **camel-context.xml. **

  1. Add this(be sure to remove the earlier version of <to uri=&#8221;cxf&#8230;.&#8221;)

**<to uri=&#8221;cxf:bean:wsdlEndpoint?dataFormat=MESSAGE&#8221;/>**

  1. Define the cxf endpoint called **wsdlEndpoint** (You call it whatever you want).

**<cxf:<span class="hiddenSpellError">cxfEndpoint id=&#8221;wsdlEndpoint&#8221;</span>**

**                     address=&#8221;http://www.webservicex.net/CurrencyConvertor.asmx&#8221;**

**                     endpointName=&#8221;c:SOAPOverHTTP&#8221;**

**                     serviceName=&#8221;c:CurrencyConvertor&#8221;**

**                     xmlns:s=&#8221;http://www.webserviceX.NET&#8221;/>**

That&#8217;s it.

Now just run the app. This will print the following-

> [ead #0 &#8211; file://src/data/order] route1                         INFO

<soapenv:Header/>

<soapenv:Body>

<web:ConversionRate>

<web:FromCurrency>AUD</web:FromCurrency>

<web:ToCurrency>USD</web:ToCurrency>

</web:ConversionRate>

<!&#8211;<span class="hiddenSpellError">soapenv</span>:Body>&#8211;>

<!&#8211;<span class="hiddenSpellError">soapenv</span>:Envelope>&#8211;>

[           default-workqueue-1] route1                         INFO  <!--?xml version="1.0" encoding="utf-8"?-->0.8951

~~~~ Enjoy Cameling &#8230;.