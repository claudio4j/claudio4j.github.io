---
id: 459
title: Show deployment timestamp on wildfly
date: 2014-09-24T23:38:33+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=459
permalink: /2014/09/show-deployment-timestamp-on-wildfly/
categories:
  - Java
tags:
  - wildfly
---
<a href="https://github.com/wildfly/wildfly-core/pull/161" target="_blank">A contribution to wildfly</a> to display when the deployed application was enabled or disabled, see below the attributes enabled-timestamp and disabled-timestamp.

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

I will add this feature to the web console, this will make it easier to track when the application was enabled and disabled.