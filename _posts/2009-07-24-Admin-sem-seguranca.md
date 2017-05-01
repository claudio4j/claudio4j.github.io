---
id: 226
title: Admin sem segurança
date: 2009-07-24T16:34:41+00:00
author: Claudio Miranda
layout: post
permalink: /2009/07/Admin-sem-seguranca/
categories:
  - Dicas
---
<img src="/resources/claudio/20090724-fail-security-guard.jpg" hspace="80" align="right" border="0" />

Vejam alguns consoles do JBoss em instalações na internet. 

<pre>http://www.google.com/search?hl=all&q=inurl%3A%22%2Fjmx-console%2F%22+%22JMX+MBean+View%22</pre>

Esta pesquisa no google irá procurar por todas as urls que tenham &#8220;/jmx-console/&#8221; e a string completa &#8220;JMX MBean View&#8221;. 

Se quiserem ver sites brasileiros, adicionem a opção <font face="monospace">site:com.br</font> ou <font face="monospace">site:gov.br</font>

O console do JBoss tem esta String no console de administração, que visualiza os nomes JNDI. 

Os administradores de sistema dos sites resultados da pesquisa deveriam habilitar a segurança do console de administração. 

<a target="_blank" href="http://www.jboss.org/community/wiki/securethejmxconsole">Vejam como habilitar o console de segurança</a>. 

Já usei o JBoss em diversos projetos desde 2002 e sempre que o projeto é colocado em produção, o console admin é removido ou é habilitado a segurança na autenticação. 

Leiam isso apenas como aviso de como melhorar as instalações de sistemas. Acessei alguns consoles admin, para ver se a segurança estava realmente desabilitada. Não fiz nenhuma alteração no sistema. Recomendo que vocês também não o façam.