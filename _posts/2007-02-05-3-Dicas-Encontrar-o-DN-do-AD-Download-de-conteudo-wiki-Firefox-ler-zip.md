---
id: 130
title: '3 Dicas: Encontrar o DN do AD &#8211; Download de conteúdo wiki &#8211; Firefox ler .zip'
date: 2007-02-05T15:21:38+00:00
author: Claudio Miranda
layout: post
permalink: /2007/02/3-Dicas-Encontrar-o-DN-do-AD-Download-de-conteudo-wiki-Firefox-ler-zip/
categories:
  - Dicas
---
Como fiquei vários dias sem escrever nada, agora seguem 3 dicas, que são mais relacionadas ao meu trabalho. Mas como não foi fácil encontrar na internet, acredito que existam outras pessoas que possam precisar dessa informação. 

  1. Normalmente o Microsoft Active Directory (AD) é usado como repositório de usuários em grandes organizações, considerando isso, os serviços de autenticações precisam ser configurados para acessar o AD. 
    No caso de Java, então o acesso ao AD acaba sendo através de JNDI, através de um SPI LDAP. Então para isso é necessário saber qual o DN (Distinguished Name) de acesso ao AD.
    
    Para saber qual o DN do AD, procurei na ferramenta de administração do AD mas não encontrei nada sobre o DN. Então recorri a um colega da Sun (obrigado Marcos Belarmino), que me informou sobre o comando <font face="courier new,courier,monospace">ldifde</font>, para realizar exportação da árvore completa do AD (note que não há solicitação de senha). A sintaxe é: <font face="courier new,courier,monospace">ldifde -f saida_ad.ldif</font>
    
    Então basta abrir o arquivo saida_ad.ldif que os respectivos DNs e usuários estarão lá.

  2. A outra dica é com relação a uma facilidade de exportação do wiki Confluence, onde é possível exportar qualquer espaço do wiki para HTML e depois compactar em um arquivo .zip para realizar download e ler off-line. 
    Para fazer isso, acesse qualquer wiki confluence, clique em &#8220;Browse Space&#8221; no canto superior direito
    
    <img src="/resources/claudio/070205_confluence1.png" align="right" border="0" hspace="0" vspace="0" />
    
      
    Depois clique em &#8220;Export Space&#8221; no menu do lado esquerdo.
    
    <img src="/resources/claudio/070205_confluence2.png" align="bottom" border="0" hspace="0" vspace="0" />
    
    Então, é só escolher as opções e clicar em download.

  3. No firefox é possível ler o conteúdo de um arquivo .zip, com isso não é necessário descompactar o arquivo. Basta informar uma URL da seguinte maneira. 
    <font face="courier new,courier,monospace">jar:file:///home/claudio/downloads/WW-20070204-18_16_03.zip!/WW/Site.html</font>
    
    Essa dica pode ser mais bacana em situações onde é necessário ter vasta documentação HTML e economizar espaço, por exemplo em documentações que acompanham CDs. Essa dica eu peguei em um <a target="_blank" href="http://blogs.sun.com/roumen/entry/netbeans_documentation_jumbo_pack#comment-1170531332000">comentário de um blog</a>.
    
    </li> </ol> 
    
    
    
      
    &nbsp;