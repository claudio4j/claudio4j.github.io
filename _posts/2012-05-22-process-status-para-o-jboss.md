---
id: 278
title: process status para o JBoss
date: 2012-05-22T14:30:55+00:00
author: Claudio Miranda
layout: post
guid: http://claudius.com.br/?p=278
permalink: /2012/05/process-status-para-o-jboss/
categories:
  - Dicas
---
Fiz um script que pode ajudar em ambiente que possuem diversas instâncias do JBoss, versão 5 e 7.

Dado um comando <a href="http://code.google.com/p/claudius-alphaworks/source/browse/trunk/shell_bin/ps_jboss.sh" target="_blank">ps_jboss.sh</a>

veja um resultado no meu computador

É mostrado o

  * número do processo (PID),
  * Versão do JBoss (5 ou EAP6, AS7)
  * nome da instância iniciada,
  * quantidade de threads do processo,
  * há quanto tempo o processo já está em funcionamento
  * memória real consumida (RSS)
  * Todas as portas em LISTEN
  * Diretório de instalação do JBoss
  * Diretório onde residem os logs

Notem que o comando é bem rápido, o que demora um pouquinho é a execução do jinfo para obter algumas propriedades da instância.

<pre>24746 - EAP 5 - lab-tagcloud (94 threads, elapsed time 02:23, RSS memory 1377 MB)
        /opt/jboss-epp-5.2.1/jboss-as
        /opt/jboss-epp-5.2.1/jboss-as/server/lab-tagcloud/log

        tcp 127.0.0.1:1098
        tcp 127.0.0.1:1099
        tcp 127.0.0.1:3873
        tcp 127.0.0.1:41862
        tcp 127.0.0.1:4444
        tcp 127.0.0.1:4445
        tcp 127.0.0.1:4446
        tcp 127.0.0.1:4712
        tcp 127.0.0.1:4713
        tcp 127.0.0.1:8009
        tcp 127.0.0.1:8080
        tcp 127.0.0.1:8083

25029 - EAP 5 - lab-tse1 -b 192.168.5.90 (17 threads, elapsed time 00:05, RSS memory 60 MB)
        /opt/jboss-eap-5.1.2-hornetq-cxf/jboss-as
        /opt/jboss-eap-5.1.2-hornetq-cxf/jboss-as/server/lab-tse1/log

24838 - EAP 6/AS 7 Standalone [standalone-lab1.xml] (38 threads, elapsed time 01:30, RSS memory 228 MB)
        /opt/jboss-as-7.1.0.Final/standalone
        /opt/jboss-as-7.1.0.Final/standalone/log

        tcp 127.0.0.1:10090
        tcp 127.0.0.1:10099
        tcp 192.168.5.90:4547
        tcp 192.168.5.90:8180</pre>

Se este script é útil, ou precise de alguma funcionalidades, faça um comentário e posso melhorá-lo.