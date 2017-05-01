---
id: 162
title: Quantidade de threads por processo
date: 2007-06-05T20:25:57+00:00
author: Claudio Miranda
layout: post
permalink: /2007/06/Quantidade-de-threads-por-processo/
categories:
  - Dicas
---
Regularmente preciso verificar a quantidade de threads em um processo. Tanto em solaris como em linux. Coloco primeiro a versão para linux e depois a versão para Solaris. 

#### Linux
    

  


Então coloco aqui o comando <font face="monospace">ps</font> completo e logo abaixo um script para facilitar o monitoramento.
  
  


O comando ps 

<pre>ps -p PID -o pid,user,%cpu,rss,etime,nlwp,args
</pre>

Exemplo de invocação 

<more/>

<pre>$ ps -p 5124  -o pid,user,%cpu,rss,etime,nlwp,args
  PID USER     %CPU   RSS     ELAPSED NLWP COMMAND
 5124 claudio   8.0 122160      39:37   11 /usr/local/firefox/firefox-bin
</pre>

A quantidade de threads é mostrada na coluna NLWP, que neste exemplo mostra 11 threads. 

A opção -o informa quais colunas devem ser mostradas. Veja o [manual do comando ps](http://man-wiki.net/index.php/1:ps) para verificar outras opções. 

Note que o comando ps tem apenas uma invocação, o que torna difícil o monitoramento. Então criei um script bash, que tem as seguintes vantagens: 

  * Aceita uma quantidade de repetições.
    
    
  * Repete o cabeçalho em 15 linhas
  * Aceita uma string como argumento, ao invés do nome do processo. Para não ter de ficar procurando o PID a todo momento.
    
    

[<font face="monospace">threads_per_process.sh</font>](/resources/claudio/threads_per_process.sh.txt) 

#### Solaris
  


No solaris o comando é mais fácil: <font face="monospace">prstat</font> 

Ele aceita um parametro de repetição, que é útil para monitoramento. 

Comando 

<pre>prstat -c -p PID 1 3
</pre>

Exemplo de invocação 

<pre>$ prstat -c -p 15409 1 3
   PID USERNAME  SIZE   RSS STATE  PRI NICE      TIME  CPU PROCESS/NLWP
 15409 claudio   171M  120M sleep   59    0   4:22:25 6.6% java/29
Total: 1 processes, 29 lwps, load averages: 0.25, 0.27, 0.29
   PID USERNAME  SIZE   RSS STATE  PRI NICE      TIME  CPU PROCESS/NLWP
 15409 claudio   171M  120M sleep   59    0   4:22:25 6.3% java/29
Total: 1 processes, 29 lwps, load averages: 0.26, 0.27, 0.29
</pre>

A quantidade de threads é mostrada na última coluna, chamada de NLWP, ao lado do nome do binário, que neste exemplo, mostra 29 threads. 

Este monitoramento permitiu que pudesse avaliar um [teste de threads](http://www.claudius.com.br/blog/claudio/2007/05/15/Qual-%C3%A9-a-quantidade-m%C3%A1xima-de-threads-suportada-por-um-sistema) que precisei realizar um tempo atrás.&nbsp; 

Se isto é útil para você, deixe um comentário sobre como isso lhe ajudou.