---
id: 433
title: Console administrativo do Wildfly em https
date: 2014-08-08T03:43:48+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=433
permalink: /2014/08/console-administrativo-do-wildfly-em-https/
categories:
  - Dicas
---
Quer deixar o console administrativo do seu Wildly (ou JBoss) seguro, por https, veja esta dica.

Isso irá proteger o acesso pela interface web e pelo jboss-cli.

No wildfly o acesso administrativo foi consolidado em uma porta apenas, 9990 ou na porta segura (ssl) em 9993 (por padrão).

Primeiro passo é criar o certificado digital auto-assinado com a ferramenta keytool. Vá no diretório conf de sua instância (standalone ou domínio), crie o diretório certs e depois o certificado. Altere os parâmetros abaixo, conforme sua necessidade.

<pre>keytool -genkey -alias wildfly_mgmt -keyalg RSA -keystore wildfly.jks -storepass admin123 -keypass admin123 --dname "CN=mgmt-connector,OU=jboss,O=jboss,L=Brasilia,S=DF,C=BR"</pre>

Agora vamos configurar o Wildfly

## Modo Standalone

Editar standalone.xml e alterar de acordo com o exemplo abaixo, foi adicionado a seção server-identities e logo abaixo na seção http-interfaces.

<pre>&lt;security-realm name="ManagementRealm"&gt;
    &lt;server-identities&gt;
<strong>        &lt;ssl&gt;</strong>
<strong>            &lt;keystore path="${jboss.server.config.dir}/certs/wildfly.jks" keystore-password="admin123" /&gt;</strong>
<strong>        &lt;/ssl&gt;</strong>
    &lt;/server-identities&gt;

&lt;management-interfaces&gt;
    &lt;http-interface security-realm="ManagementRealm" http-upgrade-enabled="true"&gt;
        &lt;socket-binding <strong>https="management-https"</strong>/&gt;
    &lt;/http-interface&gt;
&lt;/management-interfaces&gt;</pre>

Inicie o wildfly em modo standalone e acesse pela interface web em https://localhost:9993, será solicitado a confirmação para confiar no certificado e pronto.

Para acesso pelo jboss-cli é necessário alterar o jboss-cli.xml, conforme abaixo, para especificar o protocolo https como padrão e a porta.

<pre>&lt;default-protocol use-legacy-override="true"&gt;<strong>https-remoting</strong>&lt;/default-protocol&gt;

&lt;!-- The default controller to connect to when 'connect' command is executed w/o arguments --&gt;
&lt;default-controller&gt;
<strong>    &lt;protocol&gt;https-remoting&lt;/protocol&gt;</strong>
    &lt;host&gt;localhost&lt;/host&gt;
<strong>    &lt;port&gt;9993&lt;/port&gt;</strong>
&lt;/default-controller&gt;</pre>

Então será possível acessar pelo jboss-cli sem informar parâmetros adicionais, apenas um ./jboss-cli.sh -c

## Modo Domínio

O modo domínio tem uma configuração diferente, edite o host.xml conforme mostrado abaixo:

<pre>&lt;security-realm name="ManagementRealm"&gt;
<strong>    &lt;server-identities&gt;
        &lt;ssl&gt;
            &lt;keystore path="${jboss.domain.config.dir}/certs/wildfly.jks" keystore-password="admin123" /&gt;
        &lt;/ssl&gt;
    &lt;/server-identities&gt;</strong>

&lt;management-interfaces&gt;
    &lt;native-interface security-realm="ManagementRealm"&gt;
        &lt;socket interface="management" port="${jboss.management.native.port:9999}"/&gt;
    &lt;/native-interface&gt;
    &lt;http-interface security-realm="ManagementRealm" http-upgrade-enabled="true"&gt;
        &lt;socket interface="management" <strong>secure-port="${jboss.management.http.port:9993}"</strong>/&gt;
    &lt;/http-interface&gt;
&lt;/management-interfaces&gt;
</pre>

O jboss-cli.xml deverá ser alterado conforme mostrado na seção anterior.

Avise se ocorreu algum erro ou se lhe ajudou.

&nbsp;