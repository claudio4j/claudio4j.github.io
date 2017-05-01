---
id: 354
title: Propagação de contexto de segurança no JBoss EAP 6
date: 2013-09-02T14:49:00+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=354
permalink: /2013/09/propagacao-de-contexto-de-seguranca-no-jboss-eap-6/
categories:
  - Java
---
Contribui um quickstart, que é um pequeno aplicativo que mostra uma determinada funcionalidade do JBoss EAP 6.1.

O quickstart é o &#8220;<a href="https://github.com/jboss-jdf/jboss-as-quickstart/tree/master/ejb-security-propagation " target="_blank">ejb-security-propagation</a>&#8220;, mostra um cenário, onde dado uma página web protegida por um security domain, ao acessar um EJB em outro servidor, este EJB protegido por um security domain, as credenciais de autenticação da camada web é propagada para o EJB.

&nbsp;