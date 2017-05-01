---
id: 157
title: Permissão em arquivo policy
date: 2007-05-04T05:16:44+00:00
author: Claudio Miranda
layout: post
permalink: /2007/05/Permissao-em-arquivo-policy/
categories:
  - Dicas
---
Alguns dias atrás foi necessário habilitar um mode trace do driver DB2, em uma aplicação do cliente. No entanto ocorria o seguinte erro ao usar o trace: 

<pre>Caused by: java.security.AccessControlException: access denied (java.lang.reflect.ReflectPermission suppressAccessChecks)
        at java.security.AccessControlContext.checkPermission(AccessControlContext.java:264)
        at java.lang.SecurityManager.checkPermission(SecurityManager.java:568)</pre>

Então, pensei &#8220;É só colocar o grant com codebase e permissão e está tudo resolvido. Então coloquei a seguinte linha no policy do AppServer. Sendo que no caminho do driver, são vários arquivos .jar
  
  
</p> 

<pre>grant codeBase "file:///caminho/driver-db2/-" {
        permission java.lang.reflect.ReflectPermission "suppressAccessChecks";
};</pre>

Mas ao rodar a aplicação novamente, ocorreu o mesmo erro de falta de permissão (access denied), como mostrado anteriormente. 

Então após mais alguns testes e variações desta configuração, resolvi remover o codeBase do grant. E funcionou. Claro que deixar isso desabilitado tem <a target="_blank" href="http://java.sun.com/j2se/1.5.0/docs/guide/security/permissions.html#ReflectPermission">questões de segurança envolvido</a>. Convenhamos que se alguém quiser fazer algum malefício, essa opção não ira colaborar imensamente. Visto que alguns <a target="_blank" href="http://labs.jboss.com/">outros appservers nem habilitam o security manager</a>.