---
title: How to configure JNDI with Spring and Jboss4/5
author: Dinesh
type: post
date: 2013-09-18T19:27:26+00:00
url: /2013/09/18/how-to-configure-jndi-with-spring-and-jboss45/
publicize_twitter_user:
  - dinesh19aug
  - dinesh19aug
dsq_thread_id:
  - 5447344056
  - 5447344056
categories:
  - Tech Notes

---
This is a simple process but if you try and search on the web you will come across various incomplete solutions which will leave you more confused than you already were. This configuration involves just four simple steps that I will walk through to help you set up JNDI on Jboss. I am using Jboss 4.3, but this should be valid for other version of Jboss as well.

I have a web application which is built on Spring 3.2 and uses Hibernate 4. To set up a new JNDI configuration we will first create a datasource xml file. This file needs to be deployed in Jboss/Deploy folder along with your war file.

<span style="text-decoration: underline;"><strong>Step 1:</strong></span>

Create a datasource file oracle-ds.xml. The content of the file will look like this

<span style="color: #008000;"><?xml version=&#8221;1.0&#8243; encoding=&#8221;UTF-8&#8243;?></span>

<span style="color: #008000;"><!DOCTYPE datasources PUBLIC &#8220;-//JBoss//DTD JBOSS JCA Config 1.5//EN&#8221; &#8220;http://www.jboss.org/j2ee/dtd/jboss-ds_1_5.dtd&#8221;></span>

<span style="color: #008000;"><datasources></span>

<span style="color: #008000;">  <local-tx-datasource></span>

<span style="color: #008000;">    <jndi-name><strong>jdbc/listener-dss</strong></jndi-name></span>

<span style="color: #008000;">    <connection-url>jdbc:oracle:thin:@dbsrvossdevl:1521:US91</connection-url></span>

<span style="color: #008000;">    <driver-class>oracle.jdbc.driver.OracleDriver</driver-class></span>

<span style="color: #008000;">    <user-name>myuser</user-name></span>

<span style="color: #008000;">    <password>mypassword</password></span>

<span style="color: #008000;">    <min-pool-size>5</min-pool-size></span>

<span style="color: #008000;">    <max-pool-size>50</max-pool-size></span>

<span style="color: #008000;">    <idle-timeout-minutes>10</idle-timeout-minutes></span>

<span style="color: #008000;">    <exception-sorter-class-name>org.jboss.resource.adapter.jdbc.vendor.OracleExceptionSorter</exception-sorter-class-name></span>

<span style="color: #008000;">    <metadata></span>

<span style="color: #008000;">      <type-mapping>Oracle9i</type-mapping></span>

<span style="color: #008000;">    </metadata></span>

<span style="color: #008000;">  </local-tx-datasource></span>

<span style="color: #008000;"></datasources></span>

&nbsp;

<span style="color: #000000;"><strong>Explanation:</strong> <jndi-name><strong style="color: #008000;">jdbc/listener-dss</strong></jndi-name> . This line tells what is the jndi name that we are going to use across configuration files.</span><span style="color: #008000;"><br /> </span>

&nbsp;

<span style="text-decoration: underline;"><strong><span style="color: #000000; text-decoration: underline;">Step</span></strong></span>** <span style="color: #000000;">2:</span>**<span style="color: #000000;"> Now open your web.xml file and add the resource-ref. This tells that jee container that your web application is using JNDI.</span>

<span style="color: #000000;">Your web.xml should be under <strong>WEB-INF</strong> folder. Add the below lines in your web.xml (<strong>see the highlighted section</strong>). This step is common whether you use Jboss or Tomcat or Websphere or any other application server.</span>

&nbsp;

<span style="color: #008000;"><?xml version=&#8221;1.0&#8243; encoding=&#8221;UTF-8&#8243;?></span>

<span style="color: #008000;"><web-app version=&#8221;2.5&#8243; xmlns=&#8221;http://java.sun.com/xml/ns/javaee&#8221; xmlns:xsi=&#8221;http://www.w3.org/2001/XMLSchema-instance&#8221;</span>

