---
title: 13 Most Common Java Keytool Keystore Commands
author: Dinesh
type: post
date: 2014-03-16T04:41:03+00:00
url: /2014/03/16/13-common-java-keytool-keystore-commands/
dsq_thread_id:
  - 5453580475
  - 5453580475
categories:
  - Tech Notes

---
I was working on a project last month where I had to call a third-party web service. The third-party web service wanted me to add a SSL keystore and I struggled. I could have gone to my UNIX Admin and asked him to do this job but decided to learn about all about keystores. I went through couple of forums and <a title="SO" href="http://stackoverflow.com" target="_blank">SO</a> and ended my spending 2 &#8211; 3 hours reading about keystores and commonly used commands.

To give you a quick run here what I was doing. I had to use a third party wsdl to create a client. I tried to use Maven jaxws plugin to generate the client. I downloaded the wsdl to my local machine and was able to successfully create a client. For production I wanted to generate the client using the current wsdl so decided to generate the client using the wsdl url of the third-party website but ran into keystore issue. I had to download their certificate and add it to my CACERT.

The whole charade led me to compile this post. Before I begin here is a quick run through Keystore

**Why Do I need a keystore?**

_By using a public/private key mechanism. This provides a layer of security that prevents, among other things, remote attackers from pushing malicious updates to your application  (all updates must be signed with the same key)_

**What is a Java Keytool?**

_It is a key and certificate management utility. It **allows users to manage their own public/private key pairs and certificates**. It also allows users to cache certificates. Java Keytool stores the keys and certificates in keystore. It protects private keys with a password. A Keytool keystore has the private key and any certificates necessary to complete a chain of trust and set up the trustworthiness of the primary certificate._

_Each certificate in a Java keystore is associated with a unique alias. When creating a Java keystore you will first create the .jks file that will initially only contain the private key. You will then generate a CSR and have a certificate generated from it. Then you will import the certificate to the keystore including any root certificates. _

#### **Here is a list of 13 most common commands**

##### <span style="color: #339966;"><strong>CREATING AND IMPORTING COMMANDS</strong></span>

**1. Create a Java Keystore and value pair**

> keytool -genkey -alias <span style="text-decoration: underline;">yourDomainName</span> -keyalg RSA -keystore <span style="text-decoration: underline;">Your</span><span style="text-decoration: underline;">keystoreName.jks </span>

**2. Creating a signing request (CSR) for an existing keystore**

> keytool -certreq -alias <span style="text-decoration: underline;">yourDomainName</span> -keystore <span style="text-decoration: underline;">keystore.jks</span> -file <span style="text-decoration: underline;">yourDomainName</span><span style="text-decoration: underline;">.csr</span>

**3. Importing a signed primary certificate to an existing  keystore****
  
** 

> keytool -import -trustcacerts -alias <span style="text-decoration: underline;">yourDomainName</span> -file <span style="text-decoration: underline;">yourDomainName</span>.crt -keystore <span style="text-decoration: underline;">YourkeystoreName</span>.jks

**4. Importing a root or intermediate CA certificate to an existing  keystore**

> keytool -import -trustcacerts -alias root -file Thawte.crt -keystore <span style="text-decoration: underline;">YourkeystoreName</span>.jks

**5. Creating a keystore and self-signed certificate**

> keytool -genkey -keyalg RSA -alias selfsigned -keystore Yourkeystore.jks -storepass password -validity 360

##### <span style="color: #339966;"><strong>CHECKING COMMANDS</strong></span>

When you need to check the information about a certificate or keystore then you use these commands.

<strong style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;">6. Checking a particular certificate</strong><strong style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;"><br /> </strong>

> keytool -printcert -v -file <span style="text-decoration: underline;">Your</span><span style="text-decoration: underline;">domain.crt</span>

<strong style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;">7. Checking all certificates in a keystore</strong>

> keytool -list -v -keystore <span style="text-decoration: underline;">Your</span><span style="text-decoration: underline;">keystore.jks</span>

<strong style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;">9. Checking a particular keystore entry using an alias</strong>

> keytool -list -v -keystore <span style="text-decoration: underline;">Your</span><span style="text-decoration: underline;">keystore.jks</span> -alias Yourdomain

##### **<span style="color: #339966;">EDIT/IMPORT COMMANDS</span>**

<strong style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;">10. Deleting a certificate from a keystore</strong>

> keytool -delete -alias <span style="text-decoration: underline;">Yourdomain</span> -keystore <span style="text-decoration: underline;">Your</span><span style="text-decoration: underline;">keystore.jks</span>

<strong style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;">11. Changing a keystore password</strong>

> keytool -storepasswd -new new_password -keystore <span style="text-decoration: underline;">keystore.jks</span>

<strong style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;">12. Exporting a certificate from a keystore</strong>

> keytool -export -alias <span style="text-decoration: underline;">Yourdomain</span> -file <span style="text-decoration: underline;">Yourdomain.crt</span> -keystore Your<span style="text-decoration: underline;">keystore.jks</span>

<strong style="font-family: sans-serif; font-size: medium; font-style: normal; font-variant: normal; line-height: normal;">13. Listing Trusted CA Certs</strong>

> keytool -list -v -keystore $JAVA_HOME/jre/lib/security/cacerts

> _**P.S. – If you liked the post please click on one of the ads in the right hand column to help me keep up this site and do drop a me a line to suggest some topics that would like to see on this site.**_

So Long &#8230;&#8230;