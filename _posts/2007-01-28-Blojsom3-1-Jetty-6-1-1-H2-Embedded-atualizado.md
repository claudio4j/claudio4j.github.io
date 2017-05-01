---
id: 129
title: Blojsom3.1 + Jetty 6.1.1 + H2 Embedded, atualizado
date: 2007-01-28T18:46:49+00:00
author: Claudio Miranda
layout: post
permalink: /2007/01/Blojsom3-1-Jetty-6-1-1-H2-Embedded-atualizado/
categories:
  - Java
---
Em <a target="_blank" href="http://blog.claudius.com.br/blog/claudio//2006/11/01/Blojsom3-Jetty-6-1-Derby-Embedded.html">novembro escrevi sobre a instalação do sistema de blog Blojsom</a> 3.1 (que usa Spring, Hibernate, banco de dados SQL), usando o <a target="_blank" href="http://jetty.mortbay.org/">Jetty</a> e Apache Derby. Depois de alguns testes, verifiquei que o footprint do derby era um pouquinho maior. Então resolvi testar com o <a target="_blank" href="http://www.h2database.com/">H2</a>, o que demonstrou ser um pouco melhor. 

Então fiz a atualização do sistema de blog Blojsom para a versão 3.1 (usava a versão 2.3). O legal é que no Blojsom, tem uma maneira de migrar o sistema anterior para o atual, considerando tudo o que escrevi, comentários de leitores, imagens, etc.&nbsp; 

A atualização foi realizada com sucesso, a única exceção foi a customização nos templates do velocity. Na atualização os templates customizados foram copiados, (oba!), mas o problema é que algumas macros do velocity não funcionaram adequadamente. Então o que fiz, foi copiar os templates novos (blojsom 3.1) e customizar novamente. Mas isso, foi bem fácil, eram apenas 3 templates. 

O maior problema, foi o seguinte. Na atualização do blojsom, tem alguns passos a seguir e se depois foi feito tudo com sucesso, então o modo de atualização deve ser desabilitado do bean factory (isso mesmo, agora o spring é usado para gerenciar o Blojsom), na próxima reinicialização. 

Então, o espertão aqui, parou o webserver, mudou algumas outras coisas e ESQUECI de desabilitar o modo de atualização. Resultado: ferrou a instalação. Com uma exception: <font face="courier new,courier,monospace">org.hibernate.NonUniqueResultException: query did not return a unique result: 2</font> 

O console de administração não funcionava mais. Ô cabeça de bagre. Mas, nem tudo estava perdido. Como é baseado em SQL, então era só verificar como estavam as tabelas do banco de dados. Como uso o H2, foi só levantar o servidor web e acessar pelo browser (detalhe, tive de colocar a opção <font face="courier new,courier,monospace">-webAllowOthers true</font>) inspecionar as tabelas e verificar alguma inconsistência. 

Verifiquei que foi criado outro usuário e criado uma categoria raiz. Arrumei isso e (ufa) passou tudo a funcionar direitinho. 

O detalhe é que, anteriormente eu fiz um ambiente de teste em meu computador local, onde tudo funcionou direitinho. O único detalhe, quando fui aplicar no meu servidor de produção, foi esquecer de desabilitar o modo de atualização do Blojsom.