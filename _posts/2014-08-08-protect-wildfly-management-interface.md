---
id: 435
title: Protect wildly management interface
date: 2014-08-08T03:58:21+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=435
permalink: /2014/08/protect-wildfly-management-interface/
categories:
  - Dicas
---
Want to protect your wildfly administrative console with https only access ? See this tech tip. It will protect the web console and jboss-cli.

First step is to create the self-signed digital certificate with keytool. Open the terminal and go to **conf** directory (standalone or domain), add the **certs** directory and cd into it. Modify the parameters below to fit your needs.

<pre>keytool -genkey -alias wildfly_mgmt -keyalg RSA -keystore wildfly.jks -storepass admin123 -keypass admin123 --dname "CN=mgmt-connector,OU=jboss,O=jboss,L=Brasilia,S=DF,C=BR"</pre>

Now, lets configure wildfly.

## Standalone mode

Edit standalone.xml and modify as the sample below, a **server-identities** section is added and the **http-interface** is modified.

<pre>&lt;security-realm name="ManagementRealm"&gt;
<strong>    &lt;server-identities&gt;
        &lt;ssl&gt;
            &lt;keystore path="${jboss.server.config.dir}/certs/wildfly.jks" keystore-password="admin123" /&gt;
        &lt;/ssl&gt;
    &lt;/server-identities&gt;</strong>

&lt;management-interfaces&gt;
    &lt;http-interface security-realm="ManagementRealm" http-upgrade-enabled="true"&gt;
        &lt;socket-binding <strong>https="management-https"</strong>/&gt;
    &lt;/http-interface&gt;
&lt;/management-interfaces&gt;</pre>

Start Wildfly in standalone mode and point the browser navigator to https://localhost:9993. it will ask you to trust the self-signed certificate.

To use jboss-cli.sh, it should use the https protocol, see below how to modify jboss-cli.xml.

<pre>&lt;default-protocol use-legacy-override="true"&gt;<strong>https-remoting</strong>&lt;/default-protocol&gt;

&lt;!-- The default controller to connect to when 'connect' command is executed w/o arguments --&gt;
&lt;default-controller&gt;
<strong>    &lt;protocol&gt;https-remoting&lt;/protocol&gt;</strong>
    &lt;host&gt;localhost&lt;/host&gt;
<strong>    &lt;port&gt;9993&lt;/port&gt;</strong>
&lt;/default-controller&gt;</pre>

That way, jboss-cli.sh will connect to Wildfly with no additional parameter on command line, only ./jboss-cli.sh -c

&nbsp;

## Domain mode

Domain mode has a slightly different configuration, edit host.xml as below

<pre>&lt;security-realm name="ManagementRealm"&gt;
<strong>    &lt;server-identities&gt;
        &lt;ssl&gt;
            &lt;keystore path="${jboss.domain.config.dir}/certs/wildfly.jks" keystore-password="admin123" /&gt;
        &lt;/ssl&gt;
    &lt;/server-identities&gt;</strong>

&lt;management-interfaces&gt;
    &lt;native-interface security-realm="ManagementRealm"&gt;
        &lt;socket interface="management" port="${jboss.management.native.port:9999}"/&gt;
    &lt;/native-interface&gt;
    &lt;http-interface security-realm="ManagementRealm" http-upgrade-enabled="true"&gt;
        &lt;socket interface="management" <strong>secure-port="${jboss.management.http.port:9993}"</strong>/&gt;
    &lt;/http-interface&gt;
&lt;/management-interfaces&gt;
</pre>

jboss-cli.xml must be modified as show before.

Comment below if this was of some help for you.