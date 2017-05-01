---
id: 18
title: Escolha do Sistema de Blog
date: 2004-10-19T05:55:56+00:00
author: Claudio Miranda
layout: post
permalink: /2004/10/Escolha-do-Sistema-de-Blog/
categories:
  - Java
---
Sei que existem blogs gratuitos (JRoller, javablogs.com.br, UOL Blogs,
  
etc.), mas preferi ter um instalado no meu website para usar o
  
dom&iacute;nio em algo mais interessante do que dom&iacute;nio de
  
email apenas :-o&nbsp; 

Para iniciar vou descrever um pouco sobre as motiva&ccedil;&otilde;es
  
em usar o <a target="_blank"
 href="http://wiki.blojsom.com/wiki/display/blojsom/About+blojsom">Blojsom</a>
  
como sistema de blogging. 

Como requerimentos iniciais, o sistema de blog deve suportar:

  * Escrito em Java 
  * Suporte a <a target="_blank"
 href="http://www.movabletype.org/trackback/beginners/">trackbacks</a>
  * Limita&ccedil;&atilde;o de inclus&atilde;o de coment&aacute;rios
  
    de um mesmo IP em espa&ccedil;os de tempos curtos 
  
    (comment throttling) 
  * Licen&ccedil;a que permita extens&atilde;o (tipo <a
 target="_blank" href="http://opensource.org/licenses/">F/OSS</a>),
  
    pois vou fazer extens&otilde;es
  * M&uacute;ltiplos usu&aacute;rios
  * Escolha de temas/skins
  * Moblog, xmlrpc

Com isso, cheguei a 3 sistemas: [Blojsom](http://wiki.blojsom.com/wiki/display/blojsom/About+blojsom),
  
[Roller Weblogger](http://www.rollerweblogger.org/page/project)
  
e <a target="_blank" href="http://pebble.sourceforge.net/">Pebble</a>.

Inicialmente n&atilde;o quis usar o Roller, pois ele necessita de um
  
banco de dados, e no meu caso espec&iacute;fico prefiro usar o sistema
  
de arquivos como reposit&oacute;rio de coment&aacute;rios e blogs.

Instalei e testei o Blojsom, funcionou tudo direitinho logo de primeira
  
(em um tomcat local). E precisava de um sistema de blog que funcionasse
  
sem precisar configurar muito.

Com o pebble, suporta todas as funionalidades que precisava, mas ainda
  
n&atilde;o tem skins diferentes e n&atilde;o permite editar blogs
  
criados (pela interface web), sei que para apenas um desenvolvedor ([Simon Brown](http://www.simongbrown.com/blog/) do Pebble)
  
&eacute; complicado fazer o que todos desejam, sem desmerecer o
  
trabalho do autor, &eacute; um grande projeto. Logo achei por bem usar
  
o Blojsom, se bem que como tudo est&aacute; armazenado em sistema de
  
arquivos fica f&aacute;cil fazer a migra&ccedil;&atilde;o para qualquer
  
sistema de blogging (mas n&atilde;o pretendo fazer isso t&atilde;o
  
cedo).

Bem interessante a API de plugins do Blojsom, e os pr&oacute;prios
  
plugins existentes, pretendo desenvolver alguns que acho interessante
  
como:

  * Printable view para cada entrada com coment&aacute;rios
  * Referers URLs
  * Referers Throttling
  * Estat&iacute;sticas por entrada de blog 
  * Salvar blogs sem publicar (draft entries)
  * Estat&iacute;sticas: browser, total por dom&iacute;nio, etc.

Sobre os plugins existentes, os mais interessantes:

  * Associa&ccedil;&atilde;o de categorias: permite efetuar blogs e
  
    associar com diferentes categorias
  * Emoticons: ao colocar os sinais de emoticons, troca por um icone
  * Show me more: Na p&aacute;gina principal do blog, limita a
  
    apresenta&ccedil;&atilde;o do texto em <span
 style="font-style: italic;">n</span> caracteres, com um link &#8220;see
  
    more&#8221; (customiz&aacute;vel) para ver o blog completo.
  * Google highlight: Coloca um background diferente nas palavras que
  
    satisfazem uma pesquisa de algum visitante que tenhado clicado em um
  
    link de pesquisa do google.
  * Groovy: Escreva plugins com [Groovy](http://groovy.codehaus.org/)
  * Hyperlink: Automaticamente cria um link para URLs colocadas no
  
    blog.
  * Moblog: Escreva blogs atrav&eacute;s de mensagens de email, com
  
    (relativa) seguran&ccedil;a

&Eacute; importante que os sistemas de blogging tenham alguma esquema
  
de referer throttling para evitar que sejam publicados nos &#8220;income
  
URLs&#8221; dos blogs, as pesquisas de websites de conte&uacute;do acima de
  
18 anos, como se fossem visitantes do blog. Apesar de que isso pode ser
  
minimizado com filtros de referers. O Blojsom tem um filtro de
  
websites, pode ser usado express&otilde;es regulares para bloquear
  
referers indesejados.