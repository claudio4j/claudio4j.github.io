---
id: 335
title: Eclipse 3.7 com JBoss EAP 6.1
date: 2013-06-20T19:50:13+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=335
permalink: /2013/06/eclipse-3-7-com-jboss-eap-6-1/
categories:
  - Dicas
---
Após o lançamento do JBoss EAP 6.1, fui integrar no jboss tools, do eclipse 3.7 (indigo), e vejo que não consegue-se, pois o plugin do jboss tools não foi preparado para o EAP 6.1. Isso ocorre pois no EAP 6.0 os módulos do EAP 6.1 ficam no subdiretório de modules, assim $JBOSS_HOME/modules/org/jboss/as/

Já no EAP 6.1 este diretório foi reorganizado, onde os módulos ficam em $JBOSS_HOME/modules/system/layers/base/org/jboss/as/&#8230;

Esta nova estrutura de diretórios que não é esperada pelo plugin jboss tools 3.3 do eclipse. A nova versão do jboss tools 4.0.1 já suporta o eap 6.1, mas o plugin é somente para o eclipse 4, juno.

Tentei usar o eclipse 4, mas achei bem mais lento do que o 3.7, alguns ícones da janela de console ficam desaparecendo, não gostei. Tentei usar, mas muito lento.

Então, peguei o fonte do jboss tools 3.3 e alterei para que consiga funcionar com o EAP 6.1.

Abaixo, a tela mostra que o diretório de módulos consegue ser procurado.

[<img class="alignnone size-medium wp-image-336" alt="jbt1" src="/wp-content/uploads/2013/06/jbt1-280x300.png" width="280" height="300" srcset="http://claudius.com.br/wp-content/uploads/2013/06/jbt1-280x300.png 280w, http://claudius.com.br/wp-content/uploads/2013/06/jbt1.png 527w" sizes="(max-width: 280px) 100vw, 280px" />](/wp-content/uploads/2013/06/jbt1.png)
  
[<img class="alignnone size-medium wp-image-337" alt="jbt2" src="/wp-content/uploads/2013/06/jbt2-300x283.png" width="300" height="283" srcset="http://claudius.com.br/wp-content/uploads/2013/06/jbt2-300x283.png 300w, http://claudius.com.br/wp-content/uploads/2013/06/jbt2.png 965w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2013/06/jbt2.png)

Para alterar o código fonte,

  * Feche o eclipse
  * Faça o [download dos fontes do jboss tools 3.3](http://www.jboss.org/tools/download/stable/3_3_Final.html) e descompacte em algum local
  * Faça o download do script [compile](/wp-content/uploads/2013/06/compile), altere o JAVA_HOME e ECLIPSE, bem como descomentar a seção que faz o backup dos arquivos do plugin (onde tem o cp)
  * Coloque o [compile](/wp-content/uploads/2013/06/compile) no diretório as/plugins de onde descompactou o jboss tools
  * Veja as alterações no [diff](/wp-content/uploads/2013/06/changes.txt), aplique-as.
  * Execute o script compile

Nota: Esta alteração faz com que o jboss plugin reconheça apenas o EAP 6.1, da família JBoss. Até é possível melhorar o código para suportar tanto o 6.0 e 6.1, mas não é o meu foco agora.

Para sua conveniência e se confia em mim, pode fazer o [download das classes compilada](/wp-content/uploads/2013/06/classes_as_core.zip)s e atualizar direto no seu plugin do jboss tools. Veja o script compile para saber em qual jar colocar as classes compiladas.