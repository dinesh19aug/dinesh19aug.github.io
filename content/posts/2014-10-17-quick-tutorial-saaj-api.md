---
title: A quick tutorial on SAAJ API
author: Dinesh
type: post
date: 2014-10-17T20:28:07+00:00
url: /2014/10/17/quick-tutorial-saaj-api/
dsq_thread_id:
  - 5442115090
  - 5442115090
categories:
  - Tech Notes

---
We ran into an issue last week. I had to call a third party web service that was built in PHP. Anyone who wokrs with Java will tell you that calling a web service is not more 15 minutes coding. You take the wsdl, run wsdl2Java command from Axis2 and start calling the service.

Like I said before, things are never so straightforward. No matter what version of Axis or CXF we used, we kept getting this error:

> Caused by: org.apache.axiom.soap.SOAPProcessingException: Transport level information does not match with SOAP Message namespace URI
  
> at org.apache.axis2.builder.BuilderUtil.validateSOAPVersion(BuilderUtil.java:772)
  
> at org.apache.axis2.builder.SOAPBuilder.processDocument(SOAPBuilder.java:58)
  
> at org.apache.axis2.transport.TransportUtils.createDocumentElement(TransportUtils.java:179)
  
> at org.apache.axis2.transport.TransportUtils.createSOAPMessage(TransportUtils.java:145)
  
> at org.apache.axis2.transport.TransportUtils.createSOAPMessage(TransportUtils.java:108)
  
> &#8230; 13 more

Now what this usually means is that client and server are using different version of SOAP(1.1 vs 1.2). For a long time my colleague tried to look for a solution on various forums, blogs etc. and everyone confirmed the same that the issue is at the service provider end. However, the same service was being used by 20 other vendors without an issue. Our Canada office reported that they were able to call the service without any issue albeit in PHP(OOPS!!).

One fine afternoon it just struck me that Axis, CXF etc. are nothing but a wrapper around Java&#8217;s SAAJ API. Imagine how did developers call services before Axis and CXF? They coded QNAME, SOAPMessage manually! Lo and Behold but I went down to &#8230; let&#8217;s call it low level programming because I had to write code for all the XML node element, define namespaces etc.. which was not fun at all.
  
So this tutorial will walk you through basics of SAAJ, how and when to use the SAAJ API.

**WHY DO I NEED SAAJ over AXIS2 or CXF?**
  
I so badly want to say that when you want to avoid the above error, use SAAJ :-). SAAJ is helpfule when you want complete control over SOAP elements. For example if you need to change name spaces or modify soap message attributes then SAAj comes in handy.

A typical SOAP message looks like this

<img class="alignnone size-full wp-image-743" src="http://javahabit.com/wp-content/uploads/2014/10/img_544163699fb361.png" alt="" />

As you can see SAAJ provides _SOAPMessage, SOAPHeader, SOAPBody_ classes to capture the message. When you create a new SOAPMessage object, it will automatically have the parts that are required to be in a SOAP message. In other words, a new SOAPMessage object has a SOAPPart object that contains a SOAPEnvelope object. The SOAPEnvelope object in turn automatically contains an empty SOAPHeader object followed by an empty SOAPBody object. If you do not need the SOAPHeader object, which is optional, you can delete it. The rationale for having it automatically included is that more often than not you will need it, so it is more convenient to have it provided. The SOAPHeader object may contain one or more headers with information about the sending and receiving parties. The SOAPBody object, which always follows the SOAPHeader object if there is one, provides a simple way to send information intended for the ultimate recipient. For example, if there is a SOAPFault object, it must be in the SOAPBody object.

So If have a service where I need the request SOAP Message should look like

> <soapenv:Envelope xmlns:soapenv=&#8221;http://schemas.xmlsoap.org/soap/envelope/&#8221; xmlns:urn=&#8221;urn:http://com.mycompany.IamDoingSomething&#8221;>
  
> <soapenv:Header/>
  
> <soapenv:Body>
  
> <urn:getPresaleByAddress>
  
> <stnum>123
  
> <stnumsuff></stnumsuff>
  
> <stnam>Forest</stnam>
  
> <sttyp>DR</sttyp>
  
> <stdir></stdir>
  
> <loctypa></loctypa>
  
> <locnuma></locnuma>
  
> <loctypb></loctypb>
  
> <locnumb></locnumb>
  
> <muni>OTTAWA</muni>
  
> <post>K1A1A1</post>
  
> <prov>on</prov>
  
> <!--<span class="hiddenSpellError" pre="" data-mce-bogus="1"-->urn:getPresaleByAddress>
> 
> 
  
> <!--<span class="hiddenSpellError" pre="" data-mce-bogus="1"-->soapenv:Body>
> 
> 
  
