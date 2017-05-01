---
id: 174
title: Como encontrar uma classe ?
date: 2007-07-30T02:56:18+00:00
author: Claudio Miranda
layout: post
permalink: /2007/07/Como-encontrar-uma-classe/
categories:
  - Dicas
---
<img align="right" src="/resources/claudio/tips_icon.gif" alt="Dicas" hspace="80" />
  
Nesta dica mostrarei duas dicas que me ajudam muito no dia a dia. 

**1) Encontrar em qual biblioteca está uma classe**&nbsp; 

Existem diversas situações onde é necessário encontrar em qual biblioteca encontra-se uma determinada classe Java. 

[Em 2004 coloquei uma dica de um script bash que resolve isso](http://www.claudius.com.br/blog/claudio/2004/11/22/scripts%20bash%201.txt). Esse script mostra todos os arquivos que ele vasculhou para procurar a classe, mesmo que a classe não estivesse no arquivo, ele seria mostrada mesmo assim, causando desperdício de tempo e de tela. 

Então aproveitei um tempinho e arrumei o script, onde é mostrado apenas o arquivo que contém a classe procurada e ainda arrumei a impressão da tela.
  
  


<more/>

<pre>#!/bin/sh

usage="Uso:        findJavaClass directory ClassName   "

if [ $# -lt 2 ] ; then
    echo $usage
    exit 1
fi

if [ -d $1 ] ; then
    FIND_CMD="find $1"
else 
    echo "Diretorio nao existe"
    exit 1    
fi

$FIND_CMD -name \*.jar | while read jar_file ; 
do
    found_class=`unzip -l $jar_file | awk '{print $4}' | grep  $2`
    num_classes=`echo $found_class | wc -c`
    if [ $num_classes -gt 1 ] ; then 
        echo ""
        echo "Arquivo:"
        echo "    $jar_file"
        echo "Classes:"
        echo $found_class | sed 's/\ /\n/g' | sed 's/^.*/\ \ \ \ &/g'
    fi
done

  </pre>

E o um resultado como exemplo: 

<pre>$ findJavaClass ~/javaSoftware/netbeans-5.5.1/ide7/modules/ext/jaxws21/ Task

Arquivo:
    /home/claudio/javaSoftware/netbeans-5.5.1/ide7/modules/ext/jaxws21/http.jar
Classes:
    sun/net/httpserver/ServerImpl$ServerTimerTask.class

Arquivo:
    /home/claudio/javaSoftware/netbeans-5.5.1/ide7/modules/ext/jaxws21/jaxb-xjc.jar
Classes:
    com/sun/istack/tools/ProtectedTask$AntElement.class
    com/sun/istack/tools/ProtectedTask.class
    com/sun/tools/jxc/AptBasedTask$1.class
    com/sun/tools/jxc/AptBasedTask$AptAdapter.class
    com/sun/tools/jxc/AptBasedTask$InternalAptAdapter.class

  </pre>

**2) Como mostrar o conteúdo de um arquivo que está compactado ?** 

Quantas vezes por dia você descompacta um arquivo só para olhar o conteúdo do manifest ?
    
    


Então segue mais uma dica, onde não é necessário descompactar o arquivo. 

<pre>$ unzip -c /home/claudio/javaSoftware/netbeans-5.5.1/ide7/modules/ext/jaxws21/jaxb-xjc.jar META-INF/MANIFEST.MF
  </pre>