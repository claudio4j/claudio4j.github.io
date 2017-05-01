---
id: 410
title: Scripts and variables with jboss-cli.sh
date: 2014-06-16T16:30:08+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=410
permalink: /2014/06/scripts-and-variables-with-jboss-cli-sh/
categories:
  - Dicas
---
<div class="entry-content">
  <p>
    jboss-cli.sh is a command line tool that allows the administrator to perform many tasks at once with JBoss or Wildfly.
  </p>
  
  <p>
    Sometimes, users wants to use variables to input values, see how to use variables with jboss-cli.sh
  </p>
  
  <pre>DSNAME=ExampleDS

cmd=`cat &lt;&lt;EOF 
/host=master/server=server-one/subsystem=datasources/data-source=$DSNAME:test-connection-in-pool,
version
EOF`

echo "cmd="$cmd

/opt/jboss-eap-6.3/bin/jboss-cli.sh -c --commands="$cmd"

</pre>
  
  <p>
    The above sample, adds a variable named DSNAME.
  </p>
  
  <p>
    See, each line ends with a comma, it is the command separator, when &#8211;commands is used.
  </p>
</div>

<div class="entry-content">
</div>