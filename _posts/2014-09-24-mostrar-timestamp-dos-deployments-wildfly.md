---
id: 457
title: Mostrar timestamp dos deployments no wildfly
date: 2014-09-24T23:32:55+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=457
permalink: /2014/09/mostrar-timestamp-dos-deployments-wildfly/
categories:
  - Java
tags:
  - wildfly
---
Fiz uma <a href="https://github.com/wildfly/wildfly-core/pull/161" target="_blank">contribuição para o wildfly</a>, para mostrar o timestamp dos momentos que a aplicação foi habilitada e desabilitada, vejam os atributos enabled-timestamp e disabled-timestamp no exemplo abaixo.

<pre>[standalone@localhost:9990 /] ./deployment=jboss-kitchensink.war:read-resource
{
    "outcome" =&gt; "success",
    "result" =&gt; {
        "content" =&gt; [{"hash" =&gt; bytes {
            0x13, 0x75, 0x1e, 0x5f, 0xeb, 0x65, 0x1e, 0xe0,
            0x4f, 0x8e, 0x29, 0x33, 0x87, 0xf9, 0xec, 0xdf,
            0x1c, 0xa8, 0xff, 0xc7
        }}],
<strong>        "disabled-time" =&gt; 1411611922962L,</strong>
<strong>        "disabled-timestamp" =&gt; "2014-09-24 23:25:22,962 BRT",</strong>
        "enabled" =&gt; false,
<strong>        "enabled-time" =&gt; 1411611399707L,</strong>
<strong>        "enabled-timestamp" =&gt; "2014-09-24 23:16:39,707 BRT",</strong>
        "name" =&gt; "jboss-kitchensink.war",
        "persistent" =&gt; false,
        "runtime-name" =&gt; "jboss-kitchensink.war",
        "subdeployment" =&gt; undefined,
        "subsystem" =&gt; undefined
    }
}</pre>

Vou implementar essa funcionalidade na ferramenta de administração web, assim ficará fácil rastrear os momentos que a aplicação sofreu intervenções.