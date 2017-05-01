---
id: 173
title: Completar números com zeros a esquerda
date: 2007-07-28T05:07:59+00:00
author: Claudio Miranda
layout: post
permalink: /2007/07/Completar-numeros-com-zeros-a-esquerda/
categories:
  - Dicas
---
Ao lidar com impressão de números em relatórios, geralmente é necessário preencher todas as posições com o número zero a esquerda. 

Exemplo: 

É necessário preencher um campo de 10 posições, onde dado um número qualquer, que seja menor do que a quantidade de posições, então as posições do lado esquerdo devem ser preenchidos com o número zero. 

<table style="border: 1px groove rgb(0, 0, 102); float: none; background-image: none;" border="1" frame="void" rules="none" width="14%">
  <tr>
    <td>
      Número
    </td>
    
    <td>
      Impressão
    </td>
  </tr>
  
  <tr>
    <td>
      382
    </td>
    
    <td>
      0000000382
    </td>
  </tr>
  
  <tr>
    <td>
      450018
    </td>
    
    <td>
      0000450018
    </td>
  </tr>
</table>

  
Uma das técnicas mais comuns é usar a quantidade total de números do campo e adicionar com zeros a esquerda e depois remover os zeros excedentes. 

<pre>int n = 38002;
String zeros = "0000000000";
String numero = zeros + n;
System.out.println(numero.substring(numero.length() - 10));
</pre>

No Java 5 existe um método [printf](http://java.sun.com/j2se/1.5.0/docs/relnotes/features.html#formatter), copiado da linguagem C que permite formatar a impressão do resultado.&nbsp; 

<pre>int n = 38002;
System.out.printf("%010d", n);
</pre>

Esta é apenas uma das funcionalidades adicionadas ao Java 5 que aos poucos são incorporadas no dia a dia dos projetos. 

_Atualização em 28/julho_: 

Nem tudo é impresso no console, mas manipulações de variáveis, então basta usar outro método que retorna uma String. No exemplo abaixo, a variável f, contém o número formatado.
  
  


<pre>String f = String.format("%010d", n);
System.out.printf(f);
</pre>