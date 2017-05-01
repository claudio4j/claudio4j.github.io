---
id: 227
title: Stop do DB2 sem stop
date: 2009-07-29T11:33:01+00:00
author: Claudio Miranda
layout: post
permalink: /2009/07/Stop-do-DB2-sem-stop/
categories:
  - Linux
---
Script init.d do DB2 Express-C 9.5 para linux. 

Não entendo para que colocam um argumento stop, se o script não faz nada ao invocar o stop. 

Podiam colocar um echo &#8220;stop command not supported&#8221;. 

DB2 0wn3d !!!
  
  


<pre>case "$1" in

  start)
        log_action_begin_msg "Starting $DESC"
        /opt/ibm/db2exc/V9.5/instance/db2istrt
        if running ; then
                log_action_end_msg 0
        else
                log_action_end_msg 1
        fi
        ;;

  stop)
        ;;

  status)
    echo -n "$DESC is "
    if running ;  then
        echo "running"
    else
        echo " not running."
        exit 1
    fi
    ;;

  *)
</pre>