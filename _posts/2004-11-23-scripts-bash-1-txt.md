---
id: 26
title: '&Uacute;teis scripts bash'
date: 2004-11-23T01:30:01+00:00
author: Claudio Miranda
layout: post
permalink: /2004/11/scripts-bash-1-txt/
categories:
  - Dicas
---
Alguns scripts bash que uso regularmente e que ajudam um bocado.

**1) Script bash para pesquisar uma classe em arquivos jar**

## <pre>#!/bin/sh

if [ $# -lt 1 ] ; then
    echo "Uso: "
    echo "     findJavaClass  [-r] directory ClassName "
    echo ""
    echo "     -r search into directory, wildcard can be used"
    echo ""
    exit 1
fi

if [ "$1" ] && [ $1 = '-r' ] ; then
    for n in `find $2 -name \*.jar`; do
        echo "--    "$n
        jar tf $n|grep $3;
    done
else
    for n in $1/*.jar; do
        echo "--    "$n
        jar tf $n|grep $2;
    done
fi

</pre>

**2) Mostra portas usadas no sistema operacional e qual processo usa a porta (necessita permissão de root)**

## <pre>#!/bin/sh

LANGUAGE=en sudo netstat -anptuw
echo "--------------------------------------------------------------"

if [ "$1" ] && [ $1 = '-a' ] ; then
    sudo lsof -i -P
    echo "--------------------------------------------------------------"
fi

</pre>

**3) Normalmente &eacute; necess&aacute;rio mostrar apenas algumas linhas de algum arquivo, e n&atilde;o &eacute; desej&aacute;vel mostrar   
desde as primeiras linhas e fazer page down at&eacute; a linha desejada, ent&atilde; este script mostra   
apenas as 10 linhas antes e depois do n&uacute;mero de linhas especificado. Resumindo, mostra apenas o que interessa.**

## <pre>#!/bin/sh

line=`echo $1+10|bc`

head -$line $2 |tail -20
</pre>

**4) Captura todos os pacotes tcp que traf&eacute;gam na interface de rede especificada   
no argumento (necessita permiss&atilde;o de root).**

## <pre>#!/bin/sh

sudo tcpdump  -Xxl -vvv -i $1  -s 1024
</pre>