---
id: 30
title: 'Projetos de C&oacute;digo Livre e Ferramentas'
date: 2005-01-04T03:28:00+00:00
author: Claudio Miranda
layout: post
permalink: /2005/01/ferramentas-codigo-livre/
categories:
  - Java
---
Em muitas vezes participo em projeto de c&oacute;digo
  
livre: testando, corrigindo pequenos problemas, tradu&ccedil;&atilde;o
  
(por enquanto Blojsom e Jahia), f&oacute;runs e listas de
  
discuss&atilde;o.

Como desenvolvedor, fico satisfeito de ter acesso ao c&oacute;digo
  
fonte, para colocar funcionalidades ou corrigir problemas que estejam

relacionado ao dom&iacute;nio de uso do software em meu contexto. E
  
poder devolver as modifica&ccedil;&otilde;es para a comunidade e ser
  
aceito no controle de vers&atilde;o &eacute; muito melhor, pois
  
n&atilde;o &eacute; necess&aacute;rio fazer merge (he he he he,
  
situa&ccedil;&atilde;o chata).

Uma das coisas que acho fundamental em qualquer projeto de
  
c&oacute;digo livre, &eacute; uma documenta&ccedil;&atilde;o
  
m&iacute;nima, para que possa atrair mais desenvolvedores, como:
  
roadmap, javadoc (bem comentado), processo de gera<tt>ant</tt>&ccedil;&atilde;o de
  
distribui&ccedil;&atilde;o, issue tracking. Acho que isso deve ser o
  
m&iacute;nimo. 

Algumas ferramentas que acho que todo projeto mantido por desenvolvedores dispersos geograficamente

  * <a target="_blank" href="http://www.atlassian.com/software/jira/">Jira</a>&nbsp; &#8211; (Issue Tracker) *
  * <a target="_blank" href="http://www.atlassian.com/software/confluence/">Confluence</a>&nbsp; &#8211; (Wiki) *
  * <a target="_blank" href="http://www.cenqua.com/clover">Clover</a>&nbsp; (Relat&oacute;rios JUnit)*
  * <a target="_blank" href="http://www.cenqua.com/fisheye/">FishEye</a>&nbsp; (Relat&oacute;rios de uso do controle de vers&atilde;o)*
  * <a target="_blank" href="http://subversion.tigris.org/">SubVersion</a>
  * <a target="_blank" href="http://maven.apache.org/">Maven</a>
  * <a target="_blank" href="http://ant.apache.org">Ant</a>

* licensa gratuita para projetos de c&oacute;digo livre

Com essas ferramentas &eacute; poss&iacute;vel monitorar as
  
corre&ccedil;&otilde;es de problemas, gera&ccedil;&atilde;o de
  
changelog, gera&ccedil;&atilde;o de releases. Os mais importantes em
  
minha opini&atilde;o.

O SubVersion n&atilde;o &eacute; suportado na vers&atilde;o
  
dispon&iacute;vel do FishEye, j&aacute; est&aacute; em desenvolvimento
  
o suporte a SubVersion.

Para quem ainda n&atilde;o brincou com SubVersion, por favor, instale-o e use-o, vale a pena:

  * Merge muito melhor do que o CVS
  * Suporta renomear e mover arquivos/diret&oacute;rios e manter o hist&oacute;rico
  * Suporta revis&otilde;es em symlinks e diret&oacute;rios
  * Manuten&ccedil;&atilde;o mais f&aacute;cil do que o CVS: backup, protocolos 
  * Suporta dump do reposit&oacute;rio

Mas o SubVersion ainda tem poucas ferramentas com suporte a ele. Atualmente uso um <a target="_blank" href="http://vcsgeneric.netbeans.org/profiles/">plugin do Netbeans</a>.