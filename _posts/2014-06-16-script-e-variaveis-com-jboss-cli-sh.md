---
id: 408
title: Script e variáveis com jboss-cli.sh
date: 2014-06-16T16:25:47+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=408
permalink: /2014/06/script-e-variaveis-com-jboss-cli-sh/
categories:
  - Dicas
---
O jboss-cli.sh é uma ferramenta por linha de comando que permite criar scripts para automatizar diversas tarefas com o JBoss ou Wildfly.

Em algumas situações é necessário criar variáveis ou alterar valores, para informar no comando jboss-cli.sh.

Veja como usar variáveis com o jboss-cli.sh

<pre>DSNAME=ExampleDS

cmd=`cat &lt;&lt;EOF 
/host=master/server=server-one/subsystem=datasources/data-source=$DSNAME:test-connection-in-pool,
version
EOF`

echo "cmd="$cmd

/opt/jboss-eap-6.3/bin/jboss-cli.sh -c --commands="$cmd"

</pre>

No exemplo acima, é criado a variável DSNAME, que pode ser passada como argumento na invocação do script.

Também veja que cada linha termina em virgula, pois é o separador de comandos, quando usa-se o &#8211;commands (plural).