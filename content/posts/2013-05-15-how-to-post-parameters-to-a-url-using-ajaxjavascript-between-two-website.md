---
title: How to post parameters to a url using Ajax/Javascript between two website
author: Dinesh
type: post
date: 2013-05-15T03:33:28+00:00
url: /2013/05/15/how-to-post-parameters-to-a-url-using-ajaxjavascript-between-two-website/
publicize_twitter_user:
  - dinesh19aug
  - dinesh19aug
dsq_thread_id:
  - 5442813266
  - 5442813266
categories:
  - Tech Notes

---
<p style="color: #000088; text-align: left;" align="left">
  <span style="color: black; font-family: Helvetica; font-size: 14pt;">I am working a new project and I recently ran into an interesting problem. One of the web site that I keep up at work was supposed to take the user to </span><span style="color: black; font-family: Helvetica; font-size: 14pt;">another website which required me to add post parameters.</span>
</p>

<span style="color: black; font-family: Helvetica; font-size: 14pt;">EX &#8211; www.mywebsite.makeapayment.com ==> Collects Billing information ex &#8211; name, amount, address etc.==> Post this information to www.vendor-website.com.</span>

<span style="font-family: Helvetica; font-size: 14pt;">I did not realize the problem until I started coding and my colleague pointed out that as soon as www.mywebsite.makeapayment.com goes to my servlet, the servlet will not pass params to external web site if use &#8220;POST&#8221;, I had to use &#8220;GET&#8221; because servlet will look up relative path only and the <strong>HTTPServletRequest/Response</strong> object is specific to an application. So if I wanted to send parameters using servlet I could only that using action = GET. Now since I was passing sensitive information so I did not want to use GET.</span>

<span style="font-family: Helvetica; font-size: 14pt;">A couple of solutions were discussed as follows:</span>

<span style="font-family: Helvetica; font-size: 14pt;">1. Insert the params in database and use servlet get from the mywebsite.com to pass the primary key of the database. Ex &#8211; www.mywebsite.makeapayment.com ==>  www.vendor-website.com?key=10001. The vendor application look up the required params from the database.</span>

<span style="font-family: Helvetica; font-size: 14pt;">2. Create a new JSP and use JavaScript onLoad() to pass the params as Hidden Input and submit as post to  www.vendor-website.com.</span>

<span style="font-family: Helvetica; font-size: 14pt;">Ex &#8211; www.mywebsite.makeapayment.com==> Servlet==> New Blank JSP with Hidden params loaded on onLoad() and submitted to vendor website ==> www.vendor-website.com.</span>

<span style="font-family: Helvetica; font-size: 14pt;">3. Third approach is interesting and I had not tried this ever but looked promising and this is what I eventually implemented. Make an Ajax call to from the JSP page to your servlet and when the Ajax Call returns, post it to vendor web site.</span>

<span style="font-family: Helvetica; font-size: 14pt;">Ex &#8211; www.mywebsite.makeapayment.com on hitting submit==> calls the JS, uses DWR to post to call the servlet==> Servlet does back ground processing like saving the records etc ==> Returns the control back to the JavaScript ==> Upon return in Ajax Call ==> Post to <span style="color: black;">www.vendor-website.com.</span></span>

<span style="font-family: Helvetica; font-size: 14pt;">I implemented the combination of one and three but here I am going to show you how post params to a different URL &#8211; i.e. solution 3</span>

<span style="font-family: Helvetica; font-size: 14pt;">Let&#8217;s say I have a submit form with Name and address which needs to be saved in database when I submit the form and then I need to post the same information to different web site.</span>

<span style="font-size: 14pt;"><span style="font-family: Helvetica;"><strong>PersonalInformation.jsp</strong></span></span>

<span style="color: red; font-family: cursive; font-size: 12pt;"><html></span>

<span style="color: red; font-family: cursive; font-size: 12pt;"><head></span>

