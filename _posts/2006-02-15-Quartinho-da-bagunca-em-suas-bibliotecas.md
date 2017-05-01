---
id: 94
title: Quartinho da bagunça em suas bibliotecas
date: 2006-02-15T01:38:37+00:00
author: Claudio Miranda
layout: post
permalink: /2006/02/Quartinho-da-bagunca-em-suas-bibliotecas/
categories:
  - Java
---
Ok, o t&iacute;tulo n&atilde;o &eacute; dos melhores, apenas para chamar a sua aten&ccedil;&atilde;o. Mas o tema &eacute; totalmente pertinente, voc&ecirc; vai entender.

J&aacute; verificou quantas redund&acirc;ncias de bibliotecas existentes em seus programas Java ? 

Hoje precisei criar um diret&oacute;rio com as bibliotecas mais comuns do jakarta-commons. Ao pensar nesse projeto qual &eacute; a biblioteca mais lembrada ? **commons-logging**.

Ent&atilde;o fiz uma busca em meu diret&oacute;rio de programas Java

<pre><strong>find . -name commons-logging\*.jar -exec ls -l {} \;</strong></pre>

<pre><strong>
-rw-r--r--  1 claudio claudio 38015 Fev  4 00:31 ./webwork/lib/bootstrap/commons-logging.jar
-rw-r--r--  1 claudio claudio 38015 Fev  4 00:31 ./webwork/lib/default/commons-logging.jar
-rw-r--r--  1 claudio claudio 38015 Fev  4 00:31 ./webwork/lib/hibernate/commons-logging.jar
-rw-r--r--  1 claudio claudio 38015 Fev  4 00:31 ./webwork/lib/spring/commons-logging.jar
-rw-r--r--  1 claudio claudio 38015 Jan 18 05:24 ./hibernate-3.1/lib/commons-logging-1.0.4.jar
-rw-r--r--  1 claudio claudio 22327 Jan 18 19:30 ./eclipse/plugins/org.eclipse.tomcat_4.1.30.1/commons-logging-api.jar
-rw-r--r--  1 claudio claudio 26202 Mar 26  2005 ./jakarta-tomcat-5.5.9/bin/commons-logging-api.jar
-rw-r--r--  1 claudio claudio 38015 Jun 16  2005 ./jakarta-tomcat-5.5.9/webapps/blojsom/WEB-INF/lib/commons-logging-1.0.4.jar
-rw-r--r--  1 claudio claudio 38015 Fev 11  2005 ./jakarta-tomcat-5.5.9/webapps/hib/WEB-INF/lib/commons-logging-1.0.4.jar
-rw-r--r--  1 claudio claudio 18404 Mar  2  2005 ./jakarta-tomcat-5.5.9/webapps/jboss-profiler/WEB-INF/lib/commons-logging-api.jar
-rw-r--r--  1 claudio claudio 26388 Mar  2  2005 ./jakarta-tomcat-5.5.9/webapps/jboss-profiler/WEB-INF/lib/commons-logging.jar
-rw-r--r--  1 claudio claudio 31774 Mai  3  2005 ./jboss-4.0.2/client/commons-logging.jar
-rw-r--r--  1 claudio claudio 31774 Mai  3  2005 ./jboss-4.0.2/docs/examples/jboss.net/jboss-net.sar/commons-logging.jar
-rw-r--r--  1 claudio claudio 31774 Mai  3  2005 ./jboss-4.0.2/lib/commons-logging.jar
-rw-r--r--  1 claudio claudio 31774 Mai  3  2005 ./jboss-4.0.2/server/all/lib/commons-logging.jar
-rw-r--r--  1 claudio claudio 31774 Mai  3  2005 ./jboss-4.0.2/server/default/lib/commons-logging.jar
-rw-r--r--  1 claudio claudio 31642 Out  5  2003 ./jetty-5.1.4/ext/commons-logging.jar
-rwxrwxr-x  1 claudio claudio 24062 Abr  7  2005 ./jxplorer/jars/dsml/commons-logging.jar
-rw-r--r--  1 claudio claudio 38015 Mai 25  2005 ./libs/jakarta-commons/commons-logging-1.0.4.jar
-rw-r--r--  1 claudio claudio 26202 Jan 25 14:05 ./libs/netbeans-src/libs/external/commons-logging-1.0.4.jar
-rw-rw-r--  1 claudio claudio 31605 Jan 31 14:13 ./netbeans-5.0/mobility7.2/external/commons-logging.jar
-rw-r--r--  1 claudio claudio 26202 Jan 25 14:39 ./netbeans-5.0/ide6/modules/ext/commons-logging-1.0.4.jar
-rw-r--r--  1 claudio claudio 26202 Mar 26  2005 ./netbeans-5.0/enterprise2/jakarta-tomcat-5.5.9/bin/commons-logging-api.jar
-rw-r--r--  1 claudio claudio 31638 Jan 25 14:45 ./netbeans-5.0/enterprise2/modules/ext/jsf/commons-logging.jar
-rw-r--r--  1 claudio claudio 38015 Jan 25 14:46 ./netbeans-5.0/enterprise2/modules/ext/struts/commons-logging.jar
-rw-r--r--  1 claudio claudio 31605 Jan  9 19:15 ./jlibrary/client/plugins/org.eclipse.tomcat_4.1.30.1/commons-logging.jar
-rw-r--r--  1 claudio claudio 22327 Jan  9 19:15 ./jlibrary/client/plugins/org.eclipse.tomcat_4.1.30.1/commons-logging-api.jar
-rw-r--r--  1 claudio claudio 38015 Jan  9 19:15 ./jlibrary/client/plugins/org.jlibrary.client_3.0.0/lib/commons-logging-1.0.4.jar
-rw-r--r--  1 claudio claudio 31605 Ago 25  2004 ./genesis-3.0-EA2/genesis/lib/commons/commons-logging-1.0.3.jar
-rw-r--r--  1 claudio claudio 38015 Ago 25  2004 ./genesis-3.0-EA2/genesis/lib/hibernate/commons-logging-1.0.4.jar
-rw-r--r--  1 claudio claudio 26388 Dez 16 20:19 ./genesis-3.0-EA2/xdoclet/dist/commons-logging.jar
-rw-r--r--  1 claudio claudio 37170 Jan  3 15:49 ./sjsas8/lib/commons-logging.jar
-rw-r--r--  1 claudio claudio 38015 Out  5 23:47 ./axis-1_3/lib/commons-logging-1.0.4.jar
-rw-r--r--  1 claudio claudio 38015 Out  5 23:47 ./axis-1_3/webapps/axis/WEB-INF/lib/commons-logging-1.0.4.jar
-rw-r--r--  1 claudio claudio 26202 Jan  3 13:13 ./apache-tomcat-5.5.15/bin/commons-logging-api.jar
</strong>
</pre>

