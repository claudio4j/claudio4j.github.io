---
id: 153
title: Certificação Digital em Aplicações Java ME
date: 2007-04-17T14:28:30+00:00
author: Claudio Miranda
layout: post
permalink: /2007/04/Certificacao-Digital-em-Aplicacoes-Java-ME/
categories:
  - Java
---
Em uma <a target="_blank" href="https://soujava.dev.java.net/servlets/ReadMsg?list=j2me-list&msgNo=5978">thread de discussão do SouJava sobre assinatura de aplicações Java ME</a> com certificados, lembrei-me de um trabalho que fiz um tempo atrás sobre isso, e colaboro com a discussão. Respondi esta mensagem na lista de email, para ser arquivado e coloco no meu blog também.
  
  


Recentemente tive de investigar isso para celulares motorola e outros fabricantes, onde uma aplicação envia mensagens SMS e não é para aparecer um alerta solicitando permissão para efetuar a conexão. Para isso é necessário assinar a aplicaçao com um certificado emitido por uma autoridade certificadora (CA), e este CA já deve existir no telefone celular (geralmente na parte de configurações e segurança)

Tem um documento no site de desenvolvedores da motorola &#8220;[Midlet Testing and Signing](http://developer.motorola.com/techresources/testingcertification/testing_signing_programs/MIDlet_Testing_and_Signing.pdf)&#8221; que mostra bem os passos para assinatura de aplicações em telefones motorola. Recomedo a leitura.

Na [página 10 do documento](http://developer.motorola.com/techresources/testingcertification/testing_signing_programs/MIDlet_Testing_and_Signing.pdf) é possível requisitar um certificado de desenvolvimento (é um processo burocrático). Note que esse processo será usado para a obtençao de um certificado de produção. E mostra que o telefone motorola suporta certificados emitidos pelo CA da motorola, CA da operadora ou UTI (<a target="_blank" href="http://javaverified.com/jvProcess.jsp">Unified Testing Initiative, do programa Java Verified</a>). O CA da motorola somente é usado, quando existe um acordo como partner da morotola (envolvendo contratos, NDA, etc) e quando usar alguma característica específica da API da motorola.

Sobre o UTI, é burocrático também e caro. Pois exige o envio da aplicação para o UTI, então pode-se <a target="_blank" href="http://javaverified.com/test_providers.jsp">escolher uma empresa para testar a aplicação</a> eles testam e se der qualquer erro, eles cancelam o programa de testes, então é necessário submeter uma versão da aplicação corrigida e o teste refeito. E para cada teste e cada device é cobrado um preço, <a target="_blank" href="http://www.relquti.com/UTI/services.htm">veja</a> <a target="_blank" href="http://unified-testing-initiative.ra.adc-hosting.fr.capgemini.com/marketing.htm">preços</a> de dois fornecedores. Note que este preço inclui&nbsp; teste e a asssinatura se der tudo certo. 

Outro cenário é saber se todos os telefones o CA ROOT da UTI. Veja os telefones que o suportam na <a target="_blank" href="http://javaverified.com/supp_devices.jsp">tabela existente no website</a>.

Para os devices que não suportam o UTI é necessário checar com o fabricante, qual o CA ROOT que é disponibilizado em cada aparelho. Para saber isso é necessário checar no website de desenvolvedores de cada fabricante os certificados suportados em cada device. Ou olha em cada aparelho qual é o CA ROOT disponível. 

Um exemplo, eu tenho o telefone <a target="_blank" href="http://forum.nokia.com/devices/3650">Nokia 3650</a>, que tem instalado o CA ROOT: Verisign, Thawte, Cybertrust, etc. Então não suporta o UTI, teria de pagar para a <a target="_blank" href="https://www.thawte.com/ssl-digital-certificates/code-signing/index.html">Thawte por um certificado de para assinatura de aplicações</a>, que custa US$ 159. Se a mesma aplicação tiver de ser instalada em outro telefone que não suporta Thawte, teria os custos de certificado desse CA ROOT.
  
  


Informações complementares, que encontrei no website da motorola (é necessário ter login no website):

<a target="_blank" href="https://motocoder.custhelp.com/cgi-bin/motocoder.cfg/php/enduser/std_adp.php?p_faqid=733&p_created=1121847546">I am a Motorola Partner, how do I obtain Partner Access to the MOTODEV website?</a>
    
  
<a target="_blank" href="https://motocoder.custhelp.com/cgi-bin/motocoder.cfg/php/enduser/std_adp.php?p_faqid=708&p_created=1119609364">Development MIDlet Signing Process</a>
    
  
<a target="_blank" href="https://motocoder.custhelp.com/cgi-bin/motocoder.cfg/php/enduser/popup_adp.php?p_req_pass=1&p_sid=-4OaEkvi&auth=&p_sid=-4OaEkvi&p_lva=undefined&p_sp=undefined&p_faqid=936&p_created=1156476507&p_accessibility=">Signing Midlets with a VeriSign or Thawte Certificate</a>

E um <a target="_blank" href="http://blog.javia.org/?p=42">blog comentando sobre a assinatura de aplicações Java ME</a>.