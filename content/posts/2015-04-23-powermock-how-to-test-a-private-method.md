---
title: 'PowerMock : How to test a private method'
author: Dinesh
type: post
date: 2015-04-23T20:49:08+00:00
url: /2015/04/23/powermock-how-to-test-a-private-method/
snap_MYURL:
  - 
  - 
snapEdIT:
  - 1
  - 1
snap_isAutoPosted:
  - 1
  - 1
snapLI:
  - 's:568:"a:1:{i:0;a:14:{s:4:"doLI";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:41:"New post has been published on %SITENAME%";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:19:"5997108793043931136";s:7:"postURL";s:124:"https://www.linkedin.com/updates?discuss=&amp;scope=20656194&amp;stype=M&amp;topic=5997108793043931136&amp;type=U&amp;a=qhz2";s:5:"pDate";s:19:"2015-04-23 20:49:17";}}";'
  - 's:568:"a:1:{i:0;a:14:{s:4:"doLI";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:10:"AttachPost";s:1:"1";s:10:"SNAPformat";s:41:"New post has been published on %SITENAME%";s:11:"SNAPformatT";s:18:"New Post - %TITLE%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:19:"5997108793043931136";s:7:"postURL";s:124:"https://www.linkedin.com/updates?discuss=&amp;scope=20656194&amp;stype=M&amp;topic=5997108793043931136&amp;type=U&amp;a=qhz2";s:5:"pDate";s:19:"2015-04-23 20:49:17";}}";'
snapDI:
  - 's:211:"a:1:{i:0;a:7:{s:4:"doDI";s:1:"1";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:2:"DI";s:5:"pDate";s:19:"2015-04-23 20:49:17";}}";'
  - 's:211:"a:1:{i:0;a:7:{s:4:"doDI";s:1:"1";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:2:"DI";s:5:"pDate";s:19:"2015-04-23 20:49:17";}}";'
snapFB:
  - 's:425:"a:1:{i:0;a:13:{s:4:"doFB";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:8:"postType";s:1:"I";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:35:"10153196955833698_10153255449203698";s:5:"pDate";s:19:"2015-04-23 20:49:24";}}";'
  - 's:425:"a:1:{i:0;a:13:{s:4:"doFB";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:8:"postType";s:1:"I";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:35:"10153196955833698_10153255449203698";s:5:"pDate";s:19:"2015-04-23 20:49:24";}}";'
snapIP:
  - 's:252:"a:1:{i:0;a:8:{s:4:"doIP";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0ip";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:9:"579799774";s:5:"pDate";s:19:"2015-07-12 20:38:31";}}";'
  - 's:252:"a:1:{i:0;a:8:{s:4:"doIP";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0ip";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:9:"579799774";s:5:"pDate";s:19:"2015-07-12 20:38:31";}}";'
snapDL:
  - 's:270:"a:1:{i:0;a:8:{s:4:"doDL";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:32:"29835bcf919a2df474f3981c369af64c";s:5:"pDate";s:19:"2015-04-23 20:49:27";}}";'
  - 's:270:"a:1:{i:0;a:8:{s:4:"doDL";s:1:"1";s:12:"rpstPostIncl";s:1:"0";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:32:"29835bcf919a2df474f3981c369af64c";s:5:"pDate";s:19:"2015-04-23 20:49:27";}}";'
dsq_thread_id:
  - 5441445511
  - 5441445511
categories:
  - Uncategorized

---
&#8220;I HAVE THE POWER!!&#8221; &#8211; I had this feeling a few days ago. I will be honest that at work I do not get time to write unit test cases for each and every piece of code that I write. Often when I do have time, I make an effort to write test cases even for the trivial piece of code blocks such as &#8212; Check if properties file is present.

I was working on new code where I had the luxury to write the code in peace (a rarity at my work place where every project is like a fire drill). While writing test cases I came across a situation where I had a class with two methods:

[java]
  
<pre>public void my\_public\_method()

private void my\_private\_method()
  
[/java]

&nbsp;

I wanted to write test cases for both the method. However Junit would not allow me to write a test case for a private method. I searched over internet forums and every one suggested that I use [**Java Reflection API**][1]  to write my test cases or make my private method public, which I did not want to do.

That’s when [**POWERMOCK**][2] steps in and in a tiny little section of its documentation I noticed a piece of &#8220;**WhiteboxImpl&#8221; ** class which can help me test private methods.

