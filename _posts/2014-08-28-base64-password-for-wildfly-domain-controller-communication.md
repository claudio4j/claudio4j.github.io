---
id: 444
title: base64 password for wildfly domain controller communication
date: 2014-08-28T15:29:07+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=444
permalink: /2014/08/base64-password-for-wildfly-domain-controller-communication/
categories:
  - Dicas
---
Using wildfly in domain mode with additional host controller on different servers, it is required an user to authenticate the HC (host controller) to DC (domain controller). This is configured in the host.xml of HC server, the password is base64 encoded, see the example:

<pre>&lt;management&gt;
    &lt;security-realms&gt;
        &lt;security-realm name="ManagementRealm"&gt;
<strong>            &lt;server-identities&gt;</strong>
<strong>                &lt;secret value="YWRtaW4xMjNA"/&gt;</strong>
<strong>            &lt;/server-identities&gt;</strong>

&lt;domain-controller&gt;
    &lt;remote host="${jboss.domain.master.address}" port="${jboss.domain.master.port:9999}" security-realm="ManagementRealm" <strong>username="admin2"</strong> /&gt;
&lt;/domain-controller&gt;</pre>

If you do not know the base64 of a password, use the base64 linux command to convert the plain text password, the echo -n parameter, doesn&#8217;t print the carriage return char. See the example for a password: **admin123@**

<pre>$ echo -n "admin123@" | base64 
YWRtaW4xMjNA
</pre>

This is useful in cases where the add-user.sh command is invoked in non interactive mode, as it doesn&#8217;t print the base64 password.

&nbsp;