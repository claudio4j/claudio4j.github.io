---
id: 268
title: Qual thread do programa Java mais consome cpu ?
date: 2012-05-21T12:49:26+00:00
author: Claudio Miranda
layout: post
guid: http://claudius.com.br/?p=268
permalink: /2012/05/qual-thread-do-programa-java-mais-consome-cpu/
categories:
  - Dicas
  - Java
---
Fiz um script para listar as threads que mais consomem CPU de um processo Java. Este script é para linux e utiliza os comandos: top, jstack e sed.

Basicamente utilizo o top, para listar todas as threads do processo, ordenando pelo consumo de CPU. Então faço um thread dump com jstack, e comparo cada thread id mostrado pelo top, com o thread id do thread dump, para fazer a paridade, tive de converter o process id do top para o native id do thread dump, então uso uma instrução sed para mostrar o stacktrace da thread que consome CPU.

Veja como é uma saída, quando utilizo no JBoss AS 7.1, na inicialização.

<pre>$ top_threads.sh 9772 5
  PID USER      VIRT  RES  SHR CODE DATA S %CPU %MEM   TIME COMMAND                                                                                                                                       
 9814 claudio  1452m  55m 7316    4 1.4g S  5.9  0.9   0:00 /opt/jdk/jdk1.7.0_02/bin/java -Xss128k -Xmx1300m -classpath build/web/ br.com.claudius.threads.NumThreads 40 99999 1                          
 9801 claudio  1452m  55m 7316    4 1.4g S  5.9  0.9   0:00 /opt/jdk/jdk1.7.0_02/bin/java -Xss128k -Xmx1300m -classpath build/web/ br.com.claudius.threads.NumThreads 40 99999 1                          
 9787 claudio  1452m  55m 7316    4 1.4g R  5.9  0.9   0:00 /opt/jdk/jdk1.7.0_02/bin/java -Xss128k -Xmx1300m -classpath build/web/ br.com.claudius.threads.NumThreads 40 99999 1                          
 9823 claudio  1452m  55m 7316    4 1.4g S  4.0  0.9   0:00 /opt/jdk/jdk1.7.0_02/bin/java -Xss128k -Xmx1300m -classpath build/web/ br.com.claudius.threads.NumThreads 40 99999 1                          
 9821 claudio  1452m  55m 7316    4 1.4g S  4.0  0.9   0:00 /opt/jdk/jdk1.7.0_02/bin/java -Xss128k -Xmx1300m -classpath build/web/ br.com.claudius.threads.NumThreads 40 99999 1                          
========&gt; Java LWP: 9814 - Native Thread ID=2656
"CapacityThread__30" prio=10 tid=0x5e239c00 nid=0x2656 waiting for monitor entry [0x5df07000]
   java.lang.Thread.State: BLOCKED (on object monitor)
        at java.security.SecureRandom.nextBytes(SecureRandom.java:455)
        - waiting to lock  (a java.security.SecureRandom)
        at java.util.UUID.randomUUID(UUID.java:146)
        at br.com.claudius.threads.ThreadTest.run(NumThreads.java:146)
        at java.lang.Thread.run(Thread.java:722)

========&gt; Java LWP: 9801 - Native Thread ID=2649
"CapacityThread__17" prio=10 tid=0x5e225800 nid=0x2649 waiting for monitor entry [0x5e0b4000]
   java.lang.Thread.State: BLOCKED (on object monitor)
        at java.security.SecureRandom.nextBytes(SecureRandom.java:455)
        - waiting to lock  (a java.security.SecureRandom)
        at java.util.UUID.randomUUID(UUID.java:146)
        at br.com.claudius.threads.ThreadTest.run(NumThreads.java:146)
        at java.lang.Thread.run(Thread.java:722)

========&gt; Java LWP: 9787 - Native Thread ID=263b
"CapacityThread__3" prio=10 tid=0x5e20f800 nid=0x263b waiting for monitor entry [0x5e396000]
   java.lang.Thread.State: BLOCKED (on object monitor)
        at java.security.SecureRandom.nextBytes(SecureRandom.java:455)
        - waiting to lock  (a java.security.SecureRandom)
        at java.util.UUID.randomUUID(UUID.java:146)
        at br.com.claudius.threads.ThreadTest.run(NumThreads.java:146)
        at java.lang.Thread.run(Thread.java:722)

========&gt; Java LWP: 9823 - Native Thread ID=265f
"CapacityThread__39" prio=10 tid=0x5e248000 nid=0x265f waiting for monitor entry [0x5ddde000]
   java.lang.Thread.State: BLOCKED (on object monitor)
        at java.security.SecureRandom.nextBytes(SecureRandom.java:455)
        - waiting to lock  (a java.security.SecureRandom)
        at java.util.UUID.randomUUID(UUID.java:146)
        at br.com.claudius.threads.ThreadTest.run(NumThreads.java:146)
        at java.lang.Thread.run(Thread.java:722)</pre>

[Veja e copie o script top_threads.sh](http://code.google.com/p/claudius-alphaworks/source/browse/trunk/shell_bin/top_threads.sh)

Caso este script tenha sido útil, faça um comentário abaixo. Se tiver melhorias a fazer, comente aqui, assim todos podem se beneficiar do script.