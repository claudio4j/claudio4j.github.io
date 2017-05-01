---
id: 343
title: How setup JBoss EAP 6.1 in Eclipse 3.7 Indigo
date: 2013-06-20T20:10:36+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=343
permalink: /2013/06/how-setup-jboss-eap-6-1-eclipse-3-7/
categories:
  - Dicas
---
I was just using eclipse juno with jboss tools and was sick by its slowness, some icons just disappear from console window and some buggy messages.

So I went and modified jboss tools 3.3 to make it work with EAP 6.1

Steps

  * <a href="http://www.jboss.org/tools/download/stable/3_3_Final.html" target="_blank">download source of jboss tools core 3.3</a> and unpack it somewhere
  * download and modify attached <a href="/wp-content/uploads/2013/06/compile" target="_blank">compile script</a> to suit your environment (JAVA_HOME and ECLIPSE), also uncomment the section to backup target jar files
  * apply the modification as suggested in the <a href="/wp-content/uploads/2013/06/changes.txt" target="_blank">diff</a> file.
  * invoke compile

NOTE: This will make it work ONLY with EAP 6.1 that uses modules/system/layers/base, EAP 6.0 \_will not work\_.

Tested and verified on Linux and Windows.

For your convenience I attached the <a href="/wp-content/uploads/2013/06/classes_as_core.zip" target="_blank">compiled code (classes_as_core.zip)</a> to save you the time to download and compile. With this piece you only need to update the target jars, see compile.

Hope this help those who find that eclipse juno is not working accordingly.

[<img class="alignnone size-medium wp-image-336" alt="jbt1" src="/wp-content/uploads/2013/06/jbt1-280x300.png" width="280" height="300" srcset="http://claudius.com.br/wp-content/uploads/2013/06/jbt1-280x300.png 280w, http://claudius.com.br/wp-content/uploads/2013/06/jbt1.png 527w" sizes="(max-width: 280px) 100vw, 280px" />](/wp-content/uploads/2013/06/jbt1.png)

[<img class="alignnone size-medium wp-image-337" alt="jbt2" src="/wp-content/uploads/2013/06/jbt2-300x283.png" width="300" height="283" srcset="http://claudius.com.br/wp-content/uploads/2013/06/jbt2-300x283.png 300w, http://claudius.com.br/wp-content/uploads/2013/06/jbt2.png 965w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2013/06/jbt2.png)