---
id: 212
title: Jetty no Solaris 10
date: 2008-07-16T14:10:58+00:00
author: Claudio Miranda
layout: post
permalink: /2008/07/Jetty-no-Solaris-10/
categories:
  - Java
---
![](/resources/claudio/jetty_logo.gif)
     
![](/resources/claudio/opensolaris_logo.png)
  
![](/resources/claudio/java-logo.jpg)

Segue uma contribuição que fiz para o projeto Jetty, para inicializar/parar/reiniciar o Jetty, usando o serviço nativo SMF do Solaris 10.

Os softwares necessários

  * [Jetty 6.11](http://www.mortbay.org/jetty-6/)
  * Solaris 10 
  * JDK 6u7

Outra versão do Jetty irá funcionar, basta adaptar o script jetty.sh

Essa contribuição está no [OpenSolaris](http://opensolaris.org/os/community/smf/manifests/) e no [Jetty, pelo patch 639](https://jira.codehaus.org/browse/JETTY-639).

A vantagem do uso do SMF que fiz

  * Uso de portas privilegiadas por usuário não root (permissão de privilégios)
  * Restar do serviço automaticamente (watchdog)
  * Padronização para o ambiente Solaris no uso do serviço



**Sobre o Jetty**

Para quem não conhece o Jetty, é um servidor Java, como o Tomcat. Ele é muito bom, uso-o há muito tempo, inclusive ele foi o servidor web que acompanhava o JBoss antes do tomcat. [Vejam alguns usuários do Jetty](http://docs.codehaus.org/display/JETTY/Jetty+Powered).

O Jetty é reconhecido por ter baixo consumo de memória e recursos, permitir o uso da API de maneira embutida (Embedded), já usei em projetos profissionais.

De fato o Jetty é usado neste site [(claudius.com.br)](http://claudius.com.br)&nbsp; e no do SouJava (soujava.org.br).