---
id: 113
title: Atualização do KUbuntu Dapper (6.06) para o Edgy (6.10)
date: 2006-11-04T18:03:49+00:00
author: Claudio Miranda
layout: post
permalink: /2006/11/Atualiza-o-do-KUbuntu-Dapper-6-06-para-o-Edgy-6-10/
categories:
  - Linux
---
A organização Ubuntu liberou a versão final do KUbuntu 6.10 (codinome Edgy Eft). A versão que uso é a 6.06 (codinome Dapper), que é a primeira versão que instalei (anteriormente usava <a target="_blank" href="http://www.mandrivaclub.com/">Mandriva</a> no laptop, ainda a uso no desktop). Então resolvi fazer uma atualização, para ver como é. 

<cut>

  
Quais as motivações para realizar a atualização ?
  
  


  * Entender como funcionar o esquema de atualização da distribuição inteira
  * Usar o <a target="_blank" href="https://wiki.ubuntu.com/ReplacementInit">novo sistema de inicialização</a> (em substituição ao sysvinit)
  * Instalar a versão 2.0 do Gnucash

Para entender como funciona a atualização, li o <a target="_blank" href="https://wiki.ubuntu.com/EdgyReleaseNotes">release notes do ubuntu</a> e <a target="_blank" href="http://kubuntu.org/announcements/6.10-release.php">do kubuntu</a>. E os <a target="_blank" href="https://wiki.ubuntu.com/EdgyReleaseNotes#head-7348aa0831ef34256bdd066d1d9a1d112a4afa50">possíveis</a> <a target="_blank" href="https://wiki.kubuntu.org/KubuntuEdgyKnownProblems">problemas</a>, <a target="_blank" href="http://www.debianadmin.com/ubuntu-edgy-upgrade-common-problems-with-solutions.html">após</a> a instalação. 

Para uma comparação, no madriva, para atualizar a versão do sistema operacional, bastava dar boot com o cd-rom e solicitar uma atualização. Tentei fazer isso com o livecd do kubuntu 6.10, iniciei o sistema de instalação, segui os passos até o momento de particionar o disco, como não foi apresentado nenhuma opção de atualizar, então abortei e resolvi seguir a atualização através do apt-get. 

A atualização através do apt-get está no <a target="_blank" href="http://kubuntu.org/announcements/6.10-release.php">release notes do kubuntu 6.10</a>: </p> 

<pre>Users of Kubuntu 6.06 LTS can upgrade to 6.10 over the internet by following these instructions:

    * NOTE: This procedure upgrades your system over the Internet, which requires a large download of several hundred megabytes.
    * In Konqueror go to /etc/apt, right click on sources.list and choose Actions -&gt; Edit as Root
    * Change all instances of dapper to edgy
    * Launch a console with KMenu -&gt; System -&gt; Konsole
    * In the console run: sudo apt-get update
    * In the console run: sudo apt-get dist-upgrade and follow the prompts to upgrade
    * In the console run: sudo apt-get install kubuntu-desktop python-qt3 python-kde3 ubuntu-minimal and follow the prompts to install
    * Reboot your computer

If you have a Kubuntu 6.10 CD, put it in the drive, and run apt-cdrom from the command line. Then follow the instructions above.&nbsp;</pre>

Então usei o comando apt-cdrom add, que adicionou o cd-rom no repositório do apt-get. Então comentei os repositórios freecontrib,&nbsp; debuntu.org. 

Invoquei o dist-upgrade, pensei que fosse demorar uns 30min, que nada, demorou cerca de 2h, para efetuar o download. Deu um erro ao fazer o download de um pacote, então fiz o dist-upgrade novamente, o download ocorreu tranquilo. 

Mas depois do download, é realizado as atualizações dos pacotes, o qual ocorreu um erro de <a target="_blank" href="https://launchpad.net/distros/ubuntu/+source/courier-authlib/+bug/64615">inconsistência do pacote courier-authdaemon</a>, que depois de algumas pesquisas no google, fui o infeliz que deparou com um bug na atualização de pacotes. Tentei de primeira usar o workaround sudo dpkg &#8211;force-remove-reinstreq -P courier-authdaemon, mas não funcionou, então invoquei o sudo dpkg &#8211;configure -a, depois sudo dpkg &#8211;purge courier-authdaemon e sudo apt-get -f install para ver se resolvia o problema, que continuava acusando o erro de inconsistência de pacote do courier-authdaemon, então por fim invoquei o sudo dpkg &#8211;force-remove-reinstreq -P courier-authdaemon novamente e então o pacote foi removido com sucesso, ufa, pude continuar com a atualização do kubuntu. 

Invquei o&nbsp; sudo apt-get -f install para resolver a integridade dos pacotes e começou a realizar um monte de checagens, até deparar com uma janela de diálogo informando em português &#8220;Incorrect nice value. Please enter an integer between -20 and 19&#8221;, e não é possível clicar no Next nem Cancel, então matei o processo, <a target="_blank" href="http://www.ubuntuforums.org/showthread.php?p=1686388#post1686388">encontrei a solução nesta thread</a> e parece <a target="_blank" href="https://launchpad.net/distros/ubuntu/+source/xorg/+bug/68267">ser um bug</a>. 

<pre>sudo dpkg-reconfigure debconf
</pre>

E escolher Dialog, depois escolha&nbsp; o nível Alto 

Então pude invocar novamente o sudo apt-get -f install para continuar. Demorou mais uns 20min configurando e atualizando pacotes, então para verificar se não havia mais erros de dependência ou integridade invoquei os comandos: sudo apt-get -f install, sudo dpkg &#8211;configure -a e sudo apt-get dist-upgrade. Os quais não retornaram erros, então reiniciei a maquina. 

Na tela de inicialização, verifiquei o uso do novo sistema de inicialização, pareceu que foi mais rápido, mas ainda não cronometrei (o anterior sysvinit demorava cerca de 44s), então para minha surpresa, verifiquei que o X não inicializava. Mesmo invocando no console o startkde, o mesmo retornava com o erro:&nbsp; &#8220;xsetroot: unable to open display&#8221; seguido de erros do &#8220;kpersonalizer: unable to open display&#8221;. 

Sempre que o X não inicializar, dê uma olhada no log do X (/var/log/Xorg.0.log). Aqui acusava um erro de mismatch de versão ao carregar o driver da placa de vídeo i810. Lembrei da dica do debianadmin, em que o driver instalado estava errado. O que estava instalado aqui era o xserver-xorg-driver-i810 então removi e instalei o xserver-xorg-video-i810. 

<pre>$ sudo apt-get remove  xserver-xorg-driver-i810
$ sudo apt-get install xserver-xorg-video-i810
</pre>

Reiniciei o X e foi iniciado corretamente.
  
  


Realmente não entendi, o motivo dessa mudança da nomenclatura de pacotes, nem fui verificar o motivo, mas enfim, estava com as coisas funcionando novamente. 

Verifiquei que outros <a target="_blank" href="http://www.mail-archive.com/ubuntu-br@lists.ubuntu.com/msg11146.html">brasileiros enfrentaram o mesmo problema da inicialização do X</a>. 

Mas, o kernel 2.6.17 não foi instalado, isso é estranho. Verifiquei a nomenclatura dos pacotes e percebi que o meu kernel é linux-image-2.6.15-26-686 e o a nomenclatura do 2.6.16 é linux-image-2.6.17-10-386, que é diferente. Mas, caramba, porque não liberaram a versão 686 que é tão comum hoje ?
  
  


Bom, mas o importante é que o objetivo foi alcançado. Agora vou brincar com as crianças, falow.
  
  


</cut>