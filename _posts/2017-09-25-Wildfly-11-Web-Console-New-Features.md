---
title: 'Wildfly 11 - Web Console new features'
author: Claudio Miranda
permalink: /2017/09/wildfly-11-web-console-new-features
tags:
  - wildfly
  - jboss
  - java
---

This blog post will highlight the new features of Web Console for [Wildfly 11](http://wildfly.org). [Wildfly 11 is in Candidate Release](http://wildfly.org/news/2017/08/25/WildFly11-CR1-Released/) right now, [you can download it](http://wildfly.org/downloads), it's free. 

You can read [what is new in WildFly 11](http://wildfly.org/news/2017/08/25/WildFly11-CR1-Released/). For now on I will talk about the new features that were added to Web Console. Besides the new features, there were many bug fixed and enhancements, you can check the list of fixed issues since Wildfly 10.1.

## Elytron Subsystem

There is a new subsystem named Elytron, it replaces the picketbox security framework with an advanced capabilities such as privilege propagation across multiple service invocations, identity switching, pre-request TLS verification, and rich security policies.

The elytron configuration is available for every profile, the entry point is the "Security - Elytron" item menu.

{% include figure image_path="/images/20170925-elytron_1.png" alt="Web Console - Elytron Subsystem" caption="The entry point for elytron configuration" %}

From there you may access the configurations for: Factories, Transformers, Mappers, Decoders, Security Realms, Authentication, Key Store, Credential Store, SSL Context, etc. Elytron is a new subsystem but it contains many resources to configure. See some screenshots.

{% include figure image_path="/images/20170925-elytron_2.png" alt="Web Console - Elytron Subsystem" caption="SSL Options - Key Store resource configuration" %}


{% include figure image_path="/images/20170925-elytron_3.png" caption="Security Realm option - Properties Realm configuration" %}

{% include figure image_path="/images/20170925-elytron_4.png" caption="Permission Mapper option - Simple Permission Mapper configuration" %}

There is also a runtime view to display the aliases for the credential store.

{% include figure image_path="/images/20170925-elytron_5.png" caption="Display aliases for credential stores" %}

## EJB Security Domain Mapping

The EJB subsystem allows to configure mapping a security domain for a deployed application.

{% include figure image_path="/images/20170925-ejb_sec_domain.png" caption="EJB Application Security Domain Mapping" %}

## JMS Bridge in Messaging subsystem

The Messaging subsystem in web console allows the user to manage JMS Bridges.

{% include figure image_path="/images/20170925-messaging_1.png" caption="Messaging - JMS Bridge" %}

{% include figure image_path="/images/20170925-messaging_2.png" caption="Messaging - Add a JMS Bridge" %}

{% include figure image_path="/images/20170925-messaging_3.png" caption="Messaging - JMS Bridge resource" %}

There is also a runtime view to monitor pool statistics for Pooled Connection Factory connections.

{% include figure image_path="/images/20170925-messaging_4.png" caption="Monitor pool statistics for Pooled Connection Factory connections" %}

{% include figure image_path="/images/20170925-messaging_5.png" caption="Monitor Prepared Transactions" %}

## Web Services - Client and Endpoint configuration

User are allowed to configure Client and Endpoint configurations.

{% include figure image_path="/images/20170925-webservices_1.png" caption="Client and Endpoint Configuration" %}

The Pre/Post Handler Chain is also allowed to configure.

{% include figure image_path="/images/20170925-webservices_2.png" caption="Pre/Post Handler Chain Configuration" %}

## Undertow

Web Console users are allowed to configure undertow filters, application security domain mapping to deployed applications and map response header filter to hosts.

{% include figure image_path="/images/20170925-undertow_1.png" caption="Entrypoint for the Undertow Filters" %}

{% include figure image_path="/images/20170925-undertow_2.png" caption="Response header filter" %}

{% include figure image_path="/images/20170925-undertow_3.png" caption="Undertow Application Security Domain" %}

{% include figure image_path="/images/20170925-undertow_4.png" caption="Response header filters mapped to a host" %}

{% include figure image_path="/images/20170925-undertow_5.png" caption="Map an undertow response header filter to a host" %}


## Runtime view - Hosts

Previously, when users wanted to reload or restart a host controller, they went to CLI to run those commands, now it is possible to reload or restart a host controller from the web console.

The restart option calls the management command as `:shutdown(restart=true)`

The reload option calls the management command as `:reload()`

{% include figure image_path="/images/20170925-host_1.png" caption="Reload and restart options to host controller" %}

{% include figure image_path="/images/20170925-host_2.png" caption="Reload host confirmation" %}

Also, there is a the configuration-changes log, to register all changes performed to a host controller. Users are allowed to enable/disable and monitor the configurations changes.

{% include figure image_path="/images/20170925-host_3.png" caption="Configuration Changes" %}

## Runtime view - Server

Previously, when the server was in a blocked state, not responding, users needed to kill the server with a kill command (from a command prompt). Wildfly already contains an operation `kill` to destroy a server process. Web console allows the user to invoke the `kill` operation on a server, it is named <p><small>Force shutdown" %}, see below the menu option.

{% include figure image_path="/images/20170925-server_kill.png" caption="Option to shutdown a server" %}

## Runtime view - Monitor Batch executions

Application may package batch jobs and execute them in Wildfly application runtime. The batch subsystem allows to monitor them

{% include figure image_path="/images/20170925-monitor_batch.png" caption="Monitor batch executions" %}

## Runtime view - Monitor datasource pool statistics

There is a new view to monitor datasource pool statistics.

{% include figure image_path="/images/20170925-monitor_ds_pool_stats.png" caption="Monitor datasource pool statistics" %}

## Browse deployment contents

It is possible to browse the content of deployments, this is useful when an user wants to navigate the contents of deployments and download its contents.

Emmanuel Hugonnet [blogged a detailed view](http://wildfly.org/news/2017/09/08/Exploded-deployments/) about this feature.

{% include figure image_path="/images/20170925-browse_1.png" caption="Browse deployments option" %}

It shows the full path of each content item and its size.

{% include figure image_path="/images/20170925-browse_2.png" caption="Browse deployments" %}




