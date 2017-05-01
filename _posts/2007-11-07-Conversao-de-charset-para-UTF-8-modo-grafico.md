---
id: 191
title: Conversão de charset para UTF-8, modo gráfico
date: 2007-11-07T17:26:44+00:00
author: Claudio Miranda
layout: post
permalink: /2007/11/Conversao-de-charset-para-UTF-8-modo-grafico/
categories:
  - Dicas
---
<img align="right" src="/resources/claudio/tips_icon.gif" alt="Dicas" hspace="80" />

Segue uma maneira fácil de converter arquivos ou nome de arquivos para UTF-8. Um exemplo é quando copia-se arquivos acentuados em windows para linux, o nome de arquivo não é convertido, ficando um nome ilegível. Então deve-se converter o nome do arquivo para UTF-8. 

Na <a alt="Conversão de charset para UTF-8" href="http://www.claudius.com.br/blog/claudio/2007/11/05/Convers%C3%A3o-de-charset-para-UTF-8">dica anterior</a>, foi mostrado como modificar o conteúdo do arquivo para UTF-8. O uso da ferramenta konwert por linha de comando é útil quando se tem muitos arquivos a serem verificados. Quando se tem poucos arquivos e estão visíveis na interface gráfica, torna-se mais prático usar alguns cliques para resolver isso. 

Então a dica fica com o uso de um script específico para o Konqueror (KDE) que abre um menu de contexto com opções de conversão. O script é o [ToUTF-8](http://www.kde-apps.org/content/show.php/ToUTF-8?content=31400), encontrado no [kde-apps.org](http://www.kde-apps.org), as instruções de instalação estão no site. 

### Requisitos
  


  * Linux
  * KDE
  * Konqueror
    
    
  * recode
    
    

Eu uso o gerenciador de arquivos [krusader](http://krusader.sf.net/), que acho bem mais prático do que o konqueror.
  
  


Clique na imagem abaixo, para ver como ele funciona.&nbsp; 

[<img border="0" src="/resources/claudio/krusader_utf8_sm.jpg" alt="Clique na imagem para ampliar" />](/resources/claudio/krusader_utf8.png)