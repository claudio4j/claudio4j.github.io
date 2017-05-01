---
id: 108
title: Download de streaming de vídeos com mplayer
date: 2006-10-27T17:56:56+00:00
author: Claudio Miranda
layout: post
permalink: /2006/10/Download-de-streaming-de-v-deos-com-mplayer/
categories:
  - Dicas
---
Algumas vezes desejo assistir webcasts que estão no formato realplay (.rm, .ram). Normalmente estes vídeos são streaming e é possível apenas visualizar com o realplayer e deve estar on-line.

Há alguns anos percebi que com o [mplayer](http://www.mplayerhq.hu/design7/news.html) é possível capturar o vídeo e armazenar em um arquivo (de fato, realizar um dump). Sempre esquecia de colocar essa dica, pois as vezes sempre tem alguém que pergunta &#8220;Como fazer o download de streaming de vídeos ?&#8221;.

Um exemplo desses são os [vídeos da Sun, como os do JavaOne](http://java.sun.com/javaone/sf/sessions/general/index.jsp).

Na página de vídeos do JavaOne, consta:

<pre style=" background: #f7f7f7;
 border: 1px solid #d7d7d7;
 margin: 1em 1.75em;
 padding: .25em;
 overflow: auto;">http://www.sun.com/jsp_utils/ipr.jsp?elink=http://mfile.akamai.com/9191/rm/feedroomgen.download.akamai.com/9191/t_assets/20060807/20cdd81b95a1cb9caf293435fe476fdf0d00c9fe.rm?s=sun_n&c=Hidden2&ilink=http://webcast-mpk1.sfbay.sun.com/interchange/index.html?06D00627_10_200.rm</pre>

Basta realizar o download e ver o conteúdo, que deve conter as URLs onde estão de fato os vídeos:

<pre style=" background: #f7f7f7;
 border: 1px solid #d7d7d7;
 margin: 1em 1.75em;
 padding: .25em;
 overflow: auto;">rtsp://a225.v91917.c9191.g.vr.akamaistream.net/ondemand/7/225/9191/v0001/feedroomgen.download.akamai.com/9191/t_assets/20060807/bf59a1e3ca50b8ab25b19ffbe4ecf063ef0f6e3f.rm</pre>

Então basta usar o mplayer para efetuar o download:

sintaxe:

<pre style=" background: #f7f7f7;
 border: 1px solid #d7d7d7;
 margin: 1em 1.75em;
 padding: .25em;
 overflow: auto;">mplayer -dumpstream  &lt;URL:RTSP> -dumpfile &lt;arquivo de saida.rm></pre>

Para efetuar o download do vídeo acima:

<pre style=" background: #f7f7f7;
 border: 1px solid #d7d7d7;
 margin: 1em 1.75em;
 padding: .25em;
 overflow: auto;">mplayer -dumpstream rtsp://a225.v91917.c9191.g.vr.akamaistream.net/ondemand/7/225/9191/v0001/feedroomgen.download.akamai.com/9191/t_assets/20060807/bf59a1e3ca50b8ab25b19ffbe4ecf063ef0f6e3f.rm -dumpfile saida.rm</pre>

Fiz um script para isso:

É necessário o browser texto [links](http://links.sourceforge.net/) 

<pre style=" background: #f7f7f7;
 border: 1px solid #d7d7d7;
 margin: 1em 1.75em;
 padding: .25em;
 overflow: auto;">#!/bin/sh

echo "Download da URL: "$1
echo ""
rtsp_file=`links -dump $1 | grep rtsp`
mplayer -dumpstream  $rtsp_file -dumpfile $2
</pre>