> <span style="color: red; font-family: cursive; font-size: 12pt;">    <script></span>
> 
> <span style="color: red; font-family: cursive; font-size: 12pt;">       // I am not showing the code for DWR. You will need to include dwr and engine.js. Add dwr.xml in your web-inf and specify the class name and method you want to use as dwr call. This method is called in the dwr Ajax call back.</span>
> 
> <span style="font-size: 12pt;"><span style="font-family: cursive;"><span style="color: red;"><br /> function submitAndGoToVendorSite()<br /> {<br /> var form = document.createElement(&#8220;FORM&#8221;);<br /> form.method = &#8220;POST&#8221;;<br /> form.style.display = &#8220;none&#8221;;<br /> document.body.appendChild(form);<br /> var url=&#8221;www.vendor-website.com&#8221;;<br /> form.action = url;</span></span></span>
> 
> <span style="color: red; font-family: cursive; font-size: 12pt;">            //My dwr ajax call gets a Json string from the servlet response.<br /> var jsonString =      &#8216;{&#8220;transactionId&#8221;:&#8221;1368505156670&#8243;,&#8221;requesterType&#8221;:&#8221;APP&#8221;,&#8221;billingEmail&#8221;:&#8221;null@cybersource.com&#8221;,&#8221;billingState&#8221;:&#8221;NC&#8221;,&#8221;amount&#8221;:&#8221;42.7699999999999999433786257441170164384&#8243;,&#8221;refund&#8221;:&#8221;N&#8221;,&#8221;billingCity&#8221;:&#8221;CONCORD&#8221;,&#8221;billingLine1&#8243;:&#8221;Progress Pl&#8221;,&#8221;billingFirstname&#8221;:&#8221;test&#8221;,&#8221;billingLine2&#8243;:&#8221;&#8221;,&#8221;shopperIP&#8221;:&#8221;127.0.0.1&#8243;,&#8221;application&#8221;:&#8221;OEP2&#8243;,&#8221;currencyCode&#8221;:&#8221;USD&#8221;,&#8221;billingCompany&#8221;:&#8221;ACN&#8221;,&#8221;revenueSource&#8221;:&#8221;&#8221;,&#8221;billingLastname&#8221;:&#8221;test&#8221;,&#8221;countryCode&#8221;:&#8221;US&#8221;,&#8221;billingAddrNum&#8221;:&#8221;1000&#8243;,&#8221;cardType&#8221;:&#8221;VISA&#8221;,&#8221;businessPurpose&#8221;:&#8221;TOOL&#8221;,&#8221;profileConfig&#8221;:&#8221;cybersource-MLTEST1&#8243;,&#8221;language&#8221;:&#8221;en&#8221;,&#8221;billingZip&#8221;:&#8221;28025&#8243;,&#8221;repOrCustID&#8221;:&#8221;1233836&#8243;,&#8221;user&#8221;:&#8221;DARORATEST&#8221;,&#8221;paymentMethod&#8221;:&#8221;CC&#8221;,&#8221;billingPhone&#8221;:&#8221;&#8221;}&#8217;<br /> </span>
> 
> <span style="color: red; font-family: cursive; font-size: 12pt;">     // Create a JSON object from the JSON String</span>
> 
> <span style="color: red; font-family: cursive; font-size: 12pt;">     var jsonObj = jQuery.parseJSON(jsonString);</span>
> 
> <span style="color: red; font-family: cursive; font-size: 12pt;">//Iterate over Json object and set them as hidden input params to the form<br /> for(obj in jsonObj){<br /> var input = document.createElement(&#8220;INPUT&#8221;);<br /> input.type = &#8220;hidden&#8221;;<br /> input.name = obj;<br /> input.value = jsonObj[obj];<br /> form.appendChild(input);<br /> } </span>
> 
> //Submit the form
  
> form.submit();
> 
> <span style="color: red; font-family: cursive; font-size: 12pt;">}<br /> </script></span>

<span style="font-family: Helvetica; font-size: 14pt;"></head></span>

<span style="font-family: Helvetica; font-size: 14pt;"><body></span>

<span style="font-family: Helvetica; font-size: 14pt;">     <form></span>

<span style="font-family: Helvetica; font-size: 14pt;">            <label>Name:</label><Input type=&#8221;text&#8221;/></span>

<span style="font-family: Helvetica; font-size: 14pt;">            &#8230;&#8230;&#8230;.</span>

<span style="font-family: Helvetica; font-size: 14pt;">            <input type=&#8221;button&#8221; onclick=&#8221;submitAndGoToVendorSite();&#8221;/></span>

<span style="font-family: Helvetica; font-size: 14pt;">    </form></span>

<span style="font-family: Helvetica; font-size: 14pt;"></body></span>

<span style="font-family: Helvetica; font-size: 14pt;">That&#8217;s It!</span>

<span style="font-family: Helvetica; font-size: 14pt;">~Keep Coding</span>