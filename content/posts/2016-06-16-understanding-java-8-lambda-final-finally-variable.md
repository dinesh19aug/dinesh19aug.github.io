---
title: Understanding Java 8 Lambda final finally variable
author: Dinesh
type: post
date: 2016-06-16T01:19:10+00:00
url: /2016/06/16/understanding-java-8-lambda-final-finally-variable/
snap_MYURL:
  - 
  - 
snapEdIT:
  - 1
  - 1
snapDL:
  - 's:263:"a:1:{i:0;a:9:{s:4:"doDL";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0dl";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:2:"do";s:1:"1";s:10:"msgTFormat";s:7:"%TITLE%";s:9:"msgFormat";s:9:"%EXCERPT%";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";}}";'
  - 's:263:"a:1:{i:0;a:9:{s:4:"doDL";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0dl";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:2:"do";s:1:"1";s:10:"msgTFormat";s:7:"%TITLE%";s:9:"msgFormat";s:9:"%EXCERPT%";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";}}";'
snapFB:
  - 's:332:"a:1:{i:0;a:11:{s:4:"doFB";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0fb";s:8:"postType";s:1:"I";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:2:"do";s:1:"1";s:11:"isPrePosted";s:1:"1";}}";'
  - 's:332:"a:1:{i:0;a:11:{s:4:"doFB";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0fb";s:8:"postType";s:1:"I";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:51:"New post (%TITLE%) has been published on %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:2:"do";s:1:"1";s:11:"isPrePosted";s:1:"1";}}";'
snapLI:
  - 's:342:"a:1:{i:0;a:11:{s:4:"doLI";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0li";s:8:"postType";s:1:"A";s:10:"SNAPformat";s:41:"New post has been published on %SITENAME%";s:12:"liMsgFormatT";s:18:"New Post - %TITLE%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:2:"do";s:1:"1";s:11:"isPrePosted";s:1:"1";}}";'
  - 's:342:"a:1:{i:0;a:11:{s:4:"doLI";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0li";s:8:"postType";s:1:"A";s:10:"SNAPformat";s:41:"New post has been published on %SITENAME%";s:12:"liMsgFormatT";s:18:"New Post - %TITLE%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";s:2:"do";s:1:"1";s:11:"isPrePosted";s:1:"1";}}";'
snap_isAutoPosted:
  - 1
  - 1
snapDI:
  - 's:339:"a:1:{i:0;a:12:{s:4:"doDI";s:1:"1";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:2:"do";s:1:"1";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:2:"DI";s:5:"pDate";s:19:"2016-06-16 01:19:20";s:10:"msgTFormat";s:7:"%TITLE%";s:9:"msgFormat";s:9:"%EXCERPT%";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";}}";'
  - 's:339:"a:1:{i:0;a:12:{s:4:"doDI";s:1:"1";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:2:"do";s:1:"1";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:2:"DI";s:5:"pDate";s:19:"2016-06-16 01:19:20";s:10:"msgTFormat";s:7:"%TITLE%";s:9:"msgFormat";s:9:"%EXCERPT%";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";}}";'
snapTW:
  - 's:289:"a:1:{i:0;a:10:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"1";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:2:"do";s:1:"1";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"743251585157849089";s:5:"pDate";s:19:"2016-06-16 01:19:21";}}";'
  - 's:289:"a:1:{i:0;a:10:{s:4:"doTW";s:1:"1";s:10:"SNAPformat";s:15:"%TITLE% - %URL%";s:8:"attchImg";s:1:"1";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:2:"do";s:1:"1";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:18:"743251585157849089";s:5:"pDate";s:19:"2016-06-16 01:19:21";}}";'
snapIP:
  - 's:269:"a:1:{i:0;a:9:{s:4:"doIP";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0ip";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:2:"do";s:1:"1";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:9:"736604272";s:5:"pDate";s:19:"2016-06-16 01:24:39";}}";'
  - 's:269:"a:1:{i:0;a:9:{s:4:"doIP";s:1:"1";s:12:"rpstPostIncl";s:7:"nxsi0ip";s:11:"SNAPformatT";s:7:"%TITLE%";s:10:"SNAPformat";s:9:"%EXCERPT%";s:2:"do";s:1:"1";s:11:"isPrePosted";s:1:"1";s:8:"isPosted";s:1:"1";s:4:"pgID";s:9:"736604272";s:5:"pDate";s:19:"2016-06-16 01:24:39";}}";'
