---
id: 236
title: Upgrade para o KUbuntu 9.10
date: 2010-01-30T16:49:13+00:00
author: Claudio Miranda
layout: post
permalink: /2010/01/Upgrade-para-o-KUbuntu-9-10/
categories:
  - Linux
---
Finalmente fiz o upgrade para o Kubuntu 9.10 

De fato fiz uma instalação do zero, pois usava a versão 8.04 ainda. 

Demorei tanto para fazer o upgrade pois uso o KDE a muito tempo, e percebi que a versão KDE 4.x ainda não estava estável ou similar ao KDE 3.5.x (última versão). 

Engraçado ter demorando tanto para instalar uma versão recente tanto do KDE como do Kubuntu, pois uso Linux desde 1997, e até alguns anos atrás estava na crista da onda quanto ao uso de softwares recentes do mundo unix, podendo ser kernel, X, samba, aplicativos, módulos, etc. Fiz muitos builds do kernel, somente para selecionar os módulos desejados (kernel 2.2.x ou 2.4.x) e assim deixar o sistema otimizado, tanto para laptop como desktop. Consegui fazer hibernação (suspend to disk e ram) funcionar ainda em 2003 (demorava era na hora do restore). Tem até uma <a target="_blank" href="http://www.orkut.com.br/Main#Community?cmm=5936869">comunidade no orkut</a> que o&nbsp; <a target="_blank" href="http://edgarsilva.com.br/">Edgar</a> criou, somente para homenagear pessoas como eu que gostam de recompilar :) 

Também costumo usar muito sistema em beta, trunk, alpha incluindo Java SDK, Netbeans, servidores, etc. 

Na medida que foram saindo as distribuições com o KDE 4, percebi que o KDE 4 ainda não estava nem beta, faltavam muitas funcionalidades, ruim de performance (até hoje), e coisas desnecessárias. 

Vou citar algumas delas, para não ficar no vazio: 

  * o tempo de inicialização do KDE 4 era bem maior do que o KDE 3
  * Frescurinhas, como os efeitos de girar as janelas, mover, minimizar, etc. Isso só é legal nas apresentação, fora isso, é perda de tempo da CPU. Neste caso já vi diversos colegas se perederem no monte de janelas e seus efeitos.
  * Uso muito uma aplicação de gerenciador de arquivos <a target="_blank" href="http://krusader.sourceforge.net/">Krusader</a>. Para mim, a melhor ferramenta neste segmento. Está ficando boa, aogra com o porta para o KDE 4.
  * Baixa performance, no gerenciamento das janelas, ao fazer um ALT+TAB, por exemplo ou navegar no sistema de arquivos por uma aplicação gráfica.
  * Porcarias como nepomuk, strigi, akonadi, que servem apenas consumir preciosos recursos (neste caso é só remover ou desabilitar).

Resumo da ópera, desde quando começei a usar Linux, tinha de fazer muito tweak, compilar, tunar o sistema, hoje isso já não é (tão) necessário, muita coisa já vem pronta&nbsp; e sai funcionando. E eu tinha tempo de fazer isso, hoje esse tempo diminuiu. 

Ontem instalei o Kubuntu 9.10, como sempre coloco as partições importantes fora do / (como o /home /usr/local /opt) então foi uma instalação tranquila. Mas para deixar o sistema do meu jeito, vou relatar abaixo os probleminhas. 

Ao iniciar o sistema, a interface eth0 não pegava o IP do roteador, de jeito nenhum apesar de o ifconfig mostrar (quase) tudo certo, exceto que o IPv6 estava habilitado. No /var/log/messages, mostrava 

Jan 29 22:38:07 foxhound dhclient: DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 7
    
  
Jan 29 22:38:07 foxhound avahi-daemon[809]: Registering new address record for fe80::210:13ff:fe50:a343 on eth0.*.
    
  
Jan 29 22:38:14 foxhound dhclient: DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 11
    
  
Jan 29 22:38:16 foxhound kernel: [ 4782.660039] **eth0: no IPv6 routers present**
  
  


Que caca é essa ? 

O problema é que eu não tinha conexão com a internet neste computador, tive de arrumar outra conexão em outro computador e <a target="_blank" href="http://www.webupd8.org/2009/11/how-to-disable-ipv6-in-ubuntu-910.html">desabilitar o IPv6</a>.
  
  


Então passei a personalizar o sistema 

  * Desabilitar os efeitinhos frufru de janela
  * Desabilitar/remover nepomuk, strigi, akonadi, coisas que ficam indexando meu disco. não quero isso.
  * Coloquei as fontes true type que mais uso e são ótimas como Bitstream Vera e Tahoma. E podem ser colocadas em tamanho de 8 pixels sem distorção.
    
    
  * Desabilitei vários serviços do sistema KDE que são inicializados mas não necessários. Eles podem ser encontrados em **<font face="courier new,courier,monospace">/usr/share/autostart/</font>**
    
    
  * Desabilitei serviços do /etc/init.d que não são necessários

No geral ainda pretendo descobrir algumas otimizações, visto que o plasma consome mais memória. Fiquei satisfeito, talvez por ter um objetivo de uso diferente de home ou business office, mas com forte uso de desenvolvimento de aplicações e testes, com longos períodos de uso, preciso de algo que funcione extremamente bem, como estava funcionando. Prova disso é que que a instalação do Kubuntu 8.04 já tinha 2 anos.
  
  


   
![Fun](/resources/claudio/foxtrot.2003-08-14.gif)