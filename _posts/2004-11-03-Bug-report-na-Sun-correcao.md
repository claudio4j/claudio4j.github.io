---
id: 24
title: 'Bug report na Sun &#8211; correção'
date: 2004-11-03T12:35:18+00:00
author: Claudio Miranda
layout: post
permalink: /2004/11/Bug-report-na-Sun-correcao/
categories:
  - Java
---
Corre&ccedil;&atilde;o sobre o bug report, basta usar a
  
op&ccedil;&atilde;o <span style="font-family: monospace;">-Xshare:dump</span>
  
para regenerar o arquivo compartilhado. Isso &eacute;
  
necess&aacute;rio, pois o kernel 2.6.9 usa um layout diferente de
  
mem&oacute;ria. O bug report est&aacute; classificado como &#8220;request for
  
enhacement&#8221;.