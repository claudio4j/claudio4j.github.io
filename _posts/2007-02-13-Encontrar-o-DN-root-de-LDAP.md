---
id: 137
title: Encontrar o DN root de LDAP
date: 2007-02-13T18:17:44+00:00
author: Claudio Miranda
layout: post
permalink: /2007/02/Encontrar-o-DN-root-de-LDAP/
categories:
  - Dicas
---
Publiquei há alguns dias uma maneira de [encontrar o DN raiz de um MS Active Directory](http://blog.claudius.com.br/blog/claudio//2007/02/05/3-Dicas-Encontrar-o-DN-do-AD-Download-de-conte%C3%BAdo-wiki-Firefox-ler-zip), através de uma ferramenta windows. 

Então verifiquei que existe uma maneira (mais fácil) de descobrir todos os DN root configurados: 

<pre>ldapsearch -x&nbsp; -h 199.199.199.180 -p 389 -s base -b "" "objectClass=*" namingContexts
</pre>