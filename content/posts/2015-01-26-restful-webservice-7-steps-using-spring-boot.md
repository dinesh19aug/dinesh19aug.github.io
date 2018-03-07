---
title: Restful Webservice in 7 Steps using Spring boot
author: Dinesh
type: post
date: 2015-01-26T20:59:12+00:00
url: /2015/01/26/restful-webservice-7-steps-using-spring-boot/
snap_MYURL:
  - 
  - 
snapEdIT:
  - 1
  - 1
snapDI:
  - 's:119:"a:1:{i:0;a:4:{s:4:"doDI";s:1:"1";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:2:"do";s:1:"1";}}";'
  - 's:119:"a:1:{i:0;a:4:{s:4:"doDI";s:1:"1";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:2:"do";s:1:"1";}}";'
snapDL:
  - 's:147:"a:1:{i:0;a:5:{s:4:"doDL";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:2:"do";s:1:"1";}}";'
  - 's:147:"a:1:{i:0;a:5:{s:4:"doDL";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:2:"do";s:1:"1";}}";'
snapFB:
  - 's:299:"a:1:{i:0;a:10:{s:4:"doFB";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:8:"postType";s:1:"I";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:2:"do";s:1:"1";}}";'
  - 's:299:"a:1:{i:0;a:10:{s:4:"doFB";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:8:"postType";s:1:"I";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:2:"do";s:1:"1";}}";'
snapLI:
  - 's:380:"a:1:{i:0;a:12:{s:4:"doLI";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:41:"New post has been published on %SITENAME%";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:8:"postType";s:1:"A";s:12:"liMsgFormatT";s:18:"New Post - %TITLE%";s:2:"do";s:1:"1";}}";'
  - 's:380:"a:1:{i:0;a:12:{s:4:"doLI";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:41:"New post has been published on %SITENAME%";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:8:"postType";s:1:"A";s:12:"liMsgFormatT";s:18:"New Post - %TITLE%";s:2:"do";s:1:"1";}}";'
snapIP:
  - 's:269:"a:1:{i:0;a:9:{s:4:"doIP";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0ip";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:9:"586505097";s:5:"pDate";s:19:"2015-06-22 00:44:33";s:2:"do";s:1:"1";}}";'
  - 's:269:"a:1:{i:0;a:9:{s:4:"doIP";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0ip";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:9:"586505097";s:5:"pDate";s:19:"2015-06-22 00:44:33";s:2:"do";s:1:"1";}}";'
snapTW:
  - 's:162:"a:1:{i:0;a:6:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"1";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:2:"do";s:1:"1";}}";'
  - 's:162:"a:1:{i:0;a:6:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"1";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:2:"do";s:1:"1";}}";'
dsq_thread_id:
  - 5451332046
  - 5451332046
categories:
  - Tech Notes

---
Last week I was working on a new application which required me to build a web service to access it&#8217;s functionality. I decided to check out Spring 4 RestController.

I was amazed at how far we have come from writing all the boiler template code, xmls etc for making a restful call. With Spring4 boot, it was matter of adding simple annotation for RestController.
  
I will be honest, I have not been up to date on how to use a Restful webservice, I built a couple of Restful service a couple of year ago, but most of the services in my current project are old school (SOAP calls), so I never got a chance to build one from scratch and at peace.

Prerequisites: Read Carefully
  
1. Spring 4 requires you to use Maven 3 in fact it will force you to use Maven 3. This is very important point because it took me an hour to figure this out. If you try to use Maven 2, it will build and &#8220;might&#8221; compile but the code will complain that some of the RestController class methods are not found. This happens because by default, maven 2 will pull in Spring 2.5.x jar files.
  
2. Requires a minimum of JDK 6.

**What are we building?**
  
We will build a service that will accept HTTP GET request at: http://localhost:9000/welcome

and respond with a JSON message:

`{"content":"Hello Dinesh"}`

**Step 1**: Create a maven project using command line tools or your favorite IDE.

**Step 2**: In the pom.xml add the following information
  
**a) Parent:**

<p id="FFoDXdm">
  <img class="alignnone size-full wp-image-753 " src="http://www.javahabit.com/wp-content/uploads/2015/01/img_54c6997a2d5aa.png" alt="" />
</p>

b) Add spring-boot dependency

<p id="HbeyzUj">
  <img class="alignnone size-full wp-image-754 " src="http://www.javahabit.com/wp-content/uploads/2015/01/img_54c6999bd1865.png" alt="" />
</p>

c) Add spring-boot plugin

<p id="TzgpLxK">
  <img class="alignnone size-full wp-image-755 " src="http://www.javahabit.com/wp-content/uploads/2015/01/img_54c699bb563e9.png" alt="" />
</p>

d) Add spring repositories

