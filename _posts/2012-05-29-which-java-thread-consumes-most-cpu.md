---
id: 281
title: Which java thread consumes most cpu
date: 2012-05-29T23:26:28+00:00
author: Claudio Miranda
layout: post
guid: http://claudius.com.br/?p=281
permalink: /2012/05/which-java-thread-consumes-most-cpu/
categories:
  - Dicas
  - Java
---
_I wrote the topic in Portuguese ([Qual thread do programa Java mais consome cpu](http://claudius.com.br/2012/05/qual-thread-do-programa-java-mais-consome-cpu/)), and decided to write it in English to help more people._

I developed a script named [top_threads.sh](http://code.google.com/p/claudius-alphaworks/source/browse/trunk/shell_bin/top_threads.sh) to display all threads sorted by cpu usage of a java process.
  
This script is for linux and uses the command line utilities: top, jstack and sed.

Internally it uses top to list all thread for a given process, sort it by cpu usage. Then request a thread dump (jstack), for each thread from the top convert the PID to hex and sed filter out the thread stack trace from thread dump.

See a sample from a JBoss AS 7.1

<pre>$ top_threads.sh 9772 5
  PID USER      VIRT  RES  SHR CODE DATA S %CPU %MEM   TIME COMMAND                                                                                                                                       
 9814 claudio  1452m  55m 7316    4 1.4g S  5.9  0.9   0:00 /opt/jdk/jdk1.7.0_02/bin/java -Xss128k -Xmx1300m -classpath build/web/ br.com.claudius.threads.NumThreads 40 99999 1                          
 9801 claudio  1452m  55m 7316    4 1.4g S  5.9  0.9   0:00 /opt/jdk/jdk1.7.0_02/bin/java -Xss128k -Xmx1300m -classpath build/web/ br.com.claudius.threads.NumThreads 40 99999 1                          
 9787 claudio  1452m  55m 7316    4 1.4g R  5.9  0.9   0:00 /opt/jdk/jdk1.7.0_02/bin/java -Xss128k -Xmx1300m -classpath build/web/ br.com.claudius.threads.NumThreads 40 99999 1                          
 9823 claudio  1452m  55m 7316    4 1.4g S  4.0  0.9   0:00 /opt/jdk/jdk1.7.0_02/bin/java -Xss128k -Xmx1300m -classpath build/web/ br.com.claudius.threads.NumThreads 40 99999 1                          
 9821 claudio  1452m  55m 7316    4 1.4g S  4.0  0.9   0:00 /opt/jdk/jdk1.7.0_02/bin/java -Xss128k -Xmx1300m -classpath build/web/ br.com.claudius.threads.NumThreads 40 99999 1                          
========&gt; Java LWP: 9814 - Native Thread ID=2656
"CapacityThread__30" prio=10 tid=0x5e239c00 nid=0x2656 waiting for monitor entry [0x5df07000]
   java.lang.Thread.State: BLOCKED (on object monitor)
        at java.security.SecureRandom.nextBytes(SecureRandom.java:455)
        - waiting to lock &lt;0x632406b0&gt; (a java.security.SecureRandom)
        at java.util.UUID.randomUUID(UUID.java:146)
        at br.com.claudius.threads.ThreadTest.run(NumThreads.java:146)
        at java.lang.Thread.run(Thread.java:722)

========&gt; Java LWP: 9801 - Native Thread ID=2649
"CapacityThread__17" prio=10 tid=0x5e225800 nid=0x2649 waiting for monitor entry [0x5e0b4000]
   java.lang.Thread.State: BLOCKED (on object monitor)
        at java.security.SecureRandom.nextBytes(SecureRandom.java:455)
        - waiting to lock &lt;0x632406b0&gt; (a java.security.SecureRandom)
        at java.util.UUID.randomUUID(UUID.java:146)
        at br.com.claudius.threads.ThreadTest.run(NumThreads.java:146)
        at java.lang.Thread.run(Thread.java:722)

========&gt; Java LWP: 9787 - Native Thread ID=263b
"CapacityThread__3" prio=10 tid=0x5e20f800 nid=0x263b waiting for monitor entry [0x5e396000]
   java.lang.Thread.State: BLOCKED (on object monitor)
        at java.security.SecureRandom.nextBytes(SecureRandom.java:455)
        - waiting to lock &lt;0x632406b0&gt; (a java.security.SecureRandom)
        at java.util.UUID.randomUUID(UUID.java:146)
        at br.com.claudius.threads.ThreadTest.run(NumThreads.java:146)
        at java.lang.Thread.run(Thread.java:722)

========&gt; Java LWP: 9823 - Native Thread ID=265f
"CapacityThread__39" prio=10 tid=0x5e248000 nid=0x265f waiting for monitor entry [0x5ddde000]
   java.lang.Thread.State: BLOCKED (on object monitor)
        at java.security.SecureRandom.nextBytes(SecureRandom.java:455)
        - waiting to lock &lt;0x632406b0&gt; (a java.security.SecureRandom)
        at java.util.UUID.randomUUID(UUID.java:146)
        at br.com.claudius.threads.ThreadTest.run(NumThreads.java:146)
        at java.lang.Thread.run(Thread.java:722)

========&gt; Java LWP: 9821 - Native Thread ID=265d
"CapacityThread__37" prio=10 tid=0x5e244c00 nid=0x265d waiting for monitor entry [0x5de20000]
   java.lang.Thread.State: BLOCKED (on object monitor)
        at java.security.SecureRandom.nextBytes(SecureRandom.java:455)
        - waiting to lock &lt;0x632406b0&gt; (a java.security.SecureRandom)
        at java.util.UUID.randomUUID(UUID.java:146)
        at br.com.claudius.threads.ThreadTest.run(NumThreads.java:146)
        at java.lang.Thread.run(Thread.java:722)</pre>

Leave a comment if it is useful and how it helped your case. Also, if you want some improvement or bug fix, write in the comments section.