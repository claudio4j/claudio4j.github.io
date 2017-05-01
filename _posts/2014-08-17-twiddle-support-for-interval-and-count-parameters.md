---
id: 439
title: Twiddle support for interval and count parameters
date: 2014-08-17T22:43:13+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=439
permalink: /2014/08/twiddle-support-for-interval-and-count-parameters/
categories:
  - Dicas
  - Java
tags:
  - jboss
---
JBoss 5 has a good command line monitoring tool, <a href="https://community.jboss.org/wiki/Twiddle" target="_blank">twiddle.sh</a>, it can interact with JBoss jmx server to get attributes, invoke commands, etc.

The default behavior is to connect to JBoss, invoke the jmx command and exit. What if you setup a couple of monitoring attributes to read and saves to an external file ? User must create a bash script to loop the twiddle command into it, and creating a lot of connections during the monitoring.

I have modified twiddle source code to support an interval and count parameters, this allow the user to better control how much to interact with JBoss server, also it optimizes the connection behavior, where the twiddle gets one connection and works with it.

As I need only to read jmx attributes, I changed only the <a href="http://anonsvn.jboss.org/repos/jbossas/tags/JBPAPP_5_2_0_GA/console/src/main/org/jboss/console/twiddle/command/GetCommand.java" target="_blank">GetCommand.java</a>, be aware that the way I changed the source code is not reusable between commands, as I didn&#8217;t want to spend too much time on this enhancement, this is enough for me.

You can grab my enhanced <a href="/wp-content/uploads/2014/08/twiddle-claudius.zip" target="_blank">GetCommand.java</a>, do a diff to see the modifications. Packaged is a custom build.sh script to compile and package the new GetCommand version. I didn&#8217;t use maven or build.xml scripts, as I do not want the full console or spend a lot of time downloading libraries, this simple build.sh is enough for me.

You can grab the <a href="http://anonsvn.jboss.org/repos/jbossas/tags/JBPAPP_5_2_0_GA/console/" target="_blank">twiddle source code</a> (navigate the svn tree to find the correct AS version).

To run twiddle with the interval and count, use the jvm parameters as mentioned below, also you can use only the interval parameter to run continuously.

<pre>JAVA_OPTS="-Dtwiddle.interval=1 -Dtwiddle.count=5" ./twiddle.sh get &lt;regular twiddle parameters&gt;</pre>

&nbsp;