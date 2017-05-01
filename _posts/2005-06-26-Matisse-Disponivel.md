---
id: 74
title: Matisse Disponivel
date: 2005-06-26T20:20:00+00:00
author: Claudio Miranda
layout: post
permalink: /2005/06/Matisse-Disponivel/
categories:
  - Java
---
O Matisse, desenhador de telas do NetBeans <a href="http://www.netbeans.org/kb/articles/matisse.html" target="_blank">já estava disponível ha muito tempo</a>, bastava ativar através de uma opção da JVM, se você tem um development build da 4.2, tente usar esta opção:

<pre>-J-Dnetbeans.form.new_layout=true
</pre></p> 

Abra o $NB_HOME/etc/netbeans.conf e adicione ao fim da lista de opções.

<table>
  <tr>
    <td colspan="2">
      Para começar a brincar, basta criar um novo projeto ou novo JFrame<br /> <br /> <img align="left" src="/resources/claudio/nb-matisse-1.jpg" alt="Criação de JFrame" />
    </td>
  </tr>
  
  <tr>
    <td colspan="2">
      <img align="left" src="/resources/claudio/nb-matisse-2.jpg" alt="Criação de JFrame" />
    </td>
  </tr>
  
  <tr>
    <td colspan="2">
      Será aberta a tela de edição visual do Frame, <br /> agora é só brincar. Veja algumas modificações:</p> 
      
      <p>
        1) Botões de alinhamento<br /> <img align="left" src="/resources/claudio/nb-matisse-3-1.jpg" alt="Criação de JFrame" /> </td> </tr> 
        
        <tr>
          <td colspan="2">
            2) &#8220;Free Design&#8221;<br /> <img align="left" src="/resources/claudio/nb-matisse-3-2.jpg" alt="Criação de JFrame" />
          </td>
        </tr>
        
        <tr>
          <td colspan="2">
            3) Esse botão eu não sei pra que serve ainda. :-)<br /> <img align="left" src="/resources/claudio/nb-matisse-4.jpg" alt="Criação de JFrame" />
          </td>
        </tr></table> 
        
        <p>
          Tentei usar o Matisse em forms criados com GridBagLayout, mas não funcionou, não sei se será suportado isso.
        </p>
        
        <p>
          Para quem vai usar versões de desenvolvimento, recomendo fortemente assinar as <a href="http://www.netbeans.org/community/lists/top.html#top">listas de discussão do NetBeans</a>.
        </p>
        
        <p>
          <a href="/resources/claudio/matisse-saida.html" target="_blank">Veja uma demonstração</a>
        </p>