---
id: 220
title: Geração de heap dump no linux 64 bits
date: 2008-10-02T01:28:59+00:00
author: Claudio Miranda
layout: post
permalink: /2008/10/Geracao-de-heap-dump-no-linux-64-bits/
categories:
  - Java
---
Estou em um trabalho para um cliente envolvendo melhorias de performance na aplicação e no ambiente operacional (appserver, sistema operacional, jvm).

O ambiente é Linux 64 bits (RedHat, kernel 2.6.18 SMP), JDK 5 e Glassfish v2 ur2.

Em um dado momento, precisei gerar um heap dump, mas ocorreu um erro&nbsp; <font face="monospace">sun.jvm.hotspot.debugger.UnmappedAddressException</font>. 

<pre># /usr/local/jdk/jdk1.6.0_07/bin/jmap -J-d64 -F -dump:file=java_dump_10791.hprof  10791
Attaching to process ID 10791, please wait...
Debugger attached successfully.
Server compiler detected.
JVM version is 10.0-b23
Dumping heap to java_dump_10791.hprof ...
Exception in thread "main" java.lang.reflect.InvocationTargetException
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:39)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:25)
        at java.lang.reflect.Method.invoke(Method.java:597)
        at sun.tools.jmap.JMap.runTool(JMap.java:178)
        at sun.tools.jmap.JMap.main(JMap.java:110)
Caused by: sun.jvm.hotspot.debugger.UnmappedAddressException
        at sun.jvm.hotspot.debugger.PageCache.checkPage(PageCache.java:208)
        at sun.jvm.hotspot.debugger.PageCache.getData(PageCache.java:63)
        at sun.jvm.hotspot.debugger.DebuggerBase.readBytes(DebuggerBase.java:205)
        at sun.jvm.hotspot.debugger.linux.LinuxDebuggerLocal.readCInteger(LinuxDebuggerLocal.java:471)
        at sun.jvm.hotspot.debugger.DebuggerBase.readAddressValue(DebuggerBase.java:442)
        at sun.jvm.hotspot.debugger.linux.LinuxDebuggerLocal.readOopHandle(LinuxDebuggerLocal.java:431)
        at sun.jvm.hotspot.debugger.linux.LinuxAddress.getOopHandleAt(LinuxAddress.java:115)
        at sun.jvm.hotspot.oops.Oop.getKlassForOopHandle(Oop.java:222)
        at sun.jvm.hotspot.oops.ObjectHeap.newOop(ObjectHeap.java:348)
        at sun.jvm.hotspot.utilities.HashtableEntry.literal(HashtableEntry.java:53)
        at sun.jvm.hotspot.memory.SymbolTable.symbolsDo(SymbolTable.java:106)
        at sun.jvm.hotspot.utilities.HeapHprofBinWriter.writeSymbols(HeapHprofBinWriter.java:830)
        at sun.jvm.hotspot.utilities.HeapHprofBinWriter.write(HeapHprofBinWriter.java:396)
        at sun.jvm.hotspot.tools.HeapDumper.run(HeapDumper.java:56)
        at sun.jvm.hotspot.tools.Tool.start(Tool.java:221)
        at sun.jvm.hotspot.tools.HeapDumper.main(HeapDumper.java:77)

</pre>

Tentei gerar o dump através de:

  * -XX:+HeapDumpOnCtrlBreak and kill -3
  * jmap -heap:format=b
  * gcore utility

Com isso decidi usar o JDK 6 u7 ([changelog](http://dlc-cdn-rd.sun.com/c1/jdk6/6u10/promoted/b32/changes/JDK6u10.list.html?e=1222914889&h=690498eeec8731f49945b4c6b8ddcbd7)), mas ocorreu o mesmo problema.

**UPDATE**: A stacktrace mostrada acima, mostra a invocação de um comando jmap do JDK 6 u7, para uma VM 6 u7.   
**UPDATE**: Anteriormente, quando estava com JDK 5 u12, tentei rodar o jmap a partir de uma VM 5 u12, mas o mesmo erro ocorreu   
**UPDATE**: A VM não está com a opção <font face="courier new,courier,monospace">-Xrs</font> option.   
**UPDATE**: O usuário que iniciou o processo é o mesmo que usei para invocar o comando jmap, root.

**UPDATE**: [Alan Bateman](http://blogs.sun.com/alanb/), explicou sobre o uso da opção -F "_**A opção -F faz como que a ferramenta se conecte no processo de uma maneira não colaborativa e pode causa a geração de um dump inconsistente. Em outras palavras, não há garantia de que será um bom heap dump ao usar a opção -F**_", veja este comentário em inglês na seção de comentários abaixo. 

Então encontrei um bug corrigido ["<font>Throws UnmappedAddressException while reading address from core file in shared area.</font>"](http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=6480383), entao decidi usar o [JDK 6 u10 RC](http://java.sun.com/javase/downloads/ea.jsp).

Coloquei a opção <font face="monospace">-Xshare:off</font>

E funcionou muito bem,o processo não foi derrubado e a aplicação funcionou normalmente.

Não esqueça que no momento do heap a JVM paralisa todas as threads e o arquivo gerado será tão grande (ou um pouco menor) como a memória RSS usada pelo processo.

Então, se for gerar heap dump em linux 64 bits, use o JDK 6 u10 RC com a opção <font face="monospace">-Xshare:off.</font>

<font face="monospace"></font>Ao final da geração do heap dump, as mensagens abaixo foram impressas

"<font face="monospace">Finding object size using Printezis bits and skipping over&#8230;</font>"

Obrigado [Tony](http://blogs.sun.com/tony/), pelo seu trabalho no HotSpot.