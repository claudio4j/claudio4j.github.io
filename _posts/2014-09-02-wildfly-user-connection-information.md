---
id: 449
title: 'Wildfly&#8217;s User Connection information'
date: 2014-09-02T23:03:00+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=449
permalink: /2014/09/wildfly-user-connection-information/
categories:
  - Java
tags:
  - wildfly
---
A <a href="https://github.com/wildfly/wildfly-core/pull/89" target="_blank">contribution to wildfly was accepted</a>, related to a feature to jboss-cli, to display user connection informantion (<a href="https://issues.jboss.org/browse/WFCORE-73" target="_blank">WFCORE-73</a>).

Currently, when an user is connected using jboss-cli, it is not possible to display connection information, this contribution displays: username, logged in time, associated roles, ssl certificate.

To have access to this you need to clone wildfly repo and build it.

A new connection-info command is available, an example:

  * Logged in with no SSL, no RBAC

<pre>[domain@pavlov-0:9990 /] connection-info 
Username               admin, granted role ["SuperUser"] 
Logged since           Tue Sep 02 22:45:32 BRT 2014      
Not an SSL connection.                              
</pre>

&nbsp;

  * Logged in with SSL, no RBAC

<pre>[domain@pavlov-0:9993 /] connection-info
Username     admin, granted role ["SuperUser"]                             
Logged since Tue Sep 02 22:48:28 BRT 2014                                  
Subject      CN=mgmt-connector,OU=jboss,O=jboss,L=Brasilia,ST=DF,C=BR      
Issuer       CN=mgmt-connector, OU=jboss, O=jboss, L=Brasilia, ST=DF, C=BR 
Valid from   Fri Aug 08 01:13:16 BRT 2014                                  
Valid to     Thu Nov 06 02:13:16 BRST 2014                                 
SHA1         fa:25:f4:cf:57:89:ce:ff:97:82:9d:b4:c8:b1:67:ef:b3:08:a8:b4   
MD5          e6:67:14:c7:86:84:d3:22:14:21:e7:43:09:05:a4:7f
</pre>

&nbsp;

  * Logged in with  SSL, with RBAC

<pre>[domain@pavlov-0:9993 /] connection-info
Username     claudio, granted roles ["Maintainer","Operator","Deployer"]   
Logged since Tue Sep 02 22:52:22 BRT 2014                                  
Subject      CN=mgmt-connector,OU=jboss,O=jboss,L=Brasilia,ST=DF,C=BR      
Issuer       CN=mgmt-connector, OU=jboss, O=jboss, L=Brasilia, ST=DF, C=BR 
Valid from   Fri Aug 08 01:13:16 BRT 2014                                  
Valid to     Thu Nov 06 02:13:16 BRST 2014                                 
SHA1         fa:25:f4:cf:57:89:ce:ff:97:82:9d:b4:c8:b1:67:ef:b3:08:a8:b4   
MD5          e6:67:14:c7:86:84:d3:22:14:21:e7:43:09:05:a4:7f

</pre>

&nbsp;