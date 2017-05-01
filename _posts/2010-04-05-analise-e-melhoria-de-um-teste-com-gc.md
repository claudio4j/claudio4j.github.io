---
id: 242
title: Análise e melhoria de um teste com GC
date: 2010-04-05T11:23:35+00:00
author: Claudio Miranda
layout: post
permalink: /2010/04/analise-e-melhoria-de-um-teste-com-gc/
categories:
  - Java
---
Motivado pela <a href="http://code.google.com/p/claudius-alphaworks/source/browse/trunk/#trunk/java_dev/thread-capacity" target="_blank">liberação do teste de threads</a>, quiz fazer um pequeno teste, que ajude a analisar o funcionamento do Garbage Collector e como algumas alterações podem melhorar o desempenho.

Quando se fala em teste, existe muita discussão sobre a validade dos resultados.

Então já digo que este é um teste caseiro, para ter sua opinião, faça o teste em seu ambiente.

## 1) Teste

O teste de threads ([NumThreads.java](http://code.google.com/p/claudius-alphaworks/source/browse/trunk/java_dev/thread-capacity/src/java/br/com/claudius/threads/NumThreads.java), projeto completo), lança todas
  
as
  
threads enumeradas no parametro, em que cada thread faz uma série de
  
processamento matemático, cada thread pode repetir o processamento em
  
uma quantidade determinada.

o fluxo de criaçao, coloca em um array, depois faz o start de cada
  
thread, depois faz um join para esperar o processamento de todas as
  
threads.

O start de cada thread não começa imediatamente, existe um barreira
  
(CyclicBarrier) que aguarda o contador de todas as threads que foram
  
iniciadas para que todas possam de fato entrar em operação juntas.

Em uma configuração default da JVM não consegui inicar com mais de 2700
  
threads, 2000 operações matemáticas por thread, ocorriam erros da JVM
  
(OOME, ThreadDeath,
  
Stackoverflow, etc.)

A minha máquina é um laptop toshiba, Core2 Duo T2400 1.83 GHz com 3 GB
  
de RAM.

## 2) Monitoramento

O monitoramento foi feito usando o vmstat, jvisualvm, jmap
  
No caso do <a
  
href=&#8221;http://code.google.com/p/claudius-alphaworks/source/browse/trunk/shell\_bin/vmstat\_date.sh&#8221;>vmstat,
  
coloquei a data como prefixo.

## 3) Resultado (1a bateria)

O teste foi iniciado com os seguintes parametros, que geralmente é o
  
comum, onde configura-se apenas o tamanho máximo do heap.
  
Depoi veremos o que se pode melhorar neste teste.

<pre>$ time java -Xmx2g -classpath build/WEB-INF/classes/:src/conf/:src/java/ br.com.claudius.threads.NumThreads 2700 5000 60</pre>

O tempo total, deve ser descontado 60s que usei como pausa antes das
  
threads começarem de fato (3o parametro)

<pre>real 3m11.948s
user 2m14.612s
sys 1m40.354s</pre>

O tempo total foi de 2min11s ou 131s
  
O que chama a atenção na configuração default é o tamanho do Stack de
  
320 kb, bem grande.

<pre>$ jinfo -flag ThreadStackSize 18610
-XX:ThreadStackSize=320</pre>

A configuração do heap (apenas a parte importante)

<pre>$ jmap -heap 18610
Server compiler detected.
JVM version is 16.0-b13

using thread-local object allocation.
Parallel GC with 2 thread(s)

Heap Configuration:
 MinHeapFreeRatio = 40
 MaxHeapFreeRatio = 70
 MaxHeapSize = 2147483648 (2048.0MB)
 NewSize = 4194304 (4.0MB)
 MaxNewSize = 4294901760 (4095.9375MB)
 OldSize = 4194304 (4.0MB)
 NewRatio = 2
 SurvivorRatio = 8
 PermSize = 16777216 (16.0MB)
 MaxPermSize = 67108864 (64.0MB)</pre>

Um pedaço do vmstat durante a execução

<pre>2010-04-02 20:47:16 procs -----------memory---------- ---swap-- -----io---- -system-- ----cpu----
2010-04-02 20:47:16 r b swpd free buff cache si so bi bo in cs us sy id wa
...
2010-04-02 20:48:44 51 0 0 283440 81520 1825480 0 0 0 0 1131 934 61 36 3 0
2010-04-02 20:48:48 50 0 0 286032 81528 1811856 0 0 0 11 1230 1291 64 30 5 0
2010-04-02 20:48:52 109 0 0 259780 81528 1811324 0 0 0 5 1133 1579 58 36 5 0</pre>

Percebe-se que a &#8220;<tt>run queue</tt>&#8221; (coluna r) possui um alto número
  
de
  
tarefas aguardando um tempinho da CPU para processar alguma instrução.

Vejam um screenshot do visualgc ao fim do teste

<info>

O VisualGC é um plugin do VisualVM. Na versão atual do Java, o visualvm
  
faz parte do download do java, mas é chamado de jvisualvm.

Durante o teste ocorreram 115 ações do GC na área YOUNG que duraram
  
3.306 ms, enquanto a área OLD com seus 1,3 GB ociosos.

![VisualGC 1](/resources/claudio/20100405_visualgc1.png)

## 4) Análise

O objetivo do teste é a JVM e não a aplicação, então nem vamos olhar na
  
aplicação.

Sempre em uma análise do GC, é importante diminuir o impacto do tempo
  
do GC na aplicação. Sempre que puder diminuir o tempo total do GC ajuda
  
o throughput da aplicação.

Em uma análise óbvia, percebe-se que a área OLD está ociosa, enquanto
  
existe atividade intensa na área YOUNG, então seria natural aumentar a
  
área YOUNG para um tamanho grande. Aqui que costuma ocorrer um erro
  
comum também, onde aumentar uma área é proporcional ao tempo de GC,
  
pelo tamanho maior a ser varrido.

Por esta applicação ser orientada a CPU (muitas threads),
  
processamento matemático, sem sincronização, sem rede, sem banco de
  
dados, então é uma análise orientada para menor consumo de CPU e
  
otimização do funcionamento do Garbage Collector.

&nbsp;

## 5) Resultado (2a bateria)

Será feito uma otimização na invocação do comando java

<pre>$ time java -server -XX:+AlwaysTenure -XX:+UseConcMarkSweepGC -Xss64k -Xms2g -Xmx2g -classpath build/WEB-INF/classes/:src/conf/:src/java/ br.com.claudius.threads.NumThreads 2700 2000 10</pre>

Parametros adicionais:

<table border="1" width="80%" cellspacing="2" cellpadding="2">
  <tr>
    <td valign="top" bgcolor="silver">
      <b>Parametro<br /> </b>
    </td>
    
    <td valign="top" bgcolor="silver">
      <b>Explicação<br /> </b>
    </td>
  </tr>
  
  <tr>
    <td valign="top">
      <tt>-server</tt>
    </td>
    
    <td valign="top">
      Usa otimizações específicas para o modo de<br /> aplicações<br /> servidoras.
    </td>
  </tr>
  
  <tr>
    <td valign="top">
      <tt>-XX:+AlwaysTenure</tt>
    </td>
    
    <td valign="top">
      Não usa espaços Survivors da área YOUNG, a<br /> promoção<br /> vai direto da YOUNG para OLD.
    </td>
  </tr>
  
  <tr>
    <td valign="top">
      <tt>-XX:+UseConcMarkSweepGC</tt>
    </td>
    
    <td valign="top">
      Usa o algoritmo concorrente na área OLD e<br /> Paralelo na área YOUNG (<tt>-XX:+UseParNewGC</tt>)
    </td>
  </tr>
  
  <tr>
    <td valign="top">
      <tt>-Xss64k</tt>
    </td>
    
    <td valign="top">
      Reserva 64 kb para o tamanho do stack de thread.
    </td>
  </tr>
  
  <tr>
    <td valign="top">
      <tt>-Xms2g</tt>
    </td>
    
    <td valign="top">
      Aloca inicialmente o tamanho do heap para 2 GB
    </td>
  </tr>
</table>

<pre>real 1m5.618s
user 0m51.967s
sys 0m38.598s</pre>

Percebe-se a melhoria no tempo de 66s.

Descontar 10s deste tempo final, pois na aplicação tem uma pausa de 10s
  
antes de começar o teste.

O visualgc mostra uma melhoria significativa, onde ocorreram 86 ações
  
do GC com duração da atividade de  GC em 836 ms.

![VisualGC 2](/resources/claudio/20100405_visualgc2.png)

Ao efetuar a mesma medição com o jstat, percebe-se uma melhoria
  
marginal no tempo total do GC, mas com boa diminuição na quantidade de
  
GC.

<pre>$ jstat -gcutil 1451 3s
 S0 S1 E O P YGC YGCT FGC FGCT GCT
 0,00 0,00 54,22 0,08 11,30 71 0,799 0 0,000 0,799
 0,00 0,00 81,01 0,08 11,30 75 0,808 0 0,000 0,808</pre>

Ao diminuir o tamanho do stack para 48k (o mínimo aceito pela JVM), o
  
tempo do GC melhorou bem.

Com -Xss48k

<pre>$ jstat -gcutil 4265 3s
 S0 S1 E O P YGC YGCT FGC FGCT GCT
 0,00 0,00 44,52 0,08 11,30 75 0,670 0 0,000 0,670
 0,00 0,00 97,33 0,08 11,30 79 0,685 0 0,000 0,685</pre>

O comportamente da CPU mostrado pelo vmstat, mostra um uso bem mais
  
modesto da CPU, veja a coluna r (run queue)

<pre>2010-04-05 00:40:14 procs -----------memory---------- ---swap-- -----io---- -system-- ----cpu----
2010-04-05 00:40:14 r b swpd free buff cache si so bi bo in cs us sy id wa
...
2010-04-05 00:40:53 24 0 0 1386056 249416 953668 0 0 0 0 1190 631 52 32 16 0
2010-04-05 00:40:56 7 0 0 1390532 249424 953660 0 0 0 4 1199 645 59 32 10 0
2010-04-05 00:40:59 18 0 0 1395652 249424 953500 0 0 0 0 1196 609 54 34 12 0</pre>

Nota 2: o VisualGC é um plugin do VisualVM (Tools -> Plugins ->
  
Available Plugins)

## 5) Conclusão

No 2o teste foi percebido uma melhoria significativa no tempo total
  
e com menos impacto na utilização da CPU.

Não foi feito um super mega tunning para este exemplo, mas mostrar que
  
com uma boa análise, alguns testes, é possível observar o comportamento
  
da aplicação e aplicar as otimizações no lugar certo.

Tente executar um teste e análise em seu ambiente.

## 6) FAQ ?

### 6.1) Você usou o G1 ?

Usei o algorítimo G1 mas o resultado foi inferior ao concorrente, mas o
  
pior neste caso foi que a ferramenta jstat não consegue exibir os
  
resultados das áreas de memória.

<pre>Warning: Unresolved Symbol: sun.gc.generation.0.space.1.capacity substituted NaN
Warning: Unresolved Symbol: sun.gc.generation.0.space.1.used substituted NaN
...
Warning: Unresolved Symbol: sun.gc.collector.0.time substituted NaN
Warning: Unresolved Symbol: sun.gc.collector.1.time substituted NaN
 S0 S1 E O P YGC YGCT FGC FGCT GCT
 � � � � 30,33 � � � � �</pre>

&nbsp;

### 6.2) Porque aumentar o stack size da aplicação de teste para monitorar ?

Parece que as ferramentas gráficas jconsole e visualvm exigem um stack
  
de tamanho maior para monitorar, caso contrário ocorre um erro

<pre>*** java.lang.instrument ASSERTION FAILED ***: "!errorOutstanding" with message transform method call failed at ../../../src/share/instrument/JPLISAgent.c line: 806
Segmentation fault</pre>

isso é assunto para outro blog

### 6.3) Porque não aumentar o tamanho da área YOUNG (-XX:+NewSize)

Ao aumentar o tamanho da área YOUNG diminuiu a quantidade de GC, mas o
  
tempo total do GC aumentou e isso trouxe uma performance inferior ao
  
teste final. Nem sempre aumentar o tamanho da YOUNG beneficia a
  
aplicação. Cada caso tem de ser analisado diferente.