---
id: 144
title: Desabilitar o login gráfico no solaris 10
date: 2007-03-21T13:00:59+00:00
author: Claudio Miranda
layout: post
permalink: /2007/03/Desabilitar-o-login-grafico-no-solaris-10/
categories:
  - Dicas
---
Tenho usado o Solaris em uma vmware, e como preciso apenas de aplicações servidoras, e poupar o uso computacional de minha maquina, então desabilito o que não preciso, como sendmail, ftp e o login gráfico. 

No caso do login gŕafico, para desabilitar, basta invocar o comando svcadm, como abaixo: 

<pre>svcadm disable svc:/application/graphical-login/cde-login:default</pre>

Veja outra [dica para habilitar/desabilitar serviços no solaris 10](http://wiki.claudius.com.br/wiki/GerenciamentoDeServicosSolaris10)&nbsp;