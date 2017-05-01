---
id: 224
title: Como reduzir espaço em disco do JDK em ambiente servidor
date: 2009-03-06T01:22:02+00:00
author: Claudio Miranda
layout: post
permalink: /2009/03/Como-reduzir-espaco-em-disco-do-JDK-em-ambiente-servidor/
categories:
  - Java
---
No decorrer dos anos, as novas vers&otilde;es do JDK estavam acompanhadas de novas funcionalidades, bibliotecas, etc.

E sempre existiram coment&aacute;rios na comunidade, sobre o tamanho do JDK e o espa&ccedil;o ocupado pelo JDK, ap&oacute;s a instala&ccedil;&atilde;o.

Pois vou dar uma dica de como remover arquivos desnecess&aacute;rios do JDK em ambiente servidor. Na maioria das vezes, isso s&oacute; ser&aacute; necess&aacute;rio se uma economia de 100MB for importante. Ou instala&ccedil;&otilde;es em rede com imagem, para poupar tempo de download para outras esta&ccedil;&otilde;es.

A dica &eacute; baseada em um ambiente Linux 32 bits, com uma instala&ccedil;&atilde;o padr&atilde;o do JDK 6 update 12.

A instala&ccedil;&atilde;o padr&atilde;o ocupa um espa&ccedil;o de 239 MB. Veja a ocupa&ccedil;&atilde;o de espa&ccedil;o nas vers&otilde;es anteriores do JDK.

<pre>82M     j2sdk1.4.2_18
141M    jdk1.5.0_16
239M    jdk1.6.0_12
</pre>

Uma boa evolu&ccedil;&atilde;o no espa&ccedil;o ocupado.

Veja os arquivos que podem ser removidos, e o tamanho que ser&aacute; economizado em disco.

<pre>7.9M    sample/
20M     demo/
19M     src.zip
4.3M    db/demo/
18M     db/docs/
2.1M    db/javadoc/
96K     db/lib/derbyLocale_cs.jar
100K    db/lib/derbyLocale_de_DE.jar
92K     db/lib/derbyLocale_es.jar
100K    db/lib/derbyLocale_fr.jar
96K     db/lib/derbyLocale_hu.jar
92K     db/lib/derbyLocale_it.jar
108K    db/lib/derbyLocale_ja_JP.jar
104K    db/lib/derbyLocale_ko_KR.jar
96K     db/lib/derbyLocale_pl.jar
92K     db/lib/derbyLocale_pt_BR.jar
120K    db/lib/derbyLocale_ru.jar
96K     db/lib/derbyLocale_zh_CN.jar
96K     db/lib/derbyLocale_zh_TW.jar
23M     lib/visualvm/
<strong>94M     total</strong>
</pre>

Uma economia de 94 MB

Estes arquivos n&atilde;o s&atilde;o necess&aacute;rios em ambiente servidor. Com exce&ccedil;&atilde;o de alguns arquivos do visualvm, que possui as bibliotecas nativas para efetuar profiling remoto, mas isso geralmente n&atilde;o &eacute; necess&aacute;rio em ambiente servidor de testes ou produ&ccedil;&atilde;o, ou algu&eacute;m faz prifiling em produ&ccedil;&atilde;o ?

No caso dos arquivos de i18n do <tt>derby</tt>, prefiro usar os termos em ingl&ecirc;s, pois acho conveniente que os termos t&eacute;cnicos sejam em ingl&ecirc;s ([meu ponto de vista sobre o caso](http://www.claudius.com.br/blog/claudio/2008/04/19/Tradu%C3%A7%C3%A3o-de-aplica%C3%A7%C3%B5es)).