---
id: 119
title: Gerenciamento de pacotes no Solaris
date: 2006-11-30T16:18:46+00:00
author: Claudio Miranda
layout: post
permalink: /2006/11/Gerenciamento-de-pacotes-no-Solaris/
categories:
  - Dicas
---
<div class="excerpt">
  No linux estou acostumado a usar ferramentas para gerenciamento de pacotes e tratar inconsistências. Já solaris existem ferramentas por linha de comando para trabalhar (pkgadd, pkgrm, etc.), e algumas vezes a instalação do pacote é realizada por algum instalador (Java Enterprise System por exemplo), e algumas vezes ao remover pacotes pelo instalador ocorrem problemas e sobram arquivos órfãos ou pacotes inconsistentes.
</div>

No linux estou acostumado a usar ferramentas para gerenciamento de pacotes e tratar inconsistências. Já solaris existem ferramentas por linha de comando para trabalhar (pkgadd, pkgrm, etc.), e algumas vezes a instalação do pacote é realizada por algum instalador (Java Enterprise System por exemplo), e algumas vezes ao remover pacotes pelo instalador ocorrem problemas e sobram arquivos órfãos ou pacotes inconsistentes. 

Tentei tratar manualmente esses pacotes, mas era muito trabalhosos ficar pesquisando e digitando tudo em linha de comando, foi então que descobri uma ferramenta visual que gerencia isso e torna mais fácil a operação, é o prodreg. 

<cut>

[<img src="/resources/claudio/061130_solaris_prodreg_sm.png" align="bottom" border="0" hspace="0" vspace="0" />](/resources/claudio/061130_solaris_prodreg.png) 

Com ele foi possível remover vários pacotes inconsistentes.&nbsp; 

Para invocar, tem de estar com credenciais de root e digitar no prompt&nbsp;&nbsp;

<pre>prodreg swing</pre></p> 

</cut>