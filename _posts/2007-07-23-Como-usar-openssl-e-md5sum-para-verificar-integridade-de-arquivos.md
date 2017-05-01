---
id: 170
title: Como usar openssl e md5sum para verificar integridade de arquivos
date: 2007-07-23T03:56:22+00:00
author: Claudio Miranda
layout: post
permalink: /2007/07/Como-usar-openssl-e-md5sum-para-verificar-integridade-de-arquivos/
categories:
  - Dicas
---
[<img border="0" src="/resources/claudio/070722_doctorfun_kernel_panic.jpg" alt="Kernel Panic" />](http://www.ibiblio.org/Dave/drfun.html)

<more>

Sempre preciso copiar arquivos entre solaris, linux e windows. Para verificar se o arquivo foi copiado com sucesso, uso um algoritmo aplicado no arquivo que faço a cópia, que efetua um cálculo único. Esse algoritmo é o MD5. Para invocar o cálculo desse algoritmo uso uma ferramenta no linux chamado <font face="monospace">md5sum</font>. 

Essa ferramenta, efetua o cálculo e a verificação de integridade de um arquivo. 

_**Por que usar verificação de integridade na cópia de arquivos ?** 
    
  
_ Pois a cópia pode ter sido corrompida na transferência.
  
  


Então segue um exemplo de usar o md5sum 

Criar o hash 

<pre>md5sum arquivo.tar &gt; arquivo.tar.md5</pre>

Verificar o hash 

<pre>md5sum -c arquivo.tar.md5</pre>

A verificação do hash, usa o seguinte formato para verificação 

<pre>534a15536aa0152e178361983c678cc0&nbsp; arquivo.tar.md5
</pre>

O motivo desta dica, não é necessariamente sobre o md5sum, mas porque essa ferramenta não está disponível nativamente no solaris, onde uso o openssl.
  
  


No solaris, para criar o hash, uso openssl da seguinte maneira 

<pre>openssl dgst -md5 &lt;arquivo&gt;</pre>

Que gera um resultado da seguinte maneira 

<pre>$ openssl dgst -md5 list.conf
MD5(list.conf)= e5c8ebe8e2113448fd318328cf5ca582</pre>

Que é diferente do md5sum, então não é possível realizar a verificação de integridade usando checksums md5. 

Por isso criei um script bash, para solaris que faz uma tarefa semelhante do utilitário md5sum. 

</more>

[Download do script bash md5sum_solaris.sh](/resources/claudio/md5sum_solaris.sh.txt)

Dependências: openssl, awk, sed 

O código é o seguinte: 

<pre>#!/bin/bash

if [ "$1" ] ; then
    if [ $1 = '-c' ] && [ $2"x" != 'x'  ] ; then
        shift
        cat $1 | while read hash_line
        do
            hash_value=`echo $hash_line | awk '{print $1}'`
            filename=`echo $hash_line | awk '{print $2}'`
            echo -n $filename": "
            if [ -f "$filename" ] ; then
                hash_var=`openssl dgst -md5 $filename | awk '{print $2}'` ;
                if [ $hash_var == $hash_value ] ; then
                    echo "OK"
                else
                    echo "FAILED"
                fi
            else
                echo "FAILED: No such file or directory"
            fi
        done
    else
        openssl dgst -md5 $*  |  sed 's/[\(\)=]//g;s/MD5//g' | awk '{print $2"  "$1}'
    fi
else 
    echo "Usage:
    $0 -c hashs.md5      to verify checksums
    $0  &lt;file>           to create checksums
    "
fi
</pre>