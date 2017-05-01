---
id: 197
title: 'Resolvendo memory leak &#8211; Identificando o comedor de memória'
date: 2008-02-20T00:45:46+00:00
author: Claudio Miranda
layout: post
permalink: /2008/02/Resolvendo-memory-leak-Identificando-o-comedor-de-memoria/
categories:
  - Java
---
**<font size="6">Resolvendo memory leak &#8211; Procurando o devorador de memória &#8211; parte 1</font>**

  
Algo que vejo recorrente em fóruns e listas de discussão, colegas que perguntam para mim, é &#8220;**como detectar e resolver o memory leak ?**&#8221;
  
  


Começarei uma série de dicas voltados a encontrar e resolver o problema de retenção de memória (memory leak) em aplicações Java. Posteriomente, será feito um tutorial para resolver problemas de CPU. 

Estas dicas podem ser úteis para programadores que ainda não passaram por este problema ou não conhecem as ferramentas. Mesmo para profissionais experientes, espero que possa contribuir.
  
  


Isso é baseado em minha experiência, em ambiente linux e solaris. Será dado ênfase no uso de ferramentas gratuitas ou de código livre, para ajudar neste processo. Para ambiente windows, onde possível colocarei as dicas aplicáveis para este SO, mas devo dizer que não tenho especialidade neste SO, portanto desconheço as ferramentas mais adequadas. 

<font size="5"><strong>Ambiente de produção e desenvolvimento</strong> </font>
  
  


Também será mostrado como resolver esse problema, tanto em ambiente de produção como em ambiente de desenvolvimento, com as ferramentas disponíveis em cada amviente (exemplo: invocar profiler ou debug em ambiente de produção é bastante caro em termos de performance). 

É importante endender que a aplicação pode sofrer monitoramento de maneira intrusiva e não intrusiva. 

  * Intrusivo: quando é necessário modificar as configurações de inicialização da aplicação para permitir uma introspecção de suas chamadas de sistemas e quando ocorre uma interceptação destas chamadas de sistemas pelo esquema de monitoramento intrusivo. Um exemplo disso são os profilers e debuggers. Isso gera penalidade em performance, modificação da configuração do ambiente e instalação de ferramentas, o que em ambiente de produção pode ser um grande problema
    
    
  * Não intrusivo: Quando é usado ferramentas de monitoramento, que não geram interceptação das chamadas do sistema, não geram impacto negativo em desempenho e não precisam de instalação de software adicional.
    
    

Existem uma série de passos, começando por descobrir onde ocorre problema de retenção, até sua resoluçao. 

<font size="6">Qual processo do sistema operacional consome memória em demasiado ?</font> 

  
Este é o 1o passo, para identificar se o programa (desktop ou servidor) consome memória sem manter estável.
  
  


<p class="post">
  É importante entender que a aplicação deve ter passado por todas as etapas de criação de objetos e recursos, que já tenha passado por um ciclo de vida. Isso pode ser alcançado, navegando pela aplicação, consultando relatórios, etc.<br />
</p>

É necessário usar apenas o SO e suas ferramentas, para descobir qual o processo está neste estado.
  
  


Ferramentas: 

  * Linux: top, htop, ps
    
    
  * Solaris: prstat, ps
    
    
  * Windows: gerenciador de tarefas
    
    

Segue um exemplo de um programa que consome memória (propositadamente), e sua medição pelos respectivos utilitários do SO. 

Vejam que existe um processo java que consome muita memória. O que neste caso interessa saber o PID (process ID) e a linha de comando. 

**<font size="5">Linux top</font>** 


![](/resources/claudio/080219_top.png) 

Percebe-se uma visualização com cores, linha de comando completa e ordenação diferentes, isso pode ser alcançado por atalhos 

z => modifica o esquema de cores 

c => mostra a linha de comando completa 

shit M => ordena pelo consumo de memória 

W => Torna esta configuração o padrão nas próximas invocações do comando top
  
  
</p> 

O top tem uma vantagem, que ele já vem instalado em qualquer linux, então não é necessário efetuar download e instalá-lo. Já o htop, fornece uma visualização melhorada, mas é necessário efetuar download e instalar. 

Para saber o consumo da memória por processo, veja na coluna RSS (ou RES), este é o valor de memória física consumido pelo processo (de fato, existem algumas discussões em fórums sobre o comando RSS ser bem uma aproximação do valor real, mas fico devendo uma explicação melhorada sobre isso em outro blog) 

**<font size="5">Linux htop</font>** 


![](/resources/claudio/080219_htop.png) 

Este utilitário, fornece uma visualização melhorada sobre os processos e os recursos.
  
  


**<font size="5">Linux ps</font>**<!--<-->

### 

<pre>$ ps -eo pid,user,%cpu,rss,vsz,etime,nlwp,args
  PID USER     %CPU   RSS    VSZ     ELAPSED NLWP COMMAND
 7642 claudio   0.7 343536 658804      05:23   12 java TestReferences
</pre>

A diferença do comando ps e top, é apenas a visualização, já que o ps recupera um snapshot do sistema. 

O diferencial deste comando, é que mostra também a quantidade de threads por processo, na coluna NLWP.
  
  


**<font size="5">Solaris prstat</font>** 

<pre>$ prstat -s rss
   PID USERNAME  SIZE   RSS STATE  PRI NICE      TIME  CPU PROCESS/NLWP
   617 claudio   102M   78M sleep   59    0   0:00:01 2.1% java/9
   554 root      106M   32M sleep   59    0   0:00:01 0.2% ns-httpd/71
     7 root       11M   10M sleep   59    0   0:00:03 0.0% svc.startd/12
     9 root       11M 9384K sleep   59    0   0:00:07 0.0% svc.configd/17
   308 root       12M 8528K sleep   59    0   0:00:01 0.0% fmd/16
   553 root       27M 8088K sleep   59    0   0:00:00 0.0% ns-httpd/2
   618 root     8936K 4416K sleep   59    0   0:00:00 0.0% sshd/1
</pre>

Foi usada a opção prstat -s rss para ordenar a apresentação baseada no consumo de memória. Outra informação é a quantidade de threads por processo, na coluna NLWP
  
  


**<font size="5">Windows task manager</font>** 


![](http://www.netbeans.org/images/articles/win-with-netbeans/wtm.png) 

   
Então foi identificado qual é o sistema que consome mais memória. Com isso é possível ter um ponto de partida na análise do processo. 

No próximo blog, que pretendo escrever em dois dias (espero), será mostrado como detectar se existe memory leak.