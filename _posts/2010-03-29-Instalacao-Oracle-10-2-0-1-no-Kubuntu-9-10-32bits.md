---
id: 240
title: Instalação Oracle 10.2.0.1 no Kubuntu 9.10 (32bits)
date: 2010-03-29T02:14:18+00:00
author: Claudio Miranda
layout: post
permalink: /2010/03/Instalacao-Oracle-10-2-0-1-no-Kubuntu-9-10-32bits/
categories:
  - Dicas
---
Segue um tutorial de instalação do banco de dados Oracle 10.2.0.1 no Ubuntu 32 bits. Apesar de existir uma versão Express Edition, precisei instalar o 10.2.0.1 no meu laptop. Veja que este é um artigo que visa linux 32 bits, para 64 bits os parametros podem ter outros valores. Esta instalação é apenas para desenvolvimento, se você procura por uma instalação do oracle que irá servir muitos usuários, procure por maiores informações na internet.
  
  


O Ubuntu não é listado como uma distribuiçao suportada, mas isso não quer dizer que não pode instalar no ubuntu. Tem alguns ajustes manuais, veja quais são. 

Como o Oracle DB não é uma instalação next, next, nem é um serviço trivial, recomendo ler o <a target="_blank" href="http://www.oracle.com/pls/db102/to_pdf?pathname=install.102/b15663.pdf&remark=portal+(Books)">Quick Install Guide</a> onde é explicado em detalhes algumas instruções. 

1) Pre-requisitos e preparação do ambiente 

&nbsp;1.1) SWAP 

Na instalação o oracle deverá checar o tamanho da área de swap de acordo com as regras abaixo:
  
  
</p> 

<table style="width: 30%; display: table;" align="left" border="1" cellpadding="1" cellspacing="1">
  <tr>
    <td style="width: 50%; background-color: rgb(210, 210, 210);">
      <strong>&nbsp;Memória RAM<br /> <br /></strong>
    </td>
    
    <td style="width: 50%; background-color: rgb(210, 210, 210);">
      <strong>Tamanho do SWAP<br /> <br /></strong>
    </td>
  </tr>
  
  <tr>
    <td style="width: 50%;">
      &nbsp;Até 1 GB<br />
    </td>
    
    <td style="width: 50%;">
      2 x RAM<br />
    </td>
  </tr>
  
  <tr>
    <td style="width: 50%;">
      &nbsp;De 1 a 2 GB<br />
    </td>
    
    <td style="width: 50%;">
      1,5 x RAM<br />
    </td>
  </tr>
  
  <tr>
    <td style="width: 50%;">
      &nbsp;De 2 a 8 GB<br />
    </td>
    
    <td style="width: 50%;">
      Igual a RAM<br />
    </td>
  </tr>
  
  <tr>
    <td style="width: 50%;">
      &nbsp;Maior que 8 GB<br />
    </td>
    
    <td style="width: 50%;">
      0,75 x RAM<br />
    </td>
  </tr>
</table>

&nbsp;

&nbsp; 



&nbsp; 

  
No meu caso, tenho 3 GB RAM e 1 GB de swap, para não precisar redimensionar o tamanho do swap e gastar muito tempo, é possível criar um arquivo de swap e adicionar isso no kernel em runtime, quando a instalação terminar, pode remover o arquivo. <a target="_blank" href="http://www.cyberciti.biz/faq/linux-add-a-swap-file-howto/">Veja como fazer isso</a>.
  
  


1.2) Criação de grupos e usuário, diretório&nbsp; </p> 

<pre>sudo groupadd oinstall
sudo groupadd dba
sudo groupadd nobody
</pre></p> 

<pre>sudo usermod -g nobody nobody
sudo mkdir -p /opt/oracle
sudo useradd -g oinstall -G dba  -d /opt/oracle -s /bin/bash oracle
sudo chown -R oracle:oinstall /opt/oracle
</pre>

Coloque uma senha para o usuário oracle </p> 

<pre>sudo passwd oracle</pre>

1.2) Atualização dos parametros do kernel 

Preste muita atenção nesta tarefa. 

Antes faça um backup dos valores atuais do kernel 

sudo sysctl -a > ~/sysctl_bkp 

Edite o arquivo /etc/sysctl.conf e altere os seguintes parametros 

<pre># Oracle
kernel.sem = 250 32000 100 128
net.ipv4.ip_local_port_range = 32768 65000
kernel.shmmax=1073741824
net.core.rmem_default = 1048576
net.core.rmem_max = 1048576
net.core.wmem_default = 262144
net.core.wmem_max = 262144
</pre>

Coloquei apenas 1 GB para memória compartilhada no Oracle, apesar da documentação pedir a metade.

Chame o comando abaixo, para colocar em efeito os parametros alterados.
  
  


sudo sysctl -p
  
  


1.3) Alterar os limites 

<pre>sudo vi /etc/security/limits.conf
</pre>

<pre># Oracle
oracle           soft    nproc   2047
oracle           hard    nproc   16384
oracle           soft    nofile  1024
oracle           hard    nofile  65536
</pre>

1.4) Instalação de pacotes adicionais 

