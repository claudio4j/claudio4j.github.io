---
id: 358
title: Filtros globais no JBoss EAP 6
date: 2013-10-03T14:20:37+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=358
permalink: /2013/10/filtros-globais-no-jboss-eap-6/
categories:
  - Dicas
  - Java
tags:
  - dicas
  - java
---
Uma funcionalidade bastante usada no JBoss 5 é a capacidade de adicionar filtros (listeners, servlets, etc.) globais. Por exemplo, para toda aplicação .war instalada, devem ter um filtro de segurança. Esse filtro é adicionado direto no JBoss, de maneira que a aplicação não tem escolha se usa ou não. No JBoss 5 é usado o arquivo deployers/jbossweb.deployer/web.xml para configuração destes parâmetros.

No JBoss EAP 6 (ou AS 7), não existe esse arquivo deployers/jbossweb.deployer/web.xml. Então veja uma solução alternativa e java puro para adicionar filtros globais.

Implementação da interface ServletContainerInitializer

<pre>public class ServletFilterConfigurator implements ServletContainerInitializer {

    public void onStartup(Set&lt;Class&lt;?&gt;&gt; c, ServletContext ctx) throws ServletException {
        System.out.println("&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; registering filter for " + ctx.getContextPath());
        FilterRegistration fReg = ctx.addFilter("myGlobalFilter", com.claudius.MyGlobalFilter.class);
        fReg.addMappingForUrlPatterns(null, true, "/*");
    }

}</pre>

Ativação da classe, criar um arquivo META-INF/services/javax.servlet.ServletContainerInitializer, cujo conteúdo é FQCN acima.

<pre>com.claudius.ServletFilterConfigurator</pre>

Isso serve para quando o servlet container, carregar o .jar, invocar a classe do serviço.

No lado do JBoss EAP 6, crie um módulo estático e no domain.xml declare-o como módulo global, desta maneira este módulo é automaticamente carregado para todas as aplicações.

Veja [um projeto que mostra o filtro global em funcionamento](/wp-content/uploads/2013/10/globalwefilter-lib.zip).

&nbsp;