---
id: 47
title: Compilar e Instalar o Kernel do Linux 2.6.x
date: 2005-02-05T02:11:42+00:00
author: Claudio Miranda
layout: post
permalink: /2005/02/Compilar-e-Instalar-o-Kernel-do-Linux-2-6-x/
categories:
  - Dicas
---
Tenho uma mania de usar sempre as &uacute;ltimas vers&otilde;es de
  
softwares, ver o changelog, enfim ver o que tem de novo. E o Kernel faz
  
parte dessa mania, escrevi um script bash para ser executado como root,
  
ele compila o kernel, m&oacute;dulos, instala os m&oacute;dulos, faz
  
backup do kernel anterior e salva as configura&ccedil;&otilde;es da
  
&uacute;ltima compila&ccedil;&atilde;o. 

Ele pode ser executado assim:

<big><big><span style="font-family: monospace;">$ build_kernel 2.6.10</span></big></big>

Com isso deve existir o seguinte diret&oacute;rio: /usr/src/linux-2.6.10

As op&ccedil;&otilde;es s&atilde;o:&nbsp; <big><big><span
style="font-family: monospace;"><versao do kernel><br /> [-all|-kernel|-modules]</span></big></big>

<big style="font-family: monospace;"><big>-all: compila o kernel e<br /> m&oacute;dulos e instala o kernel e m&oacute;dulos<br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; make bzImage, make modules, make<br /> modules_install<br /> -kernel: compila e instala apenas o kernel<br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; make bzImage<br /> -modules: compila e instala somente os m&oacute;dulos<br /> &nbsp;&nbsp;&nbsp; &nbsp;&nbsp; make modules, make modules_install</big></big>

[Download](/resources/claudio/build_kernel "Download do script")