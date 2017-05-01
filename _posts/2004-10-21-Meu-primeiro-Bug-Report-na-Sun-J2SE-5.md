---
id: 22
title: Meu primeiro Bug Report na Sun (J2SE 5)
date: 2004-10-21T17:57:24+00:00
author: Claudio Miranda
layout: post
permalink: /2004/10/Meu-primeiro-Bug-Report-na-Sun-J2SE-5/
categories:
  - Java
---
**Updated:**
  
[
  
See a english version of this post (compact version)](http://www.claudius.com.br/blog/claudio/Java/2004/11/03/4040667D2C3778786BA6EB188A020FD4.txt) 

As vezes sou tachado de maluco quando uso as &uacute;ltimas
  
vers&otilde;es de softwares. Ontem compilei o <a target="_blank"
href="http://kernel.org/pub/linux/kernel/v2.6/linux-2.6.9.tar.bz2">Kernel<br /> 2.6.9</a> com <a target="_blank"
href="http://www.holtmann.org/linux/kernel/patch-2.6.9-mh1.gz">patch<br /> para bluetooth (mh1)</a>, fui rodar o j&aacute; conhecido J2SE 5 e saiu
  
o seguinte resultado:

<big><span style="font-family: monospace;">An error has occured while<br /> processing the shared archive file.</span><br
style="font-family: monospace;" /><br /> <span style="font-family: monospace;">Unable to reserve shared region.</span><br
style="font-family: monospace;" /><br /> <span style="font-family: monospace;">Error occurred during<br /> initialization of VM</span><br style="font-family: monospace;" /><br /> <span style="font-family: monospace;">Unable to use shared archive.</span></big>

Isso aconteceu pois usei a op&ccedil;&atilde;o <big><a target="_blank"
href="http://java.sun.com/j2se/1.5.0/docs/guide/vm/class-data-sharing.html"><span
style="font-family: monospace;">-Xshare:on</span></a></big>, uma
  
funcionalidade presente no J2SE 5, que tem como objetivo reduzir o
  
tempo de inicializa&ccedil;&atilde;o de classes. Em outro post vou
  
explicar mais sobre isso.

Fiz o Bug Report ontem (20 de Outubro) e foi aceito com o
  
n&uacute;mero: <a target="_blank"
href="http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=6182602">6182602</a>
  
(&eacute; necess&aacute;rio registro no website)

Para n&atilde;o acontecer esse erro: usar um kernel anterior (2.6.8.1
  
&eacute; o que vou usar) ou n&atilde;o usar a op&ccedil;&atilde;o <span
style="font-family: monospace;">-Xshare:on</span>