<span style="color: #008000;">  xsi:schemaLocation=&#8221;http://java.sun.com/xml/ns/javaee</span>

<span style="color: #008000;">  http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd&#8221;></span>

<span style="color: #008000;">  <display-name>ACN Web Application</display-name></span>

&nbsp;

<span style="color: #008000;">    <servlet></span>

<span style="color: #008000;">        <servlet-name>listener</servlet-name></span>

<span style="color: #008000;">        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class></span>

<span style="color: #008000;">        <load-on-startup>1</load-on-startup></span>

<span style="color: #008000;">    </servlet></span>

&nbsp;

<span style="color: #008000;">    <servlet-mapping></span>

<span style="color: #008000;">        <servlet-name>listener</servlet-name></span>

<span style="color: #008000;">        <url-pattern>/</url-pattern></span>

<span style="color: #008000;">    </servlet-mapping></span>

&nbsp;

<span style="color: #008000;">    <context-param></span>

<span style="color: #008000;">        <param-name>contextConfigLocation</param-name></span>

<span style="color: #008000;">        <param-value>/WEB-INF/listener-servlet.xml</param-value></span>

<span style="color: #008000;">    </context-param></span>

<span style="color: #008000;">    <strong><resource-ref></strong></span>

**<span style="color: #008000;">        <description>Listener Database</description></span>**

**<span style="color: #008000;">        <res-ref-name>jdbc/listener-dss</res-ref-name></span>**

**<span style="color: #008000;">        <res-type>javax.sql.DataSource</res-type></span>**

**<span style="color: #008000;">        <res-auth>Container</res-auth></span>**

**<span style="color: #008000;">    </resource-ref></span>**

&nbsp;

<span style="color: #008000;">    <listener></span>

<span style="color: #008000;">        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class></span>

<span style="color: #008000;">    </listener></span>

&nbsp;

<span style="color: #008000;">  <welcome-file-list></span>

<span style="color: #008000;">    <welcome-file>index.jsp</welcome-file></span>

<span style="color: #008000;">  </welcome-file-list></span>

&nbsp;

<span style="color: #008000;"></web-app></span>

&nbsp;

<span style="text-decoration: underline;"><strong><span style="color: #000000; text-decoration: underline;">Step</span></strong></span>** <span style="color: #000000;">3:</span>** <span style="color: #000000;">Next we will update the Spring context xml file to tell the Spring container that it needs to do a JNDI look up. My Spring context file name is listener-servlet.xml and this is under <strong>WEB-INF</strong> folder. Add the following(See highlighted section)</span>

&nbsp;

<span style="color: #008000;"><beans xmlns=&#8221;http://www.springframework.org/schema/beans&#8221;</span>

<span style="color: #008000;">       xmlns:context=&#8221;http://www.springframework.org/schema/context&#8221;</span>

<span style="color: #008000;">       xmlns:mvc=&#8221;http://www.springframework.org/schema/mvc&#8221; xmlns:xsi=&#8221;http://www.w3.org/2001/XMLSchema-instance&#8221;</span>

<span style="color: #008000;">       xmlns:tx=&#8221;http://www.springframework.org/schema/tx&#8221;</span>

<span style="color: #008000;">       xmlns:p=&#8221;http://www.springframework.org/schema/p&#8221;</span>

<span style="color: #008000;">       xsi:schemaLocation=&#8221;http://www.springframework.org/schema/beans</span>

<span style="color: #008000;">        http://www.springframework.org/schema/beans/spring-beans-3.0.xsd</span>

<span style="color: #008000;">        http://www.springframework.org/schema/context</span>

<span style="color: #008000;">        http://www.springframework.org/schema/context/spring-context-3.0.xsd</span>

<span style="color: #008000;">        http://www.springframework.org/schema/mvc</span>

<span style="color: #008000;">        http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd</span>

<span style="color: #008000;">        http://www.springframework.org/schema/tx</span>

<span style="color: #008000;">        http://www.springframework.org/schema/tx/spring-tx.xsd &#8220;></span>

<span style="color: #008000;">    <context:component-scan base-package=&#8221;com.acn.cslistener&#8221; /></span>