So that’s what I am going to demonstrate in this tutorial.

**STEP 1: Add Maven jar files**

[xml]
  
<properties>
      
<relative.path>relative/svn/path</relative.path>
        
<powermock.version>1.6.2</powermock.version>
    
</properties>
   
<dependencies>
  
&#8230;&#8230;..
        
<dependency>
            
<groupId>junit</groupId>
            
<artifactId>junit</artifactId>
            
<version>4.11</version>
            
<scope>test</scope>
        
</dependency>
        
<dependency>
            
<groupId>org.powermock</groupId>
            
<artifactId>powermock-module-junit4</artifactId>
            
<version>${powermock.version}</version>
            
<scope>test</scope>
        
</dependency>
        
<dependency>
            
<groupId>org.powermock</groupId>
            
<artifactId>powermock-api-easymock</artifactId>
            
<version>${powermock.version}</version>
            
<scope>test</scope>
        
</dependency>
   
<dependencies>
  
[/xml]

**STEP 2: Create a class MyClass.java**

&nbsp;

[java]</pre>
  
<pre>public class MyClass {
      
//PUBLIC METHOD
      
public String my\_public\_method(){
          
String msg="This is my PUBLIC method";
          
System.out.println(msg);
          
return msg;
      
}

//PRIVATE METHOD
      
private String my\_private\_method(){
          
String msg="This is my PRIVATE method";
          
System.out.println(msg);
          
return msg;
      
}
  
}
  
[/java]

<pre></pre>

**STEP 3: Write a test case for public method : my\_public\_method**

[java]

import org.junit.Assert;
  
import org.junit.Test;
  
import org.junit.runner.RunWith;
  
import org.powermock.core.classloader.annotations.PrepareForTest;
  
import org.powermock.modules.junit4.PowerMockRunner;
  
import org.powermock.reflect.internal.WhiteboxImpl;

@RunWith(PowerMockRunner.class)
  
@PrepareForTest(MyClass.class)
  
public class MyClassTest {
      
final String publicMsg = "This is my PUBLIC method";
      
final String privateMsg = "This is my PRIVATE method";

@Test
      
public void testMy\_public\_method() throws Exception {
          
MyClass myClass = new MyClass();
          
String msg=myClass.my\_public\_method();
          
Assert.assertEquals(publicMsg,msg);
      
}
  
}

[/java]

As you can see above that there is no issue with calling a public method and it will run successfully but when you try and call the private method, the code will show error that private method is not visible.

<p id="OuLQhzO">
  <img class="alignnone size-full wp-image-822 " src="http://javahabit.com/wp-content/uploads/2015/04/img_553958b7cc7c8.png" alt="" />
</p>

**STEP 4: Use PowerMock’s WhiteboxImpl class to test a private method.**

Before you do anything you need to make sure that you added Powermock annotations correctly.

  * Add these two annotations to your class.

[java]

@RunWith(PowerMockRunner.class)

@PrepareForTest(MyClass.class)

[/java]

<p id="SoISpfk">
  <img class="alignnone size-full wp-image-823 " src="http://javahabit.com/wp-content/uploads/2015/04/img_5539592432353.png" alt="" />
</p>

  * Write the code to test private method.

[java]
      
@Test
      
public void testMy\_private\_method() throws Exception {
          
MyClass myClass = new MyClass();
          
String msg= WhiteboxImpl.invokeMethod(myClass, "my\_private\_method");
          
Assert.assertEquals(privateMsg,msg);
      
}
  
[/java]

The syntax is pretty simple **WhiteboxImpl.invokeMethod(<class object>, “<Name of the private Method>,input param1, input param2,…);**

The WhiteBoxImpl class actually uses “**Java Reflection API”** in the background to make a call, but for the lazy coders like me, who do not want to write **Reflection** **API**(_Read hate Reflection API_**),** the WhiteBoxImpl class is a small piece of coding heaven.

Now run the test class and you will see that test cases have passed.

<p id="igpZSqt">
  <img class="alignnone size-full wp-image-824 " src="http://javahabit.com/wp-content/uploads/2015/04/img_553959a17f30b.png" alt="" />
</p>

~Ciao –Repeat the mantra – “I HAVE THE POWER{MOCK}!!!”

&nbsp;

<pre></pre>

 [1]: https://docs.oracle.com/javase/tutorial/reflect/
 [2]: https://code.google.com/p/powermock/