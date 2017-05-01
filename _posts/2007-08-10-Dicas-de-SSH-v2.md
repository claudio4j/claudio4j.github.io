---
id: 175
title: Dicas de SSH (v2)
date: 2007-08-10T21:26:39+00:00
author: Claudio Miranda
layout: post
permalink: /2007/08/Dicas-de-SSH-v2/
categories:
  - Dicas
---
<img align="right" src="/resources/claudio/tips_icon.gif" alt="Dicas" hspace="80" />
  
[Em junho publiquei uma dica no uso de ssh](http://www.claudius.com.br/blog/claudio/dicas/Dicas-de-SSH), sem solicitar a senha do servidor. Isso envolve criar uma chave privada/pública e colocar a chave pública no servidor. 

Ocorre que essa chave pode ter uma senha para proteger contra acesso não autorizado (passphrase), que é diferente da senha de login ssh. 

Ao usar a dica que coloquei anteriormente, mas informando um passphrase, em cada conexão com o ssh, é necessário informar a senha do passphrase, o que invalida toda a dica, onde não é necessário informar senha nenhuma. Dai o motivo de não informar um passphrase. 

Então conversando com o colega [Bruno Borges da Summa](http://www.brunoborges.com.br/) (aka Miojo), ele disse que usou o ssh-agent para proteger o passphrase. 

Então complementado a minha dica anterior, 

  1. _Geração de chave RSA de 2048 bits_
    
    </p> 
    <pre>ssh-keygen -b 2048 -t rsa
</pre>
    
    Desta vez informe um passphrase 

  2. _Use o ssh-agent para guardar o acesso ao passphrase_ 
    
    </p> 
    <pre>$ eval `ssh-agent`
$ ssh-add &lt;private key file&gt; # e.g. ~/.ssh/id_RSA
$ ssh-add -l</pre>

A dica de como [usar o ssh-agent, peguei de outro site](http://www.snailbook.com/faq/no-passphrase.auto.html).
  
  


­

Agora pode [seguir o restante da dica anterior a partir do passo 2](http://www.claudius.com.br/blog/claudio/dicas/Dicas-de-SSH)