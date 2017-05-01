---
id: 87
title: 'Nova funcionalidade: main class do jar e coringa no classpath'
date: 2005-09-25T19:35:16+00:00
author: Claudio Miranda
layout: post
permalink: /2005/09/Nova-funcionalidade-main-class-do-jar-e-coringa-no-classpath/
categories:
  - Java
---
Projeto mustang a todo vapor,
  
toda sexta saindo uma vers&atilde;o, com
  
corre&ccedil;&otilde;es e novas funcionalidades, <a target="_blank" href="https://mustang.dev.java.net/files/documents/2817/21109/mustang-b53.html">o<br /> &uacute;ltimo, b53</a>, tem duas funcionalidades bem legais:

  1. <il><a target="_blank" href="http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=4291383">Especificar qual a&nbsp;classe inicializada (<span style="font-family: monospace;">main-class</span>) do manifest</a>, ao&nbsp;invocar o <span style="font-family: monospace;">java -jar arquivo.jar</span>, a funcionalidade foi adicionada no comando <span style="font-family: monospace;">jar</span>, vejam (em negrito): 
    </il><span style="font-family: monospace;">[claudio@saturno tmp]$ /usr/local/j2se/sun/jdk1.6.0/bin/jar</span>
    
    <span style="font-family: monospace;">Usage: jar {ctxu}[vfm0Mi</span><b style="font-family: monospace;">e</b><span style="font-family: monospace;">] [jar-file] [manifest-file] </span><b style="font-family: monospace;">[entry-point]</b> <span style="font-family: monospace;">[-C dir] files &#8230;<br /> <br /> Options:<br /> </span>
        
    <span style="font-family: monospace;">&nbsp;</span><b style="font-family: monospace;">-e specify application entry point for stand-alone application<br /> bundled into an executable jar file</p> 
    
    <p>
      Exemplo:
    </p>
    
    <p>
      </b><span style="font-family: monospace;">[claudio@saturno tmp]$ /usr/local/j2se/sun/jdk1.6.0/bin/jar -cvfe main.jar br.com.claudius.mustang.Main -C . br<br /> added manifest<br /> adding: br/(in = 0) (out= 0)(stored 0%)<br /> adding: br/com/(in = 0) (out= 0)(stored 0%)<br /> adding: br/com/claudius/(in = 0) (out= 0)(stored 0%)<br /> adding: br/com/claudius/mustang/(in = 0) (out= 0)(stored 0%)<br /> adding: br/com/claudius/mustang/Main.class(in = 431) (out= 297)(deflated 31%)</span><b style="font-family: monospace;"></p> 
      
      <p>
        </b>O conte&uacute;do do manifest.mf
      </p>
      
      <div style="margin-left: 40px;">
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
        
        <br /> 
        
        <meta name="Generator" content="Kate, the KDE Advanced Text Editor" />
        </p> 
        
        <pre>Main-Class: br.com.claudius.mustang.Main</pre>
      </div>
      
      <p>
        <il></il></li> 
        
        <li>
          <span style="font-family: monospace;"></span><a target="_blank" href="http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=6268383">Especificar o classpath atrav&eacute;s de coringas</a>, exemplo: <p>
            <span style="font-family: monospace;">[claudio@saturno tmp]$ java -jar *.jar &nbsp; &nbsp; &nbsp; ou<br /> </span><span style="font-family: monospace;">[claudio@saturno tmp]$ java -classpath *.jar</span> br.com.claudius.mustang.Main
          </p>
          
          <p>
            A exce&ccedil;&atilde;o &eacute; que o classpath<br /> configurado no manifest (atrav&eacute;s de Class-Path)<br /> n&atilde;o reconhece, e toma preced&ecirc;ncia. Isso deve ser<br /> corrigido ainda, pois a API foi lan&ccedil;ada h&aacute; pouco<br /> tempo.</li> </ol> </ul> 
            
            <p>
              Em outro post, vou catalogar as novas funcionalidades e corre&ccedil;&otilde;es do Mustang.
            </p>
            
            <div style="margin-left: 40px;">
              <pre></pre>
            </div>
            
            <ul>
            </ul>