---
id: 97
title: Ambiente em UTF-8
date: 2006-03-20T18:51:23+00:00
author: Claudio Miranda
layout: post
permalink: /2006/03/Ambiente-em-UTF-8/
categories:
  - Dicas
---
Alguns dias atrás resolvi colocar o meu ambiente de desenvolvimento compatível com UTF-8, necessariamente o sistema operacional e as ferramentas precisam ser configurados para usar UTF-8 como padrão. 

Sistema operacional (Mandriva Linux) 

Em <font face="monospace">/etc/sysconfig/keyboard</font>, alterar a propriedade

<pre>KBCHARSET=UTF-8</pre></p> 

Usei o draklocale para configuração do teclado

Ferramentas
  
  
NetBeans: Menu Tools -> Options -> Advanced Options -> Editing -> Java Sources -> Default encoding. Informe UTF-8

&#8211; Apache Tomcat 5.5.x
  
  
&#8212; Em \$CATALINA_HOME/conf/server.xml no connector da porta usada (por exemplo 8080, informe o atributo URIEncoding=&#8221;UTF-8&#8243;, como no exemplo:
  
  
&nbsp;
  


<pre>&lt;Connector port="8080" maxHttpHeaderSize="8192"
&nbsp;maxThreads="150" minSpareThreads="25" maxSpareThreads="75"
&nbsp;enableLookups="false" redirectPort="8443" acceptCount="100"
&nbsp;connectionTimeout="20000" disableUploadTimeout="true"&nbsp; URIEncoding="UTF-8"/&gt;
</pre></p> 

&#8211; WebWork.
  
  
&#8212; Informar no freemarker.properties
  
  
<font face="courier new,courier,monospace">default_encoding=UTF-8 </font>
  
  
&#8211; webwork.properties
  


<pre>webwork.i18n.encoding=UTF-8</pre>

  
&#8211; Hibernate
    
  
&#8212; Extensão do dialect do MySQL para que a criação das tabelas sejam UTF-8 compatíveis
    
  
fico devendo aqui&#8230;
  
  


  
por enquanto é isso, caso você lembre de algo, me avise.

Envie um email para claudio(*)claudius com br, o sistema de moderação foi desabilitado por avalanche de spam.