É necessário instalar alguns programas adicionais 

<pre>m4
autoconf
autotools-dev
automake
gsfonts-x11
lesstif2
libaio1
sysstat
zlibc
libstdc++5
dpkg-dev
html2text
gettext
intltool-debian
po-debconf
debhelper
librpmio0
librpm0
librpmbuild0
rpm
alien
libstdc++6-4.4-dev
g++-4.4
g++
build-essential
fakeroot
libsys-hostname-long-perl
libmail-sendmail-perl

</pre>

É necessário instalar o libstdc++5, que pode ser copiado de 

<pre>http://mirrors.kernel.org/ubuntu/pool/universe/g/gcc-3.3/libstdc++5_3.3.6-17ubuntu1_i386.deb
</pre>

O Oracle espera alguns comandos em um caminho que não existe no ubuntu, então vamos arrumar </p> 

<pre>sudo ln -s /usr/bin/awk /bin/awk
sudo ln -s /usr/bin/rpm /bin/rpm
sudo ln -s /usr/bin/basename /bin/basename</pre>

Crie um arquivo de profile para o usuário oracle 

<pre>su - oracle
vi ~/.bashrc</pre>

Informe 

<pre>umask 022
</pre>

Esteja certo de que o hostname responde com um IP, faça um ping no nome do computador.
  
  


Reinicie o seu sistema operacional&nbsp; 

2) Instalação do Oracle 

Configure a permissão para que outros usuários possam iniciar programas gráficos 

<pre>xhost +</pre>

Faça o login com o usuário oracle

<pre>su - oracle
export DISPLAY=:0
</pre>

Chame o instalador do oracle 

<pre>./runInstaller -ignoreSysPrereqs
</pre>

A opção&nbsp; -ignoreSysPrereqs desabilita a verificação de compatibilidade do sistema operacional. 

Durante a instalaçã
  
  


3) Pós instalação
  
  


A instalação GUI aconteceu sem maiores problemas,&nbsp; demorou cerca de 20min. 

Segue alguns ajustes para bom funcionamento do ambiente
  
  


3.1) /etc/oratab
  
  


Foi gerado um arquivo em /etc/oratab, mas não foi colocado o local da instalação do oracle, e isso é importante para iniciar e parar o oracle. 

Coloque uma linha como o formato. Se desejar que o oracle seja iniciado com o sistema operacional, deixeo Y caso contrário, coloque N
  
  


<pre>$ORACLE_SID:$ORACLE_HOME:Y</pre>

No meu caso é assim:
  
  


<pre>APPS:/opt/oracle/oracle/product/10.2.0/db_1:Y&nbsp;
</pre>

3.2) Ambiente oracle
  
  


Configure no /etc/profile as váriaveis de ambiente. As variáveis serão globais para o sistema operacional.
  
  
</p> 

<pre>export ORACLE_HOME=/opt/oracle/oracle/product/10.2.0/db_1
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME/lib
export PATH=$PATH:$ORACLE_HOME/bin
export NLS_LANG=english
</pre>

Coloquei o NLS_LANG para inglês para as mensagens de interface do sqlplus serem em inglês, o que facilita muito o trabalho. Veja <a target="_blank" href="http://www.claudius.com.br/blog/claudio/2008/04/19/Tradu%E7%E3o-de-aplica%E7%F5es">minha opinião sobre a tradução de sistemas</a>. 

Edite o $ORACLE\_HOME/bin/dbstart e altere a declaração da variável ORACLE\_HOME\_LISTENER&nbsp; (linha 78 aproximadamente) para $ORACLE\_HOME, como o exemplo </p> 

<pre>ORACLE_HOME_LISTNER=$ORACLE_HOME
</pre>

3.3) Inicialização do oracle 

Faça o login como usuário oracle e inicie o servidor </p> 

<pre>lsnrctl start
dbstart
</pre>

&nbsp; 

3.4) rlwrap e sqlplus (opcional)
  
  


Para quem já usou o sqlplus sabe que ele não mantém um histórico dos comandos, como o bash. Seria muito útil ter um comportamento semelhante o bash, onde no console do sqlplus o usuário possa buscar no histórico (ctrl+r) ou navegar com as setas. 

Isso é possível como rlwrap 

<pre>sudo apt-get install rlwrap
</pre>

Então chame 

<pre>rlwrap sqlplus usuario/senha@oracle_sid</pre>

3.4.5) Uma dica a parte, ao usarem o sqlplus para conectar em um serviço que não esteja configura o tnsnames.ora, é possível passar o servidor e porta. 

<pre>sqlplus usuario/senha@//nome_servidor:porta/oracle_sid</pre>

Para parar o Oracle 

<pre>dbshut
lsnrctl stop
</pre>

&nbsp; 

M
  
  


http://www.makina-corpus.org/blog/how-install-oracle-10g-full-64-bits-version-not-xe-and-tora-gnu-linux-ubuntu-karmic-910-64-bits
    
  
http://www.pythian.com/news/968/installing-oracle-11g-on-ubuntu-804-lts-hardy-heron/
    
  
&nbsp;