---
id: 164
title: Dicas de SSH
date: 2007-06-13T18:08:00+00:00
author: Claudio Miranda
layout: post
permalink: /2007/06/Dicas-de-SSH/
categories:
  - Dicas
---
Seguem duas dicas no uso de ssh que facilitam um pouco a sua vida.&nbsp;
  
  


### Para efetuar login sem solicitar senha
  
 {#Paraefetuarloginsemsolicitarsenha}

Essa dica é para SO linux, para windows eu não sei.
  
  


 _1. Geração de chave RSA de 2048 bits_ 

<pre>ssh-keygen -b 2048 -t rsa
</pre>

Não digite um passphrase (aperte a tecla enter) 

_Atualização em 10/Ago/2007: [É possível usar um passphrase e o ssh-agent](http://www.claudius.com.br/blog/claudio/dicas/Dicas-de-SSH-v2) para ter a facilidade de não invocar a senha do passphrase em toda conexão e manter sua chave privada segura._&nbsp; 

 _2. Copiar a chave pública para o servidor desejado_ 

<pre>scp ~/.ssh/id_rsa.pub usuario@10.0.0.5:/home/usuario/.ssh/
</pre>

 _3. Colocar a sua chave pública como chave confiável_ 

Acessar o servidor por ssh (informando a senha ainda) e colocar a sua chave pública na lista confiável 

<pre>cd .ssh
cat id_rsa.pub &gt;&gt; authorized_keys
</pre>

Essa dica eu tirei do [site dicas-l](http://www.dicas-l.com.br/dicas-l/20050804.php), mas modifiquei algumas coisas. 

### Diminuir o tempo de login no SSH
  


Em algumas situações (desconhecidas) ao realizar um ssh para uma máquina, pode demorar cerca de 3 a 5s. Para diminuir esse tempo é necessário editar o arquivo <tt>/etc/ssh/sshd_config</tt> e configurar as seguintes opções:
  
  


<more> </more>

<pre>GSSAPIAuthentication no
GSSAPICleanupCredentials yes
</pre>