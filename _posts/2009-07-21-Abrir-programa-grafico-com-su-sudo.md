---
id: 225
title: 'Abrir programa gráfico com su &#8211; / sudo'
date: 2009-07-21T15:51:45+00:00
author: Claudio Miranda
layout: post
permalink: /2009/07/Abrir-programa-grafico-com-su-sudo/
categories:
  - Linux
---
Ao usar linux/unix é comum usar outro login de usuário para inicializar um programa gráfico. 

Repetidas vezes passei pela situação seguinte: 

<pre>sudo su -
root@foxhound:~# xeyes
Error: Can't open display:
root@foxhound:~# export DISPLAY=:0
root@foxhound:~# xeyes
No protocol specified
Error: Can't open display: :0
</pre>

Como fazer com que o programa gráfico seja iniciado e exibido ?
  
  


Em outro console é necessário dar permissão para um login localhost usar o servidor gráfico.
  
  


<pre>xhost local:claudio</pre>

Então pode lançar o programa gráfico no console anterior. 

Note, deve trocar o nome de usuário acima, para o usuário de sua máquina.
    
    


A explicação para isso é que no mundo unix existe o &#8220;X Server&#8221;, um servidor gráfico que gerencia as aplicações GUI. 

Com isso é possível, por exemplo acessar uma máquina unix remota e de lá iniciar um firefox, onde a exibição gráfica é mostrada no seu computador local.