<p id="dPDyzsX">
  <img class="alignnone size-full wp-image-756 " src="http://www.javahabit.com/wp-content/uploads/2015/01/img_54c699d20f4f9.png" alt="" />
</p>

**Why do we need Spring Boot Maven Plugin?**
  
You might be wondering what happened to the good old maven build plugin. Well that plugin still works and will compile and build your project, but Spring-boot-maven-plugin searches for the public static void main() method to mark it as runnable class if you use the command &#8220;mvn:run&#8221;. Secondly, it comes with its own dependency resolver for the version number to match the Spring-boot-starter-web dependencies.

**Step 3:** Create JSON Message POJO class

> src/main/java/dinesh/Welcome.java

<pre class="lang:java decode:true "><code>
package dinesh;
public class Welcome {

   private final String content;

   public Greeting(String content) {
      this.content = content;
   }

   public String getContent() {
     return content;
  }
}
</code></pre>

&nbsp;

Note: Spring 4 Boot automatically uses Jackson JSON library to marshal instances of Welcome into JSONObjects.

**Step 4:** Create a resource Controller
  
All Spring HTTP requests are handled by Spring controllers. For Restful services Spring 4 comes with a new annotation @RestController annotation. This will handle the requests which are posted to url **/welcome** by returning a new instance of Welcome class.

src/main/java/dinesh/WelcomeController.java

<pre class="scroll:true lang:java decode:true"><code>
package hello;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class WelcomeController {

   private static final String template = "Hello, %s!";

   @RequestMapping("/welcome")
   public Welcome welcome(@RequestParam(value="name", defaultValue="World") String name) {
      return new Greeting(String.format(template, name));
   }
}
</code>
</pre>

&nbsp;

If you look closely, you will know why I said Maven 2 will not work. Maven 2 will pull in RequestParm class from old Springmvc jar file which does not have method defined for defaultValue(). It is going cry out loud during compilation.
  
@RestController &#8211; annotation marks the class as controller where every method returns a domain object instead of a view, which is major distinction between @Controller and @RestController which is a short hand for @Controller + @ResponseBody
  
The @RequestMapping annotation helps Spring to identify what method to invoke when some one accesses &#8220;/welcome&#8221; url.
  
The @RequestParam binds the value of paramter &#8220;name&#8221; into the name parameter of the welcome() method. If you do not pass any value in the query string then the default value is &#8220;world&#8221; &#8211; defaultValue=&#8221;World&#8221;. If you do not add defaultValue and forget to pass a &#8220;name=xx&#8221; in the query string, you will hear a loud cracking, lots of smokes, some curses and code will complain of NP exceptions :-).

One important thing that you notice is that we have not done anything to marshall request/response as JSONobject. The old of way of doing this would need you to use Jackson libraries and a lot of annotation to make them as JSON properties. Thanks to Spring 4, it takes of it using Jackson dependencies in the background.

**Step 5:** Create an executable &#8220;jar&#8221; file. yes you read it right. Although you can create a war file, for smaller project like the one I build and the one for this example, I am not going to go through those steps. you cn check the Spring documentation on this topic. Just a high level view what is required is that you get right of the boot plugin, change the packaging tag in the pom.xml to war.Here&#8217;s a good <a href="http://spring.io/blog/2014/03/07/deploying-spring-boot-applications" target="_blank">post </a>

> src/main/java/dinesh/Execute.java

    
    package dinesh;
    import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
    import org.springframework.boot.SpringApplication;
    import org.springframework.context.annotation.ComponentScan;
    
    @ComponentScan(basePackages = "dinesh.*")
    @EnableAutoConfiguration
    public class Execute {
    
       public static void main(String[] args) {
         SpringApplication.run(Execute.class, args);
       }
    }

&nbsp;

&#8211; @ComponentScan tells the app to check for @component annotation and it makes sure that Spring finds and registers WelcomeController, because it is marked as &#8220;@RestController&#8221;.

**Step 6:** Build and run
  
** Method 1 :**
  
Run &#8216;mvn clean install&#8217; in the command line
  
After the jaris built, run

<pre class="lang:default decode:true">java -jar target/xxx.jar</pre>

**Method 2:**

<pre class="lang:default decode:true ">Run spring-boot:run</pre>

&nbsp;

Spring 4 comes with built-in Tomcat 7, so you do not need a full-blown JEE application server to deploy and run your web service. Either of the method will fire up the application on port 8080.

**How do I change port number?**
  
just run

<pre class="lang:default decode:true ">spring-boot:run -Dserver.port=9000</pre>

&nbsp;

**Step 7:** Test your service
  
Once the service is up, visit **http://localhost:8080/welcome?name=your-name** and you will get back a response
  
{&#8220;content&#8221;:&#8221;Hello, your-name!&#8221;}

&nbsp;

~Ciao