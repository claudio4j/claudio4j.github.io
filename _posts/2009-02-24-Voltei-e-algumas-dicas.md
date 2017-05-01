---
id: 221
title: Voltei e algumas dicas
date: 2009-02-24T19:27:41+00:00
author: Claudio Miranda
layout: post
permalink: /2009/02/Voltei-e-algumas-dicas/
categories:
  - Dicas
---
Apenas avisando que n&atilde;o morri, apenas fiquei pregui&ccedil;oso para escrever.

Id&eacute;ias n&atilde;o faltam, ent&atilde;o para voc&ecirc; n&atilde;o perder mais tempo, vou colocar algumas dicas e outras coisas que tenho feito

  * Em setembro, foi anunciado os ganhadores do pr&ecirc;mio Glassfish Awards Program, e felizmente eles consideraram minha submiss&atilde;o. Fiquei muito contente. Minha submiss&atilde;o foi um plugin para o console web de administra&ccedil;&atilde;o do glassfish v3, para [gerenciar keystores. Veja mais informa&ccedil;&otilde;es no site do projeto certadmin](https://certadmin.dev.java.net/). E o site com informa&ccedil;&otilde;es da [premia&ccedil;&atilde;o no](http://blogs.sun.com/arungupta/entry/sun_tech_days_2008_sao) [evento Sun Tech Days](http://blogs.sun.com/gap/entry/glassfish_awards_program_brazil) e a [lista completa dos ganhadores](http://wikis.sun.com/display/GAP/GAP+Winners).

<p style="margin-left: 40px;">
  O projeto ainda precisa de algumas melhorias, que vou escrever aqui, com alguns screenshots e explica&ccedil;&otilde;es.
</p>

  * Em um projeto passado, usei o Oracle SQL Plus, e cansado de pressionar a tecla para cima, na esperan&ccedil;a de ter o hist&oacute;rico de comandos e o sqplus n&atilde;o suportar, ent&atilde;o arrumei uma solu&ccedil;&atilde;o que funciona para qualquer aplica&ccedil;&atilde;o console com prompt. &Eacute; o [<kbd>rlwrap</kbd>](http://utopia.knoware.nl/~hlub/uck/rlwrap/), veja a sintaxe do comando

<p style="margin-left: 40px;">
  <code>&lt;tt>rlwrap /usr/local/instantclient_10_2/sqlplus $*&lt;/tt></code>
</p>

<p style="margin-left: 40px;">
  Onde o hist&oacute;rico fica armazenado em <code>~/.sqlplus_history</code> e a tecla para cima funciona.
</p>

<p style="margin-left: 40px;">
  O rlwrap &eacute; facilmente encontrado em qualquer distribui&ccedil;&atilde;o linux.
</p>

<p style="margin-left: 40px;">
  &nbsp;
</p>

  * Tenho instalado o mysql 5.0.51 instalado pelo apt-get no ubuntu. Precisei instalar a vers&atilde;o mais recente 5.1.31. N&atilde;o queria perder muito tempo instalando e configurando arquivos de configura&ccedil;&atilde;o com paths, portas, etc. Ent&atilde;o encontrei um projeto [`mysql_sandbox`](https://launchpad.net/mysql-sandbox), que consegue instalar v&aacute;rias vers&otilde;es do mysql em diferentes configura&ccedil;&otilde;es e isoladas uma das outras.

<pre style="margin-left: 40px;">./make_sandbox /usr/local/mysql_bits/unpacked/mysql-5.1.31-linux-i686-glibc23.tar.gz 
--db_user=claudio --db_password=blah123 --sandbox_port=3310
</pre>

<p style="margin-left: 40px;">
  Pronto, tudo funcionando.<br /> &nbsp;
</p>

  * Ajudo a moderar algumas listas do SouJava, e no sistema atual do ezmlm (gerenciador de listas de email) cada mensagem moderada &eacute; enviada um email com um cabe&ccedil;alho gigante para o meu email, ent&atilde;o se eu tivesse 15 mensagens para moderar, &eacute; um p&eacute; no saco entrar em cada mensagem, rolar ao final para ver o conte&uacute;do, copiar o endere&ccedil;o de aceite/rejei&ccedil;&atilde;o, depois agregar tudo e enviar. Ent&atilde;o cansado disso, gastei algumas horas e criei um sistema de modera&ccedil;&atilde;o, [ezmod](https://ezmod.dev.java.net/).

<p style="margin-left: 40px;">
  Usei <a href="http://wicket.apache.org/">Wicket</a>, JPA e <a href="http://docs.codehaus.org/display/JETTY">Jetty</a>, e est&aacute; funcionando muito bem. Se algu&eacute;m precisar fazer um test-drive posso enviar o link para moderar alguma lista. Por falar em Wicket, j&aacute; lan&ccedil;aram o 1.4 RC2.<br /> &nbsp;
</p>

  * Quando pesquiso no google, algum resultados de outros mecanismos de pesquisa aparecem (tel3listas, etc.), outro comportamento foi o google adicionar uma esp&eacute;cie de customiza&ccedil;&atilde;o de resultados, n&atilde;o gostei, e aproveitei para adicionar um par&acirc;metro de busca por data. Coloquei isso nas configura&ccedil;&otilde;es de pesquisa do firefox, no caminho

<pre style="margin-left: 40px;">/usr/local/firefox/searchplugins/google.xml</pre>

<p style="margin-left: 40px;">
  Como est&aacute; hoje
</p>

<pre style="margin-left: 40px;">&lt;Param name="q" value="{searchTerms}+-site:site.que.nao.quero.net+-site:outrosite.que.nao.quero.com.br"/&gt;
&lt;Param name="ie" value="utf-8"/&gt;
&lt;Param name="as_qdr" value="y5"/&gt;
&lt;Param name="hl" value="all"/&gt;
&lt;Param name="oe" value="utf-8"/&gt;
&lt;Param name="aq" value="t"/&gt;</pre>

<p style="margin-left: 40px;">
  Basicamente alterei os parametros hl e as_qdr, que significam respectivamente o idioma e o resultado ser&aacute; direcionado para o idioma ingl&ecirc;s (default); o as_qdr informa o uma faixa de tempo em meses ou anos.
</p>

<p style="margin-left: 40px;">
  Maiores <a href="http://code.google.com/intl/pt-BR/apis/searchappliance/documentation/52/xml_reference.html">informa&ccedil;&otilde;es sobre o</a> <a href="http://googlesystem.blogspot.com/2006/07/meaning-of-parameters-in-google-query.html">significado dos parametros</a>.
</p>

  * &nbsp;Meu [homonimo](http://www.claudiomiranda.com/), teve participa&ccedil;&atilde;o na cria&ccedil;&atilde;o do filme "[O estranho caso de Benjamin Button](http://www.benjaminbutton.com/)".