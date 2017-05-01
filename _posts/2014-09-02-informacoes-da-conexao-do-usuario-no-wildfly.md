---
id: 453
title: Informacoes da conexão do usuário no wildfly
date: 2014-09-02T23:37:25+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=453
permalink: /2014/09/informacoes-da-conexao-do-usuario-no-wildfly/
categories:
  - Dicas
tags:
  - wildfly
---
Uma <a href="https://github.com/wildfly/wildfly-core/pull/89" target="_blank">contribuição que fiz para o wildfly foi aceita</a>, relacionada a funcionalidade de exibir as informações da conexão do usuário logado no Wildfly (<a href="https://issues.jboss.org/browse/WFCORE-73" target="_blank">WFCORE-73</a>).

Atualmente quando o usuário se conectar com o jboss-cli, não é possível mostrar as informações da conexão, esta contribuição mostra: nome do usuário, desde quando está logado, roles associadas, certificado ssl. Pode-se fazer um clone e build do wildfly para ter acesso a estas funcionalidades, que estará disponível na próxima versão do Wildfly.

Adicionei o comando connection-info que mostra as seguintes informações

  * Logado sem SSL, sem RBAC

<pre>[domain@pavlov-0:9990 /] connection-info 
Username               admin, granted role ["SuperUser"] 
Logged since           Tue Sep 02 22:45:32 BRT 2014      
Not an SSL connection.                              
</pre>

&nbsp;

  * Logado com SSL, sem RBAC

<pre>[domain@pavlov-0:9993 /] connection-info
Username     admin, granted role ["SuperUser"]                             
Logged since Tue Sep 02 22:48:28 BRT 2014                                  
Subject      CN=mgmt-connector,OU=jboss,O=jboss,L=Brasilia,ST=DF,C=BR      
Issuer       CN=mgmt-connector, OU=jboss, O=jboss, L=Brasilia, ST=DF, C=BR 
Valid from   Fri Aug 08 01:13:16 BRT 2014                                  
Valid to     Thu Nov 06 02:13:16 BRST 2014                                 
SHA1         fa:25:f4:cf:57:89:ce:ff:97:82:9d:b4:c8:b1:67:ef:b3:08:a8:b4   
MD5          e6:67:14:c7:86:84:d3:22:14:21:e7:43:09:05:a4:7f
</pre>

&nbsp;

  * Logado com SSL, com RBAC

<pre>[domain@pavlov-0:9993 /] connection-info
Username     claudio, granted roles ["Maintainer","Operator","Deployer"]   
Logged since Tue Sep 02 22:52:22 BRT 2014                                  
Subject      CN=mgmt-connector,OU=jboss,O=jboss,L=Brasilia,ST=DF,C=BR      
Issuer       CN=mgmt-connector, OU=jboss, O=jboss, L=Brasilia, ST=DF, C=BR 
Valid from   Fri Aug 08 01:13:16 BRT 2014                                  
Valid to     Thu Nov 06 02:13:16 BRST 2014                                 
SHA1         fa:25:f4:cf:57:89:ce:ff:97:82:9d:b4:c8:b1:67:ef:b3:08:a8:b4   
MD5          e6:67:14:c7:86:84:d3:22:14:21:e7:43:09:05:a4:7f

</pre>

&nbsp;