---
id: 189
title: Conversão de charset para UTF-8
date: 2007-11-05T13:46:47+00:00
author: Claudio Miranda
layout: post
permalink: /2007/11/Conversao-de-charset-para-UTF-8/
categories:
  - Dicas
---
Em ambientes de desenvolvimento heterogêneos, onde existem diferentes sistemas operacionais e IDEs, é comum encontrar problemas de caracteres com encoding diferentes, como ISO-8859-1, UTF-8, etc.
  
  


No projeto que trabalho atualmente, existem windows e linux (por enquanto não tem apple), então é comum existirem arquivos com ISO-8859-1, ASCII e UTF-8. 

Então não é uma boa idéia gravar arquivos .java, vogais com acentos e gravar em ISO-8859-1 e outro colega abrir esse arquivo em seu linux com UTF-8, uma bagunça. 

Então segue um script para linux que verifica os encodings dos arquivos e outro que converte para UTF-8. Note que o script não mostra o arquivo se ele já estiver em UTF-8. 

É necessário o utilitário [konwert](http://sourceforge.net/projects/konwert/). Já usei anteriormente o recode e iconv, mas achei o konwert mais prático. E ele oferece uma opção interessante, onde ele tenta descobrir qual o encodingo do arquivo, através da opção <font face="monospace">any/pt/all-test</font>
  
  


### Script 1 &#8211; checagem do encoding
  


<pre>#!/bin/sh

if [ $# -lt 1 ] ; then
    echo ""
    echo " Informe um diretório para pesquisar os arquivos .java "
    exit 1
fi

find $1 -name \*.java -exec file {} \; | egrep -v 'ASCII|UTF' | while read s; do 
	ff=`echo $s | awk -F ':' '{print $1}'`;  
	file $ff; 
	echo " charset   "; konwert any/pt/all-test  $ff; 
done
</pre>

### Script 2 &#8211; Conversão para UTF-8
  


<pre>#!/bin/sh

if [ $# -lt 1 ] ; then
    echo ""
    echo " Informe um diretório para converter os arquivos .java para UTF-8"
    exit 1
fi

find . -name \*.java -exec file {} \; | grep 8859 | while read s; do 
	ff=`echo $s | awk -F ':' '{print $1}'`;   
	konwert cp1252-utf8 -O  $ff; 
done                      
</pre>

No script de conversão é usado a opção -O, que faz com que o arquivo original seja trocado pelo arquivo com encoding UTF-8&nbsp;