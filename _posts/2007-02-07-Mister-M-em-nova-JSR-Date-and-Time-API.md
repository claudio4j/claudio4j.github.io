---
id: 132
title: Mister M em nova JSR Date and Time API
date: 2007-02-07T15:14:55+00:00
author: Claudio Miranda
layout: post
permalink: /2007/02/Mister-M-em-nova-JSR-Date-and-Time-API/
categories:
  - Java
---
<a target="_blank" href="http://blog.michaelnascimento.com.br">Michael Nascimento Santos</a>, que trabalha conosco na <a target="_blank" href="http://www.summa-tech.com/">Summa</a>, fez um clone seu para trabalhar em uma <a target="_blank" href="http://www.jcp.org/en/jsr/detail?id=310">nova JSR a Date and Time API</a>. Essa JSR terá influência do projeto de código livre <a target="_blank" href="http://joda-time.sourceforge.net/">Joda Date and Time API</a>, pois o autor é participante da JSR também.
  
  


Ainda não li a proposta da JSR, mas algo que causa um pouco de trabalho, é atualizar o horário de verão, pois como as datas de ínicio e término variam em todas as ocorrências, é necessário atualizar o SO e JVM para refletir corretamente essas datas. 

Até o ano passado era necessário efetuar o download do código fonte do JDK (não é o <font face="courier new,courier,monospace">src.zip</font>) e compilar o pacote <font face="courier new,courier,monospace">javazic</font> e baseado no arquivo de timezone novo (arquivo texto), gerar o novo arquivo de timezone (binário) e colocar no <font face="courier new,courier,monospace">$JAVA_HOME/jre/lib/zi</font>. Atualmente isso já consegue ser aliviado através da <a target="_blank" href="http://java.sun.com/developer/technicalArticles/Intl/USDST/">ferramenta TZUpdate</a> que a Sun lançou ano passado. 

Não sei se essa parte estará na JSR (vou ler mais tarde). 

Ademais a API de Date e Time do Java precisa de algumas melhorias na API, para tornar mais fácil o uso dela. Ainda não esbarrei em algum problema sério que fizesse que eu usasse o JodaTime por exemplo (pelo que visualizei no guia de exemplo, é bem fácil). 

Pela brincadeira do clone do Michael Nascimento, pois possui tantas atividades, que só clonando para conseguir fazer tantas atividades. 

Desejo sucesso e que a API esteja disponível no JDK 7.