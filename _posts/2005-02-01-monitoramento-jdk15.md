---
id: 42
title: Monitoramento da JVM (JDK 1.5)
date: 2005-02-01T22:27:53+00:00
author: Claudio Miranda
layout: post
permalink: /2005/02/monitoramento-jdk15/
categories:
  - Java
---
<a target="_blank" href="http://java.sun.com/developer/technicalArticles/J2SE/jconsole.html">Artigo sobre uso do JConsole</a>,
  
do JDK 1.5 para monitoramento de v&aacute;rios aspectos da JVM:
  
mem&oacute;ria, threads, GC, classloaders. Com gr&aacute;ficos e
  
contadores. Pode conectar-se a aplica&ccedil;&otilde;es java 1.5 locais
  
e remotas. Na vers&atilde;o 1.5 estas <a target="_blank" href="http://java.sun.com/j2se/1.5.0/docs/tooldocs/index.html#manage">ferramentas de monitoramento</a> e o suporte a <a target="_blank" href="http://java.sun.com/j2se/1.5.0/docs/guide/management/">monitoramento atrav&eacute;s da API</a>
  
trouxeram para a JVM algo que j&aacute; era reclamando a muito tempo,
  
uma maneira de monitorar as caracter&iacute;sticas internas da JVM.

A especifica&ccedil;&atilde;o J2EE 1.4 tamb&eacute;m possui <a target="_blank" href="http://java.sun.com/j2ee/1.4/docs/api/javax/management/package-summary.html">aspectos de monitoramento</a>,
  
tanto do container como das aplica&ccedil;&otilde;es instaladas.
  
Informa&ccedil;&otilde;es do pool de conex&otilde;es e EJBs, recursos
  
JCA, taxas de crescimento e consumo. Ferramentas muito importantes em
  
cen&aacute;rios corporativos onde existem muitas m&aacute;quinas a
  
serem administradas e o administrador n&atilde;o &eacute; entende quase
  
nada de J2EE. O monitoramento &eacute; exposto atrav&eacute;s de JMX,
  
que pode ter um consumidor baseado em SNMP, protocolo usado nas
  
ferramentas de monitoramento de mercado, como o Tivoli.