> <!--<span class="hiddenSpellError" pre="" data-mce-bogus="1"-->soapenv:Envelope>

and I need to send this message to web service url &#8220;http://some-webservice-url.com&#8221;

**STEPS**

1. Create a SOAP Message

> MessageFactory factory = MessageFactory.newInstance();
  
> SOAPMessage message = factory.createMessage();

&nbsp;

Result:

> xmlns:SOAP-ENV=&#8221;http://schemas.xmlsoap.org/soap/envelope/&#8221;>
  
> <SOAP-ENV:Header/>
  
> <SOAP-ENV:Body/>
  
> </SOAP-ENV:Envelope>

2. Access Soap parts or message

> SOAPHeader header = message.getSOAPHeader();
  
> SOAPBody body = message.getSOAPBody();

&nbsp;

3. Add Message Content

>  SOAPBody body = message.getSOAPBody();
> 
> SOAPFactory soapFactory = SOAPFactory.newInstance();
  
> Name bodyName = soapFactory.createName(&#8220;getPresaleByAddress&#8221;,&#8221;urn&#8221;, &#8220;http://com.mycompany.IamDoingSomething&#8221;);
  
> SOAPBodyElement bodyElement = body.addBodyElement(bodyName);

Result:

> <urn:getPresaleByAddress>
> 
> &#8230;
> 
> <!--<span class="hiddenSpellError" pre="" data-mce-bogus="1"-->urn:getPresaleByAddress>

4. Add Message Headers namespaces if Any

> MimeHeaders headers = soapMessage.getMimeHeaders();
  
> headers.addHeader(&#8220;SOAPAction&#8221;, leonidUrl+ &#8220;/getPresaleByAddress&#8221;);
  
> SOAPPart soapPart = soapMessage.getSOAPPart();
  
> // SOAP Envelope
  
> SOAPEnvelope envelope = soapPart.getEnvelope();
  
> envelope.addNamespaceDeclaration(&#8220;urn&#8221;, &#8220;urn:http://com.mycompany.IamDoingSomething&#8221;);

&nbsp;

5. Add Basic Authentication if any

> String authorization = new sun.misc.BASE64Encoder().encode((&#8220;myUserName&#8221;+&#8221;:&#8221;+&#8221;myPassword&#8221;).getBytes());
  
> headers.addHeader(&#8220;Authorization&#8221;, &#8220;Basic &#8221; + authorization);

6. Add child elements

> QName bodyName = new QName(&#8220;urn:http://com.mycompany.IamDoingSomething&#8221;,&#8221;getPresaleByAddress&#8221;,&#8221;urn&#8221;) ;
  
> SOAPBodyElement bodyElement = body.addBodyElement(bodyName);
  
> QName node_name = new QName(qName);
  
> SOAPElement node_element = null;
  
> try {
  
> node_element = bodyElement.addChildElement(&#8220;stnum&#8221;);
  
> if(hasNodeValue){
  
> node_element.addTextNode(&#8220;123&#8221;);
  
> }
  
> }

Result:

> <stnum>123</stnum>

7. Get a Soap Connection Object

> SOAPConnectionFactory soapConnectionFactory = SOAPConnectionFactory.newInstance();
  
> SOAPConnection connection = soapConnectionFactory.createConnection();
> 
> &nbsp;

SOAP messages are sent and received over a connection. This connection is represented by a SOAPConnection object, which goes from the sender directly to its destination. This kind of connection is called a point-to-point connection because it goes from one endpoint to another endpoint. Messages sent using the SAAJ API are called request-response messages. They are sent over a SOAPConnection object with the method call, which sends a message (a request) and then blocks until it receives the reply (a response).

8. Send the message

> // Create an endpoint point which is either URL or String type
  
> java.net.URL endpoint = new URL(&#8220;http://some-webservice-url.com&#8221;);
> 
> // Send a SOAPMessage (request) and then wait for SOAPMessage (response)
  
> SOAPMessage response = connection.call(message, endpoint);

9. Print the SOAP Response XML

> Transformer transformer = transformerFactory.newTransformer();
  
> Source sourceContent = response.getSOAPPart().getContent();
  
> ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
  
> StreamResult result = new StreamResult(outputStream);
  
> transformer.transform(sourceContent, result);
  
> log.info(&#8220;nResponse SOAP Message ::n {}&#8221; , result.getOutputStream().toString());

That&#8217;s it!!

There are many other things that you can do with SAAJ. To read more about SAAJ and it&#8217;s capabilities you can read <a title="here" href="http://docs.oracle.com/javaee/5/tutorial/doc/bnbhg.html" target="_blank">here</a> and <a title="here" href="http://java.boot.by/wsd-guide/ch05s04.html" target="_blank">here</a>

&nbsp;

~Ciao

&nbsp;

&nbsp;

&nbsp;

&nbsp;