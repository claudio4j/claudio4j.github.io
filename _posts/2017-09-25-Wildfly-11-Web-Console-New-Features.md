---
title: 'Wildfly 11 - Web Console new features'
author: Claudio Miranda
layout: post
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

![Web Console - Elytron Subsystem]({{ site.baseurl }}/images/20170925-elytron_1.png "Web Console - Elytron Subsystem")
<p><small>The entry point for elytron configuration</small></p>

From there you may access the configurations for: Factories, Transformers, Mappers, Decoders, Security Realms, Authentication, Key Store, Credential Store, SSL Context, etc. Elytron is a new subsystem but it contains many resources to configure. See some screenshots.

![Web Console - Elytron Subsystem]({{ site.baseurl }}/images/20170925-elytron_2.png "Web Console - Elytron Subsystem")
<p><small>SSL Options - Key Store resource configuration</small></p>

![Web Console - Elytron Subsystem]({{ site.baseurl }}/images/20170925-elytron_3.png "Web Console - Elytron Subsystem")
<p><small>Security Realm option - Properties Realm configuration</small></p>

![Web Console - Elytron Subsystem]({{ site.baseurl }}/images/20170925-elytron_4.png "Web Console - Elytron Subsystem")
<p><small>Permission Mapper option - Simple Permission Mapper configuration</small></p>

There is also a runtime view to display the aliases for the credential store.

![Web Console - Elytron Subsystem]({{ site.baseurl }}/images/20170925-elytron_5.png "Web Console - Elytron Subsystem")
<p><small>Display aliases for credential stores</small></p>

## EJB Security Domain Mapping

The EJB subsystem allows to configure mapping a security domain for a deployed application.

![Web Console - EJB Application Security Domain Mapping]({{ site.baseurl }}/images/20170925-ejb_sec_domain.png "Web Console - EJB Application Security Domain Mapping")
<p><small>EJB Application Security Domain Mapping</small></p>

## JMS Bridge in Messaging subsystem

The Messaging subsystem in web console allows the user to manage JMS Bridges.

![Web Console - Messaging - JMS Bridge]({{ site.baseurl }}/images/20170925-messaging_1.png "Web Console - Messaging - JMS Bridge")
<p><small>Messaging - JMS Bridge</small></p>

![Web Console - Messaging - JMS Bridge]({{ site.baseurl }}/images/20170925-messaging_2.png "Web Console - Messaging - JMS Bridge")
<p><small>Messaging - Add a JMS Bridge</small></p>

![Web Console - Messaging - JMS Bridge]({{ site.baseurl }}/images/20170925-messaging_3.png "Web Console - Messaging - JMS Bridge")
<p><small>Messaging - JMS Bridge resource</small></p>

There is also a runtime view to monitor pool statistics for Pooled Connection Factory connections.

![Web Console - Messaging Runtime - Pool statistics]({{ site.baseurl }}/images/20170925-messaging_4.png "Web Console - Messaging Runtime - Pool statistics")
<p><small>Monitor pool statistics for Pooled Connection Factory connections</small></p>

![Web Console - Messaging Runtime - Prepared Transactions]({{ site.baseurl }}/images/20170925-messaging_5.png "Web Console - Messaging Runtime - Prepared Transactions")
<p><small>Monitor Prepared Transactions</small></p>

## Web Services - Client and Endpoint configuration

User are allowed to configure Client and Endpoint configurations.

![Web Console - Web Services Configuration]({{ site.baseurl }}/images/20170925-webservices_1.png "Web Console - Web Services Configuration")
<p><small>Client and Endpoint Configuration</small></p>

The Pre/Post Handler Chain is also allowed to configure.

![Web Console - Web Services Configuration]({{ site.baseurl }}/images/20170925-webservices_2.png "Web Console - Web Services Configuration")
<p><small>Pre/Post Handler Chain Configuration</small></p>

## Undertow

Web Console users are allowed to configure undertow filters, application security domain mapping to deployed applications and map response header filter to hosts.

![Undertow Filters]({{ site.baseurl }}/images/20170925-undertow_1.png "Undertow Filters")
<p><small>Entrypoint for the Undertow Filters</small></p>

![Response header filter]({{ site.baseurl }}/images/20170925-undertow_2.png "Response header filter")
<p><small>Response header filter</small></p>

![Undertow Application Security Domain]({{ site.baseurl }}/images/20170925-undertow_3.png "Undertow Application Security Domain")
<p><small>Undertow Application Security Domain</small></p>

![Response header filters mapped to a host]({{ site.baseurl }}/images/20170925-undertow_4.png "Response header filters mapped to a host")
<p><small>Response header filters mapped to a host</small></p>

![Map an undertow response header filter to a host]({{ site.baseurl }}/images/20170925-undertow_5.png "Map an undertow response header filter to a host")
<p><small>Map an undertow response header filter to a host</small></p>


## Runtime view - Hosts

Previously, when users wanted to reload or restart a host controller, they went to CLI to run those commands, now it is possible to reload or restart a host controller from the web console.

The restart option calls the management command as `:shutdown(restart=true)`

The reload option calls the management command as `:reload()`

![Hosts options]({{ site.baseurl }}/images/20170925-host_1.png "Hosts options")
<p><small>Reload and restart options to host controller</small></p>

![Reload host confirmation]({{ site.baseurl }}/images/20170925-host_2.png "Reload host confirmation")
<p><small>Reload host confirmation</small></p>

Also, there is a the configuration-changes log, to register all changes performed to a host controller. Users are allowed to enable/disable and monitor the configurations changes.

![Configuration Changes]({{ site.baseurl }}/images/20170925-host_3.png "Configuration Changes")
<p><small>Configuration Changes</small></p>

## Runtime view - Server

Previously, when the server was in a blocked state, not responding, users needed to kill the server with a kill command (from a command prompt). Wildfly already contains an operation `kill` to destroy a server process. Web console allows the user to invoke the `kill` operation on a server, it is named <p><small>Force shutdown</small></p>, see below the menu option.

![Shutdown server]({{ site.baseurl }}/images/20170925-server_kill.png "Shutdown server")
<p><small>Option to shutdown a server</small></p>

## Runtime view - Monitor Batch executions

Application may package batch jobs and execute them in Wildfly application runtime. The batch subsystem allows to monitor them

![Monitor batch executions]({{ site.baseurl }}/images/20170925-monitor_batch.png "Monitor batch executions")
<p><small>Monitor batch executions</small></p>

## Runtime view - Monitor datasource pool statistics

There is a new view to monitor datasource pool statistics.

![Monitor datasource pool statistics]({{ site.baseurl }}/images/20170925-monitor_ds_pool_stats.png "Monitor datasource pool statistics")
<p><small>Monitor datasource pool statistics</small></p>

## Browse deployment contents

It is possible to browse the content of deployments, this is useful when an user wants to navigate the contents of deployments and download its contents.

![Browse deployments]({{ site.baseurl }}/images/20170925-browse_1.png "Browse deployments")
<p><small>Browse deployments option</small></p>

It shows the full path of each content item and its size.

![Browse deployments]({{ site.baseurl }}/images/20170925-browse_2.png "Browse deployments")
<p><small>Browse deployments</small></p>




