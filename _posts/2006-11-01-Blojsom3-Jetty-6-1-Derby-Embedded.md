---
id: 111
title: Blojsom3 + Jetty 6.1 + Derby Embedded
date: 2006-11-01T14:46:47+00:00
author: Claudio Miranda
layout: post
permalink: /2006/11/Blojsom3-Jetty-6-1-Derby-Embedded/
categories:
  - Java
---
 <img src="/resources/claudio/ocean-poweredby.jpg" align="bottom" border="0" hspace="0" vspace="0" /><font size="24">+&nbsp;<br /> <img src="http://www.mortbay.com/images/powered_by_jetty.gif" align="bottom" border="0" hspace="0" vspace="0" /> +&nbsp;<br /> <img src="http://db.apache.org/derby/images/derby-logo-web.png" align="bottom" border="0" hspace="0" vspace="0" /></font> 

  
Uso o <a target="_blank" href="http://wiki.blojsom.com/wiki/display/blojsom3/About+blojsom">Blojsom</a> como sistema de blog, atualmente uso a versão 2.x, enquanto a versão oficial é a 3.x, que usa banco de dados como repositório. A versão 3 possui várias melhorias na usabilidade do produto, correção de problemas e tal. 

Eu quero usar a versão 3 mas estava relutante, pois não quero usar um banco de dados, pois no lugar onde tenho meu website (<a target="_blank" href="http://www.mod3.co.uk/documentation/solaris-zones/zone-pricing">mod3.co.uk</a>) quero restringir o consumo de recursos. Então verifiquei que o <a target="_blank" href="http://db.apache.org/derby/derby_downloads.html">Apache Derby</a> pode funcionar no modo embutido (<a target="_blank" href="http://db.apache.org/derby/docs/10.2/workingwithderby/twwdactivity3_Setup.html">embedded</a>), onde não é necessário usar um serviço servidor (daemon) com porta. 

Enão fiz um teste, que funcionou tranquilo, bastou ajustar o script de criação de tabelas e algumas outras coisas. 

Fiz um pequeno <a title="Instalação do Blojsom 3 + Jetty 6.1 + Derby Embedded" target="_blank" href="http://wiki.claudius.com.br/wiki/InstalacaoBlojsom3ComJetty6DerbyEmbedded">howto (em inglês) para essa configuração</a> (também está no [howto do blojsom](http://wiki.blojsom.com/wiki/display/blojsom3/Installation)), se você precisar de uma versão em português, é só me avisar.

&nbsp; 

<more/>