Depois executei o find com alguns filtros e para indexa&ccedil;&atilde;o na coluna do tamanho do arquivo. 

<pre><strong>
find . -name commons-logging\*.jar -exec ls -l {} \;| gawk '{print $5" "$9}'| sort</strong>
</pre>

<pre><strong>
18404 ./jakarta-tomcat-5.5.9/webapps/jboss-profiler/WEB-INF/lib/commons-logging-api.jar
22327 ./eclipse/plugins/org.eclipse.tomcat_4.1.30.1/commons-logging-api.jar
22327 ./jlibrary/client/plugins/org.eclipse.tomcat_4.1.30.1/commons-logging-api.jar
24062 ./jxplorer/jars/dsml/commons-logging.jar
26202 ./apache-tomcat-5.5.15/bin/commons-logging-api.jar
26202 ./jakarta-tomcat-5.5.9/bin/commons-logging-api.jar
26202 ./libs/netbeans-src/libs/external/commons-logging-1.0.4.jar
26202 ./netbeans-5.0/enterprise2/jakarta-tomcat-5.5.9/bin/commons-logging-api.jar
26202 ./netbeans-5.0/ide6/modules/ext/commons-logging-1.0.4.jar
26388 ./genesis-3.0-EA2/xdoclet/dist/commons-logging.jar
26388 ./jakarta-tomcat-5.5.9/webapps/jboss-profiler/WEB-INF/lib/commons-logging.jar
31605 ./genesis-3.0-EA2/genesis/lib/commons/commons-logging-1.0.3.jar
31605 ./jlibrary/client/plugins/org.eclipse.tomcat_4.1.30.1/commons-logging.jar
31605 ./netbeans-5.0/mobility7.2/external/commons-logging.jar
31638 ./netbeans-5.0/enterprise2/modules/ext/jsf/commons-logging.jar
31642 ./jetty-5.1.4/ext/commons-logging.jar
31774 ./jboss-4.0.2/client/commons-logging.jar
31774 ./jboss-4.0.2/docs/examples/jboss.net/jboss-net.sar/commons-logging.jar
31774 ./jboss-4.0.2/lib/commons-logging.jar
31774 ./jboss-4.0.2/server/all/lib/commons-logging.jar
31774 ./jboss-4.0.2/server/default/lib/commons-logging.jar
37170 ./sjsas8/lib/commons-logging.jar
38015 ./axis-1_3/lib/commons-logging-1.0.4.jar
38015 ./axis-1_3/webapps/axis/WEB-INF/lib/commons-logging-1.0.4.jar
38015 ./genesis-3.0-EA2/genesis/lib/hibernate/commons-logging-1.0.4.jar
38015 ./hibernate-3.1/lib/commons-logging-1.0.4.jar
38015 ./jakarta-tomcat-5.5.9/webapps/blojsom/WEB-INF/lib/commons-logging-1.0.4.jar
38015 ./jakarta-tomcat-5.5.9/webapps/hib/WEB-INF/lib/commons-logging-1.0.4.jar
38015 ./jlibrary/client/plugins/org.jlibrary.client_3.0.0/lib/commons-logging-1.0.4.jar
38015 ./libs/jakarta-commons/commons-logging-1.0.4.jar
38015 ./netbeans-5.0/enterprise2/modules/ext/struts/commons-logging.jar
38015 ./webwork/lib/bootstrap/commons-logging.jar
38015 ./webwork/lib/default/commons-logging.jar
38015 ./webwork/lib/hibernate/commons-logging.jar
38015 ./webwork/lib/spring/commons-logging.jar
</strong>
</pre>

O que nos mostra v&aacute;rias bibliotecas com diferentes tamanhos.

Quais as diferen&ccedil;as entre elas ?

  * Vers&atilde; da API
  * Pacote com interfaces e implementa&ccedil;&atilde;o separados.

O pior de tudo &eacute; o webwork empacotar a mesma biblioteca 4 vezes. tsc tsc.

O que est&aacute; em quest&atilde;o aqui &eacute; o deployment dos programas. Que exigem vers&otilde;es diferencidas das bibliotecas.

Sei que o Mavem resolve o problema em tempo de desenvolvimento, ao unificar em um reposit&oacute;rio as bibliotecas e depend&ecirc;ncias, mas em runtime, isso n&atilde;o existe ainda (ao menos eu desconhe&ccedil;o, caso exista alguma, por favor envie uma mensagem para mim, blob-comments (@) claudius com br)