---
id: 158
title: Qual é a quantidade máxima de threads suportada por um sistema ?
date: 2007-05-15T19:49:14+00:00
author: Claudio Miranda
layout: post
permalink: /2007/05/Qual-e-a-quantidade-maxima-de-threads-suportada-por-um-sistema/
categories:
  - Java
---
Tive de efetuar um teste para um cliente, onde é necessário verificar qual é a quantidade máxima de threads suportada por uma determinada máquina. 

Parece simples não é ? Pois só parece, pois existem fatores que podem variar muito o resultado 

  * Tamanho da pilha: <tt>-Xss</tt>
    
      
    <tt></tt> 
  * Tamanho máximo do heap: <tt>-Xmx</tt> 
  * Capacidade computacional disponível, para funcionar o teste. Tome cuidado ao rodar isso na sua máquina de produção.
     
    
  * Em um ambiente de servidor real, o mesmo usa mecanismos de pool e prioridades, onde este teste não considera isso. Logo o sistema irá sempre suportar mais threads do que o resultado desta medição.
  * Cada thread efetua vários cálculos matemáticos, enquanto que em uma aplicação real cada thread faz operações diferentes.

Fiz [um guia no ClaudiusWiki](http://wiki.claudius.com.br/wiki/Howto_MaxThreads_pt_BR), onde as existem mais informações sobre isso e onde estão os arquivos para download, com as respectivas instruções.