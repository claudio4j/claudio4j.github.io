---
id: 128
title: Manuseio de certificados SSL fácil
date: 2007-01-26T04:03:27+00:00
author: Claudio Miranda
layout: post
permalink: /2007/01/Manuseio-de-certificados-SSL-f-cil/
categories:
  - Dicas
---
Sempre tenho de criar certificados e CA para efetuar testes em conexões SSL, e para isso uso o OpenSSL, que é um toolkit completo para trabalhar com SSL (certificados, chaves públicas e privadas, formatos, etc.). Para isso uso o utilitário por linha de comando CA.sh (wrapper para o CA.pl). 

Então hoje encontrei um programinha gráfico que faz essa tarefa toda, é o <a target="_blank" href="http://tinyca.sm-zone.net/">TinyCA</a>. 

<a href="/resources/claudio/070126_tinyca.png" target="_blank"><br /> <img src="/resources/claudio/070126_tinyca_sm.png" align="bottom" border="0" hspace="0" vspace="0" /></a> 

Com ele não é mais necessário digitar <font face="courier new,courier,monospace">CA.sh -newca</font> por exemplo.&nbsp; 

Ele tem todas as funcionalidades que preciso e ainda permite customização na invocação do openssl, realmente achei muito bom o programa. Recomendo.