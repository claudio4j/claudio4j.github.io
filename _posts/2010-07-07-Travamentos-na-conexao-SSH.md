---
id: 244
title: Travamentos na conexão SSH
date: 2010-07-07T23:06:35+00:00
author: Claudio Miranda
layout: post
permalink: /2010/07/Travamentos-na-conexao-SSH/
categories:
  - Diversos
---
Recentemente instalei um Red Hat Enterprise Linux 5.5 (RHEL) headless, um servidor para servir de experimentos. 

Este é um servidor headless, keyboardless, mouseless, a única maneira de trabalhar com ele é pela rede, onde uso o SSH. 

Logo após a instalação percebi que as conexões ora congelavam, o terminal travava, qualquer output de dados maior do que um pagedown, já travava, não era possível que um problema deste tipo ocorria com o RHEL, mas me irritava muito, isso era tanto para conexões SSH, como para HTTP, etc. 

As configurações do SSH, rede, sem firewall, sem SELinux, o que poderia ser&#8230;
  
  


Nas investigações, percebi que o driver da placa de rede estava incorreto. 

A minha placa de rede é uma &#8220;Realtek Semiconductor Co., Ltd. RTL8111/8168B&#8221; e a versão do driver instalado pelo RHEL era para outro modelo. 

Então a solução foi <a target="_blank" href="http://152.104.125.41/downloads/downloadsView.aspx?Langid=1&PNid=13&PFid=5&Level=5&Conn=4&DownTypeID=3&GetDown=false">copiar o driver do fabricante</a>, compilar e instalar. 

Dicas adicionais podem ser vista no <a target="_blank" href="http://wiki.centos.org/AdditionalResources/HardwareList/RealTekRTL8111b">website do CentOS</a>. 

Fica a dica, se o seu servidor linux remoto começar a congelar no resultado dos comandos, após uma instalação ou atualização, verifique se o driver da placa de rede confere com a placa real.
  
  


![](/resources/claudio/exploits_of_a_mom.png)
  
Cortesia de [XKCD.com](http://www.xkcd.com)