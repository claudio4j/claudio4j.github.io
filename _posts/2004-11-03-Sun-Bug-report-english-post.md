---
id: 23
title: 'Sun Bug report &#8211; (english post)'
date: 2004-11-03T12:32:17+00:00
author: Claudio Miranda
layout: post
permalink: /2004/11/Sun-Bug-report-english-post/
categories:
  - Java
---
For those english readers, who have been visiting this blog through
  
google, I wrote a english version (resumed).

&nbsp;I submitted a <a target="_blank"
href="http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=6182602">bug<br /> report</a> to Sun, about the usage of J2SE 5 <span
style="font-family: monospace;">-Xshare:on</span> feature and Linux
  
kernel 2.6.9. At this moment, it was classified as &#8220;request for
  
enhancement&#8221;.

The issue happens if you have been using J2SE 5 -Xshare:on under Linux
  
kernel 2.6.8.1 (or versions below it), and switch to kernel 2.6.9. When
  
using -Xshare:on option again, the JVM will try to use the shared
  
archive created under a different memory layout. See the bug report.

To solve the problem, just run the JVM with <span
style="font-family: monospace;">-Xshare:dump</span> option. That will
  
regenerate the shared archive.