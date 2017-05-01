---
id: 102
title: eth0 morreu, viva eth1
date: 2006-08-16T16:52:05+00:00
author: Claudio Miranda
layout: post
permalink: /2006/08/eth0-morreu-viva-eth1/
categories:
  - Linux
---
No dia 06/ago, tive de me ausentar de minhas atividades profissionais, até o dia 13/ago. Então fui ligar o laptop e percebi que a interface de rede não estava funcionando. Pensei que o módulo e1000 (Intel Ethernet Gigabit PRO/1000), não estava fucionando bem.

Pois bem, depois reiniciar a interface de rede (/etc/init.d/networking restart) não funcionou, com messagens &#8220;eth0: no such device&#8221;, bem a coisa começou a ficar séria.

Depois, que um dmesg, mostrou a seguinte mensagem:

<pre>e1000: 0000:02:00.0: e1000_probe: PHY reset is blocked due to SOL/IDER session.
e1000: 0000:02:00.0: e1000_probe: The EEPROM Checksum Is Not Valid
e1000: probe of 0000:02:00.0 failed with error 
</pre>

Então o amigão google, deu uma mãozinha e indicou [um problema semelhante](http://www.thinkwiki.org/wiki/Problem_with_e1000:_EEPROM_Checksum_Is_Not_Valid), mas que não aplicou ao meu caso, pois o cabo de rede estava conectado. 

Tentei descarregar e carregar o módulo e1000 novamente, com cabo desconectado ou conectado, mas sem efeito.

Até carreguei um livecd, para ver se não era algo com o SO&#8230; nada a ver. Carreguei até o windows, para ver se estava funcionando, para minha surpresa o windows, nem carregou, mas mostrou um BSOD antes de carregar a tela de login, tsc tsc, que pena.

Infelizmente, nada funcionou, então presumi que a interface de rede, tirou férias definitvas.

Agora, como que depois de uma semana, desligado a interface não funciona ? Que lixo mesmo.

Tenho um laptop Dell, antigo, de 700 Mhz, de 2002, é lento para as aplicações atuais, mas tudo funcionou direitinho (e [nunca](http://www.consumeraffairs.com/news04/2006/08/dell_fire.html) [pegou](http://www.engadget.com/2006/07/28/another-dell-laptop-ignites/) [fogo](http://www.theinquirer.net/default.aspx?article=32550))

O resultado disso tudo ? Tive de comprar um cartão PCMCIA Encore, que funcionou de primeira no linux.

Esse laptop ainda será trocado pelo fornecedor (quando acabar uma novela que já dura 3 meses), vou tentar trocar por um HP NX9420, vamos ver.