<span style="color: #008000;">    <mvc:annotation-driven /></span>

<span style="color: #008000;">    <tx:annotation-driven/></span>

<span style="color: #008000;">    <bean</span>

<span style="color: #008000;">            class=&#8221;org.springframework.web.servlet.view.InternalResourceViewResolver&#8221;></span>

<span style="color: #008000;">        <property name=&#8221;prefix&#8221;></span>

<span style="color: #008000;">            <value>/WEB-INF/pages/</value></span>

<span style="color: #008000;">        </property></span>

<span style="color: #008000;">        <property name=&#8221;suffix&#8221;></span>

<span style="color: #008000;">            <value>.jsp</value></span>

<span style="color: #008000;">        </property></span>

<span style="color: #008000;">    </bean></span>

<span style="color: #008000;">   <strong> <bean id=&#8221;sessionFactory&#8221; class=&#8221;org.springframework.orm.hibernate4.LocalSessionFactoryBean&#8221;></strong></span>

**<span style="color: #008000;">        <property name=&#8221;dataSource&#8221; ref=&#8221;dataSource&#8221;/></span>**

**<span style="color: #008000;">        <property name=&#8221;hibernateProperties&#8221;></span>**

**<span style="color: #008000;">            <props></span>**

**<span style="color: #008000;">                <prop key=&#8221;hibernate.dialect&#8221;>org.hibernate.dialect.Oracle10gDialect</prop></span>**

**<span style="color: #008000;">                <prop key=&#8221;hibernate.show_sql&#8221;>true</prop></span>**

**<span style="color: #008000;">            </props></span>**

**<span style="color: #008000;">        </property></span>**

**<span style="color: #008000;">        <property name=&#8221;packagesToScan&#8221; value=&#8221;com.acn.cslistener&#8221; /></span>**

**<span style="color: #008000;">    </bean></span>**

**<span style="color: #008000;">    <span style="color: #008080;"><bean id=&#8221;dataSource&#8221; class=&#8221;org.springframework.jndi.JndiObjectFactoryBean&#8221;></span></span>**

<span style="color: #008080;"><strong>        <property name=&#8221;jndiName&#8221; value=&#8221;java:comp/env/jdbc/listener-dss&#8221;/></strong></span>

<span style="color: #008080;"><strong>    </bean></strong></span>

**<span style="color: #008000;">    <bean id=&#8221;transactionManager&#8221; class=&#8221;org.springframework.orm.hibernate4.HibernateTransactionManager&#8221;</span>**

**<span style="color: #008000;">          p:sessionFactory-ref=&#8221;sessionFactory&#8221;></span>**

**<span style="color: #008000;">    </bean></span>**

<span style="color: #008000;">    <bean id=&#8221;persistenceAnnotation&#8221;    class=&#8221;org.springframework.orm.jpa.support.PersistenceAnnotationBeanPostProcessor&#8221; /></span>

<span style="color: #008000;"></beans></span>

<span style="color: #000000;"> </span>

**<span style="color: #000000;">Step 4: </span>**<span style="color: #000000;">This is the crucial step. If you are using Jboss then it requires that you tell the web container that Jboss will provide the datasource .xml file where you have defined your jndi properties. Create a new file <strong>jboss-web.xml. </strong>Place this file under <strong>WEB-INF </strong>folder. The contents of the file whould like this.</span>

<span style="color: #008000;"><?xml version=&#8221;1.0&#8243; encoding=&#8221;UTF-8&#8243;?></span>

<span style="color: #008000;"><jboss-web></span>

<span style="color: #008000;">    <resource-ref></span>

<span style="color: #008000;">        <res-ref-name>jdbc/listener-dss</res-ref-name></span>

<span style="color: #008000;">        <res-type>javax.sql.DataSource</res-type></span>

<span style="color: #008000;">        <jndi-name>java:/jdbc/listener-dss</jndi-name></span>

<span style="color: #008000;">    </resource-ref></span>

<span style="color: #008000;"></jboss-web></span>

That&#8217;s all we need to do.

&nbsp;

~~~~ Ciao.

&nbsp;