---
id: 182
title: Site péssimo, Linhas Aéreas Gol
date: 2007-10-16T19:48:10+00:00
author: Claudio Miranda
layout: post
permalink: /2007/10/Site-pessimo-Linhas-Aereas-Gol/
categories:
  - Diversos
---
­<more>

A empresa aérea Gol, com preços baixo oferece vantagens frente às concorrentes. 

Mas não tente usar o serviço de atendimento virtual, pois não funciona. 

Tanto o atendimento on-line e o formulário de contato não funcionam. 

Tentei usar o serviço de [atendimento por chat](http://gol.directtalk.com.br/clientes/custom/voegol/init_atendimento_online.htm), onde solicitam várias informações (nome, telefone, cpf, email, cidade, estado, etc), foram preenchidas corretamente (inclusive a máscara de formatação&nbsp; 11-2222-3333), mas algum javascript rídiculo (com seu popup) não hesitava em me informar que o email ou o telefone foi preenchido incorretamente. Basta pressionar o botão de envio seguidas vezes que a validação ignóbil se alterna entre os dois campos. Desconfio que esse problema seja porque a equipe de TI da Gol, imagine que só exista plataforma windows. Ponto negativo para a equipe TI da Gol. 

</more>

Então tentei usar o [formulário de contato](http://www.voegol.com.br/faleconosco/faleconosco.aspx), para escrever sobre esse problema, onde após preencher todos os campos e escrever o motivo original (onde salvei em outro editor, para segurança), ao submeter, surge a seguinte tela 

<center>
  <br /> <img src="/resources/claudio/071016_gol1.png" /><br />
</center>

Já que não é possível enviar formulário, então desabilitem isso. O que é deprimente, a mensagem é estúpida.
  
  
</p> 

Outro problema, é ao clicar nos links das promoções da página principal (atualmente aparece a promoção da volta por R$ 10), é aberta uma página que tem o link para acesso à compra da passagem, mas quando clica-se no link para escolher o trecho, surge uma página em branco, nada mais. Então olhando o código fonte HTML, vejo outra agressão ao padrão HTML 

<pre>&lt;<span class="start-tag">html</span>&gt;
&lt;<span class="start-tag">head</span>&gt;
&lt;<span class="start-tag">title</span>&gt;Gol linhas Aéreas Inteligentes&lt;/<span class="end-tag">title</span>&gt;
&lt;<span class="start-tag">form</span><span class="attribute-name"> method</span>=<span class="attribute-value">"post" </span><span class="attribute-name">name</span>=<span class="attribute-value">"frmRedirect" </span><span class="attribute-name">action</span>=<span class="attribute-value">"http://compre3.voegol.com.br/skylights/cgi-bin/skylights.cgi"</span>&gt;
&lt;<span class="start-tag">input</span><span class="attribute-name"> type</span>=<span class="attribute-value">"hidden" </span><span class="attribute-name">name</span>=<span class="attribute-value">"module" </span><span class="attribute-name">value</span>=<span class="attribute-value">"SB"</span>&gt;
&lt;<span class="start-tag">input</span><span class="attribute-name"> type</span>=<span class="attribute-value">"hidden" </span><span class="attribute-name">name</span>=<span class="attribute-value">"language" </span><span class="attribute-name">value</span>=<span class="attribute-value">"PT"</span>&gt;
&lt;<span class="start-tag">input</span><span class="attribute-name"> type</span>=<span class="attribute-value">"hidden" </span><span class="attribute-name">name</span>=<span class="attribute-value">"mode" </span><span class="attribute-name">value</span>=<span class="attribute-value">"JURO"</span>&gt;
&lt;/<span class="end-tag">form</span>&gt;
&lt;<span class="start-tag">script</span><span class="attribute-name"> language</span>=<span class="attribute-value">"javascript"</span>&gt;
frmRedirect.submit();
&lt;/<span class="end-tag">script</span>&gt;
&lt;/<span class="end-tag">body</span>&gt;
&lt;/<span class="end-tag">html</span>&gt;
</pre>

Para resolver isso basta concatenar os inputs em uma requisição GET 

<pre>http://compre3.voegol.com.br/skylights/cgi-bin/skylights.cgi?module=SB&language=PT&mode=JURO
</pre>

Se com o firefox é assim, imaginem os usuários Opera e Konqueror. Para não falar de outros navegadores mais exóticos.