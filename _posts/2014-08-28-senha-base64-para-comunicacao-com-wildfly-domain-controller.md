---
id: 442
title: Senha base64 para comunicação com wildfly domain controller
date: 2014-08-28T15:04:55+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=442
permalink: /2014/08/senha-base64-para-comunicacao-com-wildfly-domain-controller/
categories:
  - Dicas
---
Quando configura-se o Wildfly em modo domínio com host controllers adicionais, é necessário que exista um usuário no HC (host controller) para comunicar-se com o DC (domain controller). Esta comunicação é especificado no host.xml do HC, onde é necessário informar o usuário e senha, esta no valor base64, exemplo:

<pre>&lt;management&gt;
    &lt;security-realms&gt;
        &lt;security-realm name="ManagementRealm"&gt;
<strong>            &lt;server-identities&gt;</strong>
<strong>                &lt;secret value="YWRtaW4xMjNA"/&gt;</strong>
<strong>            &lt;/server-identities&gt;</strong>

&lt;domain-controller&gt;
    &lt;remote host="${jboss.domain.master.address}" port="${jboss.domain.master.port:9999}" security-realm="ManagementRealm" <strong>username="admin2"</strong> /&gt;
&lt;/domain-controller&gt;</pre>

Caso não saiba qual o valor base64 da senha, basta usar o comando base64 do linux para obter a senha, lembre-se de remover o caracter de quebra de linha do echo, veja o valor base64 para a senha: **admin123@**

<pre>$ echo -n "admin123@" | base64 
YWRtaW4xMjNA
</pre>

Isso é útil em alguns cenários onde cria-se o usuário com o add-user.sh não interativo e deseja-se saber o valor base64 da senha.