---
id: 310
title: Cedilha no fedora 18
date: 2013-05-07T23:48:01+00:00
author: Claudio Miranda
layout: post
guid: https://secure255.hostgator.com/~claudius/?p=310
permalink: /2013/05/cedilha-no-fedora-18/
categories:
  - Dicas
  - Linux
---
Instalei o Fedora 18 e assim como no 17, a cedilha digitada é mostrada como ć nas aplicações GTK (libreoffice, firefox, pidgin, etc.).

Nas aplicações QT e console funciona tudo bem com cedilha ç certo.

Para corrigir precisei instalar alguns pacotes adicionais e configurar arquivos

<pre>$ rpm -qa|grep im|grep mod|sort
gtk2-immodules-2.24.16-1.fc18.x86_64
gtk2-immodule-xim-2.24.16-1.fc18.x86_64
gtk3-immodule-xim-3.6.4-1.fc18.x86_64</pre>

<pre>sudo vim /usr/lib64/gtk-3.0/3.0.0/immodules.cache</pre>

Adicionar o en na lista cedilla

<pre>"cedilla" "Cedilla" "gtk30" "/usr/share/locale" "az:ca:co:fr:gv:oc:pt:sq:tr:wa:en"</pre>

Usar o programa im-chooser para escolher o cedilla como método de entrada.

[<img class="alignnone size-medium wp-image-313" alt="cedilla-im" src="https://secure255.hostgator.com/~claudius/wp-content/uploads/2013/05/cedilla-im-300x167.png" width="300" height="167" srcset="http://claudius.com.br/wp-content/uploads/2013/05/cedilla-im-300x167.png 300w, http://claudius.com.br/wp-content/uploads/2013/05/cedilla-im.png 365w" sizes="(max-width: 300px) 100vw, 300px" />](https://secure255.hostgator.com/~claudius/wp-content/uploads/2013/05/cedilla-im.png)