---
id: 350
title: 'Impressora HP Deskjet &#8211; erro de comunicação'
date: 2013-08-20T15:22:24+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=350
permalink: /2013/08/impressora-hp-deskjet-erro-de-comunicacao/
categories:
  - Dicas
---
Tenho uma impressora HP DeskJet 3050 multifuncional wireless, que funcionava muito bem no linux. Ocorre que em Julho, fiz uma atualização no Fedora onde ela não funcionou mais, ocorriam erros de comunicação. No /var/log/messages mostra:

<pre>Aug 20 14:43:10 localhost python: io/hpmud/jd.c 802: error timeout mdns lookup HP8ED8C6.local
Aug 20 14:43:14 localhost python: io/hpmud/jd.c 93: unable to read device-id
Aug 20 14:43:14 localhost hp-toolbox: hp-toolbox(UI)[4817]: error: Unable to communicate with device (code=12): hp:/net/Deskjet_3050_J610_series?zc=HP8ED8C6
Aug 20 14:43:14 localhost hp-toolbox: hp-toolbox(UI)[4817]: error:  Unable to open device hp:/net/Deskjet_3050_J610_series?zc=HP8ED8C6.</pre>

Apesar do utilitário HP-Toolbox conseguir detectar a impressora na instalação, mas não funciona posteriormente. Analisando nos fóruns, na página do <a href="https://wiki.archlinux.org/index.php/CUPS#hp-setup_finds_the_printer_automatically_but_reports_.22Unable_to_communicate_with_device.22_when_printing_test_page_immediately_afterwards" target="_blank">ArchLinux, vejo uma dica preciosa, de que o avahi-daemon deve estar em funcionamento</a>.

Então, verifique seu ambiente, se o avahi-daemon está instalado. No caso abaixo, ele retorna o caminho do binário de execução.

<pre>$ which avahi-daemon
/usr/sbin/avahi-daemon</pre>

Instale, caso não esteja

<pre>sudo yum install avahi</pre>

Ative o serviço na inicialização do Linux

<pre>sudo systemctl enable avahi-daemon.service
sudo systemctl start avahi-daemon.service</pre>

Pronto, o serviço deve estar em execução e com uma porta UDP aberta.

<pre>$ ps -ef|grep avahi
avahi     5062     1  0 14:53 ?        00:00:00 avahi-daemon: running [pavlov.local]
avahi     5063  5062  0 14:53 ?        00:00:00 avahi-daemon: chroot helper
claudio   5483   911  0 15:20 pts/1    00:00:00 grep --color=auto avahi

$ sudo netstat -antpuew|grep avahi
udp        0      0 0.0.0.0:5353            0.0.0.0:*                           70         124719     5062/avahi-daemon:  
udp        0      0 0.0.0.0:34370           0.0.0.0:*                           70         124720     5062/avahi-daemon:</pre>

Agora, ative o serviço do hp-toolbox e veja se a impressão funciona.