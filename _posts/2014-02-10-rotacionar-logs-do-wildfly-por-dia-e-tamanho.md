---
id: 391
title: Rotacionar logs do Wildfly por dia e tamanho
date: 2014-02-10T09:18:38+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=391
permalink: /2014/02/rotacionar-logs-do-wildfly-por-dia-e-tamanho/
categories:
  - Dicas
  - Java
---
Uma dica interessante é rotacionar os logs por dia e tamanho. Ao rotacionar somente por dia, o tamanho do arquivo pode ficar gigante, atingindo a ordem de GB. Se rotacionar por tamanho, perde-se a capacidade de identificar os logs pelo nome do arquivo, então combina-se os dois.

No Wildfly 8 (também no EAP 6.1) é possível ter esta configuração através de um handler já disponível: org.jboss.logmanager.handlers.PeriodicSizeRotatingFileHandler

Ele deverá ser configurado através de um custom-handler.

Veja o trecho xml a adicionar no subsistema de logging.

<pre>&lt;custom-handler name="<strong>ROTACAO_TAMANHO_DATA</strong>" class="org.jboss.logmanager.handlers.PeriodicSizeRotatingFileHandler"  module="org.jboss.logmanager"&gt;
    &lt;level name="INFO"/&gt;
    &lt;formatter&gt;
        &lt;pattern-formatter pattern="<strong>%d{dd-MM-yyyy HH:mm:ss,SSS} %-5p [%c] (%t) %s%E%n</strong>"/&gt;
    &lt;/formatter&gt;
    &lt;properties&gt;
        &lt;property name="rotateSize" value="4024000"/&gt;
        &lt;property name="maxBackupIndex" value="10"/&gt;
        &lt;property name="suffix" value=".yyyy-MM-dd"/&gt;
        &lt;property name="append" value="true"/&gt;
        &lt;property name="autoFlush" value="true"/&gt;
        &lt;property name="fileName" value="${jboss.server.log.dir}/jboss.log"/&gt;
    &lt;/properties&gt;
&lt;/custom-handler&gt;</pre>

Ou se não quiser para o Wildfly, pode fazer isso enquanto ele funciona, com o uso do CLI.

<pre>/subsystem=logging/custom-handler=ROTACAO_TAMANHO_DATA:add(class="org.jboss.logmanager.handlers.PeriodicSizeRotatingFileHandler", module="org.jboss.logmanager", enabled=true, formatter="%d{dd-MM-yyyy HH:mm:ss,SSS} %-5p [%c] (%t) %s%E%n", level=INFO, name="ROTACAO_TAMANHO_DATA", properties={rotateSize=4024000,maxBackupIndex=10,suffix=".yyyy-MM-dd",fileName="${jboss.server.log.dir}/jboss.log", append=true, autoFlush=true})</pre>

Os arquivos gerados ficarão com a seguinte nomenclatura.

<pre>jboss.log
jboss.log.2014-02-10.1
jboss.log.2014-02-10.10
jboss.log.2014-02-10.2
jboss.log.2014-02-10.3
jboss.log.2014-02-10.4
jboss.log.2014-02-10.5
jboss.log.2014-02-10.6
jboss.log.2014-02-10.7
jboss.log.2014-02-10.8
jboss.log.2014-02-10.9</pre>

&nbsp;