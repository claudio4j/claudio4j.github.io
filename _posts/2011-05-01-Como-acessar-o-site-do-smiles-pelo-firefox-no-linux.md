---
id: 250
title: Como acessar o site do smiles pelo firefox no linux
date: 2011-05-01T12:00:31+00:00
author: Claudio Miranda
layout: post
permalink: /2011/05/Como-acessar-o-site-do-smiles-pelo-firefox-no-linux/
categories:
  - Dicas
---
<big><a href="http://www.claudius.com.br/blog/claudio/dicas/Como-acessar-o-site-do-smiles-pelo-firefox-no-linux-v2">Atualização: Fiz uma versão melhor</a>.</big>

Como milhares de outras pessoas neste Brasil, estou cansado da
  
decadência tecnológia do site da gol e smiles, onde não consegue-se
  
acessar o site do smiles para gerenciar suas milhas, fui ver o que dava
  
para fazer e conseguir continuar o firefox no linux. E consegui !

  1. Instalar as extensões [User
  
    Agent Switcher](https://addons.mozilla.org/pt-BR/firefox/addon/user-agent-switcher/) e [Firebug](https://addons.mozilla.org/pt-BR/firefox/addon/firebug/) 
  2. Após reiniciar o firefox, <span style="font-weight: bold;">usar<br /> o &#8220;Internet Explorer 8&#8221; como User Agent</span> (o site recebe a
  
    informação que é o IE o navegador)</p> 
    ![](/resources/claudio/20110501_smiles1.png)
  
    ![](/resources/claudio/20110501_smiles2.png)

  3. Na tela de login, quando o mouse fica na eterna espera e não
  
    deixa clicar em nada, <span style="font-weight: bold;">abra o firebug<br /> </span>
  4. Na aba HTML, clique no icone para <span
style="font-weight: bold;">ispecionar um elemento</span> (<span
style="font-weight: bold;">Ctrl+Shift+C</span>)
  5. Clique bem no meio da tela, irá aparecer o HTML, então procure o <span
style="font-weight: bold;">div=&#8221;dvBusy&#8221;</span>, fica um pouco acima do
  
    elemento que você clicou (veja abaixo um screenshot da imagem)</p> 
    
![](/resources/claudio/20110501_smiles4.png) </li> 
    
      * Clique no elemento div e o remova&nbsp; (pressione del), pronto
  
        agora a página é uma tela web convencional</p> 
        ![](/resources/claudio/20110501_smiles5.png)
    
      * Para cada página é necessário remover o div inútil, acho que o
  
        greasemonkey deve deixar isso definitivo, vou ver depois coloco o
  
        resultado aqui. </ol> 
    
    <big><big>Ao gerente do site da Gol, pode por gentileza pedir para a<br /> equipe remover este div que só atrapalha, tenho certeza que a equipe de<br /> marketing e suporte irão agradecer.Assim como milhares de<br /> usuários firefox.</big></big> 
    
    Ainda não fiz o teste para o site da tam, depois coloco o resultado
  
    aqui.