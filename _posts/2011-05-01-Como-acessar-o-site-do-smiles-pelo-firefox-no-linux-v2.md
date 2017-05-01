---
id: 251
title: Como acessar o site do smiles pelo firefox no linux (v2)
date: 2011-05-01T12:58:50+00:00
author: Claudio Miranda
layout: post
permalink: /2011/05/Como-acessar-o-site-do-smiles-pelo-firefox-no-linux-v2/
categories:
  - Dicas
---
Há [algumas horas escrevi como fazer isso](http://www.claudius.com.br/blog/claudio/2011/05/01/Como-acessar-o-site-do-smiles-pelo-firefox-no-linux), usando o firebug, e para cada reload da página, o div tem de ser removido, uma chateação.
  
  


Pois vi uma maneira mais simples e deixar automático para cada visita. 

É necessário usar outra extensão do firefox que também já é bastante útil, o [adblock](https://addons.mozilla.org/en-US/firefox/addon/adblock-plus/), [já escrevi sobre ele antes](http://www.claudius.com.br/blog/claudio/2005/06/13/ADBlock_o_melhor.html), para despoluir as páginas visitadas. 

O &#8220;User Agent Switcher&#8221; cotinua necessário. 

Após instalar o adblock e reiniciar o firefox, crie a seguinte regra de exclusão no adblock 

<pre>clientes.smiles.com.br##div#dvBusy
</pre>

Veja uma imagem de como deve ser a regra no adblock.

![](/resources/claudio/20110501_adblock.png)

Pronto, está feito. Se quiser pode remover o firebug.