dsq_thread_id:
  - 5292097524
  - 5292097524
categories:
  - Tech Notes

---
I am a little late to the java 8 party and was trying to quickly get some hands on with lambdas and ran into an issue where I got the error message <span style="color: #ff0000;"><br /> </span>

#### Variables used in lambda should be final or effectively final

&nbsp;

. I know what final is but what is effectively final.

Here is what I was trying to do. I had a HashMap which had values like &#8220;one : 1&#8221;, &#8220;two : 2&#8221;, &#8220;three : 3&#8221; and wanted to replace the String ${one} with 1 etc.

> <pre><strong>    public String evaluate(HashMap&lt;String, String&gt; variables){
       String result = "${One}, ${two}, ${three}";
       variables.forEach((k,v)-&gt;{
          String regex = "\\$\\{" + k + "\\}";
          result=result.replaceAll(regex, v);
       });
       return result;
    }
</strong></pre>

When I assigned result=result.replaceAll(regex, v); I got the error message &#8211;

#### <span style="color: #ff0000;">Variables used in lambda should be final or effectively final</span>

. On further research using SO forums and blog I learned that Java 8 has new concept called &#8220;Effectively final&#8221; variable. It means that a non-final local variable whose value never changes after initialization is called &#8220;Effectively Final&#8221;. This concept was introduced because prior to Java 8 we could not use a non-final local variable in an anonymous class. If you have access to a local variable in Anonymous class, you have to make it final.

When Lambdas was introduced, this restriction was eased. Hence to the need to make local variable final if it&#8217;s not changed once it is initialized as Lambda in itself is nothing but an anonymous class. Java 8 realized the pain of declaring local variable final every time developer used Lambda and introduced this concept and made it unnecessary to make local variables final. So if you see the rule for anonymous class still not changed, it&#8217;s just you don&#8217;t have to write final keyword every time when using lambdas.

OK. So now I understand what the error means but how do I solve my issue where I want to replace the variables using regex. Surprisingly, before I looked up
  
documentation and SO forums, I checked the options suggested by IntelliJ. It said &#8211; &#8220;Transform result variable into final one element array&#8221;. As I clicked continue, My code transformed to

> <pre><strong>    public String evaluate(){
       final String[] result = {"${One}, ${two}, ${three}"};

       variables.forEach((k,v)-&gt;{
          String regex = "\\$\\{" + k + "\\}";
          result[0] = result[0].replaceAll(regex, v);
       });
       return result[0];
   }
</strong></pre>

Now what the heck just happened? Why is a String not allowed to change but an Array is allowed to change? Going back to basics of Java I realized that when we decalre a variable final, it is the reference to the object that is set to final. So in this case when I write

##### final String result= &#8220;abc&#8221;;

The reference is <span style="text-decoration: underline;">STRING OBJECT</span> **<span style="color: #ff0000;">result &#8212;memory location &#8212;> &#8220;abc&#8221;</span>** and because the result is declared final, it cannot change the memory reference and point to memory location who value is say<span style="color: #ff0000;"><strong> &#8221; DEF&#8221;</strong></span>.

When I write

##### final String [] result = {&#8220;abc&#8221;}

In this case, result is pointing to a reference that is a Array and that array has value that reference <span style="text-decoration: underline;"><strong>memory location</strong></span> of <span style="text-decoration: underline; color: #ff0000;"><strong>String &#8220;abc&#8221;</strong></span>.
  
<span style="text-decoration: underline; color: #ff0000;"><strong>FINAL STRING [] result &#8212;- Memory location &#8211;> Single Array &#8212;&#8211;Memory location &#8212;> &#8220;abc&#8221;.</strong></span>
  
So as you see our result now references the memory location of Array element but the value Array element can change. Remember what is constant here is the reference, <span style="text-decoration: underline;"><strong>not</strong></span> its values.

&nbsp;

~~ Smell the Java ~~

Dinesh