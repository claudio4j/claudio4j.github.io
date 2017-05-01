---
id: 195
title: Ler arquivos do office com Java
date: 2007-11-16T15:36:46+00:00
author: Claudio Miranda
layout: post
permalink: /2007/11/Ler-arquivos-do-office-com-Java/
categories:
  - Java
---
<img src="/resources/claudio/tips_icon.gif" alt="Dicas" align="right" hspace="80" />

No passado existiu uma situação no projeto, em que existiam vários documentos de projeto (guia, arquitetura, requisitos, manual, etc.), vindo de diferentes fontes (diretório de backup, cdrom), e são documentos office (doc, xls, ppt), e vários documentos repetidos, mas de origens diferentes. 

Então como saber qual é o último arquivo e remover os antigos ? 

Uma maneira é abrir cada arquivo e olhar nas propriedades do mesmo, mas fazer isso manualmente com cerca de 300 arquivos, poxa não sou mais estagiário para isso :-D (nada contra os estagiários). 

Então fiz um programa em java, que usa a API SDK do OpenOffice para ler estas propriedades e mostrar as datas da última modificação e o autor. 

Claro que é possível usá-lo para ler qualquer outra propriedade ou expandir para outros usos. 

Atualmente a pesquisa é efetuada nos seguintes arquivos com extensão: <font face="courier new,courier,monospace">sxw doc xls odt ods pps odt odp ppt&nbsp;</font> 

Altere o DocViewer.java para adicionar outras extensões.&nbsp; 

Faça o download do código fonte: [DocViewer.java](/resources/claudio/DocViewer.java.txt)
  
<small>(remova a extensão .txt)</small>

## Requerimentos:&nbsp;
  


### Em tempo de compilação é necessário as seguintes bibliotecas:
  


<pre>$OO_HOME/program/classes/juh.jar
$OO_HOME/program/classes/jurt.jar
$OO_HOME/program/classes/jut.jar
$OO_HOME/program/classes/ridl.jar
$OO_HOME/program/classes/unoil.jar
</pre>

A variável OO_HOME aponta para o diretório de instalação do OpenOffice. No meu caso uso o BrOffice, que está instalado em <font face="courier new,courier,monospace">/opt/broffice.org2.3</font>
  
  


### Em runtime:
  


  * Instalação do OpenOffice
  * X Virtual Frame Buffer (Xvfb)
  * Java (testei com a versão 5)

## Compilação
  


Essa parte é simples, use sua IDE favorita ou o javac 

<pre>javac -classpath /opt/broffice.org2.3/program/classes/\* src/claudius/DocViewer.java
</pre>

Usei o classpath wildcards, válido apenas para o Java 6 

## Uso
  


Para colocar o openoffice em modo servidor, usei um servidor X virtual, isso é para ambiente servidor, onde não é necessário ter um monitor nem interface gráfica. No caso foi instalado o X Virtual Frame Buffer.
  
  


Se não puder instalar um servidor X virtual e iniciar a aplicação openoffice manualmente, tudo bem, basta não informar qual o servidor X a ser usado. Veja o exemplo abaixo: 

### Com servidor X virtual&nbsp;
  


<pre>Xvfb :5 -screen 0 800x600x16 &&nbsp;
</pre>

<pre>/opt/broffice.org2.2/program/soffice -accept="socket,host=127.0.0.1,port=8100;urp;" -display :5 -headless -norestore -invisible &
</pre>

### Sem servidor X virtual
  


<pre>/opt/broffice.org2.2/program/soffice -accept="socket,host=127.0.0.1,port=8100;urp;" -headless -norestore -invisible &
</pre>

### Invocar o programa Java
  


A sintaxe para invocar é 

<pre>java -classpath $CP claudius.DocViewer &lt;path do arquivo ou diretório&gt;
</pre>

O classpath **$CP** é o mesmo usado na compilação, em adição ao diretório da classe DocViewer compilada.
    
  
O **path**, pode ser um arquivo único ou diretório, que neste último caso irá pesquisar nos subdiretórios também.&nbsp; 

Exemplo&nbsp; 

<pre>java -classpath build/classes/:/opt/broffice.org2.3/program/classes/\* claudius/DocViewer arquivo-projeto.odt
</pre>

O resultado: 

<pre>dir&nbsp; = /home/claudio/resources/palestras/2007/10_justjava
file = diagnostico2.odp
Modified by: Claudio Miranda 5/10/2007 17:46:8
</pre>

Se essa dica foi útil para você, deixe uma mensagem comentando como isso lhe ajudou.