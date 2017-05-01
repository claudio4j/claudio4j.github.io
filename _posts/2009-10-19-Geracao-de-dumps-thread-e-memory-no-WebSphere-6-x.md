---
id: 233
title: Geração de dumps (thread e memory) no WebSphere 6.x
date: 2009-10-19T16:49:01+00:00
author: Claudio Miranda
layout: post
permalink: /2009/10/Geracao-de-dumps-thread-e-memory-no-WebSphere-6-x/
categories:
  - Java
---
Segue uma dica de como extrair um dump de threads e memória do WebSphere, funciona tanto em unix como em windows. 

Acessar a interface administrativa e configurar os parametros 

Navegação
  
  


<pre>Servers -&gt; Application Servers -&gt; Server1 -&gt; Process Definition -&gt; Java Virtual Machine -&gt; Generic JVM arguments</pre>

Parâmetro:

<pre>-Xdump:system+heap+java:events=gpf+throw+user,filter=java/lang/OutOfMemoryError,request=exclusive+prepwalk</pre>

Navegação:

<pre>Servers -&gt; Application Servers -&gt; Server1 -&gt; Process Definition &gt; Environment Entries</pre>

Parâmetros:

<pre>IBM_HEAPDUMP=true
IBM_HEAPDUMP_OUTOFMEMORY=true
IBM_HEAPDUMPDIR=c:\temp
</pre>

Agora criar um atalho para facilitar o acesso ao script wsadmin, no diretório <font face="courier new,courier,monospace">WAS_HOME/bin</font>. 

**Windows** 

<pre>* _wsadmin_comm.bat
wsadmin -conntype SOAP -user admin -password senha_do_admin %*
</pre></p> 

**Unix** 

<pre>* _wsadmin_comm.sh
wsadmin -conntype SOAP -user admin -password senha_do_admin $*
</pre>

Crie scripts JACL (script baseado em TCL) para invocação dos comandos. 

**Memory Dump**
  
  


<pre>* heapdump.jacl
set jvm [$AdminControl queryNames type=JVM,*]
$AdminControl invoke $jvm generateHeapDump
</pre>

 **Thread dump**

<pre>* threaddump.jacl
set jvm [$AdminControl queryNames type=JVM,*]
$AdminControl invoke $jvm dumpThreads
</pre>

Para gerar os dumps basta invocar os comandos 

<pre>_wsadmin_comm.sh -f heapdump.jacl</pre>

Veja no diretório especificado em IBM_HEAPDUMPDIR ou no AppServer01 se os arquivos foram gerados em um deles. 

Depois use ferramental adequado para analisar os dumps (<a target="_blank" href="http://eclipse.org/mat/">Eclipse Memory Analyzer</a>, <a target="_blank" href="http://www.alphaworks.ibm.com/tech/jca">IBM Thread Dump Analyzer</a>).