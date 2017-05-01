---
id: 219
title: Ferramentas de diagnóstico em performance na prática
date: 2008-09-09T02:57:58+00:00
author: Claudio Miranda
layout: post
permalink: /2008/09/Ferramentas-de-diagnostico-em-performance-na-pratica/
categories:
  - Java
---
<img align="right"  src="/resources/claudio/080909_executivethree.jpg" alt="3" border="0" hspace="80" />

Tenho efetuado a palestra sobre diagnóstico em problemas de performance, desde 2006 em diversos eventos.

Pelo feedback que recebo, percebo que este é um assunto de interesse para um numeroso grupo de profissionais.

Então, é por isso que você que é interessado em entender mais sobre performance, garbage collector, thread pools, thread dumps e memory dumps, deve comparecer no próximo dia 12 (sexta-feira) as 9h no Senac, onde ocorre o JustJava. Pois irei realizar um workshop na prática sobre este assunto. 

O nome é "<a href="http://www.soujava.org.br/display/v/Grade+de+Palestras" linktext="Diagnóstico e Resolução de Problemas de Performance em Java|Resumos#9010" linktype="raw">Diagnóstico e Resolução de Problemas de Performance em Java</a>", é requerido trazer o laptop para máximo aproveitamento.

O workshop (hands-on lab), será um misto de palestra com exercícios sobre o tema. Será seguido (tentativa) o seguinte roteiro:

  * Explicação sobre um tópico
  * Demonstração
  * Fazer com que os atendentes resolvem um exercício

Os tópicos serão

  * Gerenciamento de memória do Java
  * Ferramentas para diagnóstico
  * Thread Dumps
  * Memory Dumps
  * Ferramentas para profiling

Para um máximo rendimento para o atendente, é necessário seguir alguns pontos:

  * Usar sistema operacional Linux (pode ser em uma VM)
  * Ter interface wireless funcionando
  * **Trazer instalado e funcionando** os seguintes sistemas
  * [Sun JDK 6 Update 10 RC](http://java.sun.com/javase/downloads/index.jsp) (invoque o bin/jvisualvm e instale todos os plugins)
  * [NetBeans 6.1  
](http://download.netbeans.org/netbeans/6.1/final/) 
  * [Glassfish v2 ur 2](https://glassfish.dev.java.net/downloads/v2ur2-b04.html)
  * [IBM Heap Analyzer](http://www.alphaworks.ibm.com/tech/heapanalyzer)
  * [IBM Thread Dump Analyzer](http://www.alphaworks.ibm.com/tech/jca)
  * [Thread Dump Analyzer](https://tda.dev.java.net/#download)
  * [Apache JMeter](http://jakarta.apache.org/site/downloads/downloads_jmeter.cgi)
  * 

Configurem as variáveis JAVA\_HOME e PATH=$JAVA\_HOME/bin

O uso do Linux não é obrigatório, mas **facilita muito**, e irei basear meus exemplos nele.

Note, que o tempo do workshop não será prejudicado, por aqueles que não possuem os sistemas instalados. Pois o tempo é curto para muito conteúdo de não fácil absorção.

Não posso esperar pela próxima sexta, para divertir com thread dumps, pools estourando e memória escorrendo pelos buracos do laptop.