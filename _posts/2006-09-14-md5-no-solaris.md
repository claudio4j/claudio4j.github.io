---
id: 105
title: md5 no solaris
date: 2006-09-14T14:58:47+00:00
author: Claudio Miranda
layout: post
permalink: /2006/09/md5-no-solaris/
categories:
  - Dicas
---
Efetuei algumas transferências para o solaris, e sempre verifico com md5sum para certificar se a cópia foi bem sucedida.

No entanto não consegui encontrar um md5sum para solaris, nem no [sunfreeware.com](http://www.sunfreeware.com/indexintel10.html) nem no [blastwave](http://cr.yp.to/docs/unixport.html). Estava pensando em criar um programa em java para calcular o md5. Foi então que em uma busca do google encontrei sobre algumas informações sobre [portabilidade no unix](http://cr.yp.to/docs/unixport.html), uma dica para usar o comando openssl.

Veja as possibilidades de cáculo de hash com openssl:

<pre>-md5 to use the md5 message digest algorithm (default)
-md4 to use the md4 message digest algorithm
-md2 to use the md2 message digest algorithm
-sha1 to use the sha1 message digest algorithm
-sha to use the sha message digest algorithm
-sha256 to use the sha256 message digest algorithm
-sha512 to use the sha512 message digest algorithm
-mdc2 to use the mdc2 message digest algorithm
</pre>

E como usar o comando openssl para calcular o hash

<pre>$ openssl dgst -sha1 all.tar
SHA1(all.tar)= 2c07f63405a39f78ce78564a5eb07c741bd7c281
</pre>

E no linux em geral é usado o md5sum ou sha1sum.

<pre>$ sha1sum all.tar
2c07f63405a39f78ce78564a5eb07c741bd7c281  all.tar
</pre>