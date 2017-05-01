---
id: 187
title: Descobrindo senha de banco de dados
date: 2007-10-26T07:17:47+00:00
author: Claudio Miranda
layout: post
permalink: /2007/10/Descobrindo-senha-de-banco-de-dados/
categories:
  - Dicas
---
<img align="right" src="/resources/claudio/tips_icon.gif" alt="Dicas" hspace="80" />

Você já passou por aquela situação de desconfiança, onde ao informar a senha de acesso ao banco de dados e pensou &#8220;poxa, tenho de informar a senha em texto limpo ?&#8221;, desejando que a senha estivesse cifrada. 

Isso por padrão ocorre em alguns servidores de aplicativos, onde a senha de acesso ao banco de dados é informada em texto limpo, em outros servidores de aplicativos a senha ecoa em asteriscos, deixando o usuário confortável que a senha está segura. Bem, não acredite nisso, a senha não está segura. 

O que quero mostrar é que a senha pode ser extraida de outras maneiras, como inspecionar os pacotes de mensagens IP. O que pode garantir a senha é uma combinação de práticas e configurações para deixar o ambiente mais seguro. 

<cortar> 

Passo aqui um exemplo de como obter a senha do oracle configurado em um servidor de aplicativos conhecido no mercado.
  
  


Vejam abaixo na configuração da conexão, que a senha esta protegida por asteriscos 

<img src="/resources/claudio/071022_weblogic_1.png" align="bottom" border="1" hspace="0" vspace="0" />
  
  


Faça os seguintes passos, para ver a senha no log 

  1. Usar a biblioteca JDBC de debug da oracle: <span style="font-family: monospace;">ojdbc14_d.jar</span> 
  2. Usar o driver XA <span style="font-family: monospace;">oracle.jdbc.xa.client.OracleXADataSource</span>
  3. Incluir as seguintes propriedades de JVM
  
    </p> 
    <pre>-Doracle.jdbc.Trace=true
-Doracle.jdbc.LogFile=/var/tmp/oracle-trace/trace1
</pre>

  4. Reiniciar o servidor de aplicativos 

Basta acompanhar o log de trace do oracle ou do servidor de aplicativos, que a senha será impressa desta maneira 

<pre>INFO: OracleXADataSource.getXAConnection()
03/10/2007 15:33:16 oracle.jdbc.xa.client.OracleXADataSource getXAConnection
INFO: OracleXADataSource.getXAConnection(user = claudio, <b>passwd = admin123</b>)
03/10/2007 15:33:16 oracle.jdbc.driver.PhysicalConnection setAutoCommit
</pre>

Bonito não é ? 

Para o Oracle é usado uma [funcionalidade documentada](http://www.oracle.com/technology/tech/java/sqlj_jdbc/htdocs/jdbc_faq.htm#32_00), que é o trace das chamadas. Mas infelizmente, a senha é impressa junto. E vejam que nem com SSL, a senha é protegida. 

E é necessário ter privilégios de administração do servidor de aplicativos. 

Quando que isso pode ser útil ? 

Já trabalhei em lugares onde a senha do banco de dados, era digitada no console do appserver, pelo próprio pessoal da equipe de DBA, e em algumas situações era necessário realizar alguma pesquisa no BD, então essa dica vale a pena. 

Em banco de dados de código livre fica mais fácil, basta usar o código fonte do driver JDBC, modificar o código fonte para imprimir a senha e pronto. 

Em banco de dados que não são de código livre, basta criar sua classe que estende [DataSource](http://java.sun.com/j2se/1.5.0/docs/api/javax/sql/DataSource.html) e sobrecarregar o método getConnection e fazer um proxy para o DataSource do driver JDBC. 

Então, percebam que os asteriscos no textfield não significam segurança para a senha do banco de dados. 

Tenho essa dica há uns 3 anos e percebi que não escrevi sobre ela ainda.

Se essa dica foi útil para você, deixe um comentário, informando como ela lhe ajudou !&nbsp; </p>