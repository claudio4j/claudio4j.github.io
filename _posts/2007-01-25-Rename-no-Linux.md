---
id: 127
title: Rename no Linux
date: 2007-01-25T03:03:58+00:00
author: Claudio Miranda
layout: post
permalink: /2007/01/Rename-no-Linux/
categories:
  - Dicas
---
Há alguns dias precisei renomear vários arquivos em um diretório, que obedeciam algum padrão no nome.&nbsp; 

Para fazer a operação de renomear em vários arquivos, eu já usei scripts com laço <font face="courier new,courier,monospace">for</font>.&nbsp; Mas desta vez, quis usar o comando <font face="courier new,courier,monospace">rename</font>, e foi super simples, pois ele aceita uma expressão regular: 

<pre>rename 's/_-_//' *.mp3</pre>

De vários arquivos, a string \_-\__ tinha de ser removida. Faça um <font face="courier new,courier,monospace">man rename</font>. Recomendo.