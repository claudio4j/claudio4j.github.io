---
id: 100
title: 'Servico de Hosting Solaris barato  &#8211; RECOMENDO'
date: 2006-07-28T17:32:40+00:00
author: Claudio Miranda
layout: post
permalink: /2006/07/Servico-de-Hosting-Solaris-barato-RECOMENDO/
categories:
  - Dicas
---
Trabalho com a locaweb há alguns anos, no entanto estou insatisfeito com 2 coisas:

  * POP/SMTP sem suporte a SSL (autenticação e tráfego)
  * Não suportar scp (apesar de que suportam ssh)

No chamado que já abri em outras oportunidades, o 1o item entrou como sugestão e o 2o é apenas para serviços de hosting dedicados.

Com isso, começei a procurar algun serviço de hospedagem com as premissas acima, com suporte a Java e banco de dados, com preço bom e que pudesse suportar. Infelizmente, não achei um serviço de hospedagem no Brasil que já tivesse os serviços, mas encontrei um serviço semi-dedicado, muito melhor.

![](http://www.mod3.co.uk/logo.jpg)



O serviço de uma empresa inglesa, [mod3.co.uk](http://www.mod3.co.uk/documentation/solaris-zones/zone-pricing), que oferece o seguinte

Pacote básico
  
=============

  * Um zone solaris
  * 1 GB de espaço em disco
  * Uso de CPU (slice)
  * 64 MB de memória RSS

Com **pagamento anual de 9,95** libras (moeda inglesa), [use o google para converter](http://www.google.com.br/search?q=%C2%A31+to+BRL). 

É possível aumentar a capacidade dos recursos, mas o preço sobe um pouquinho com pagamentos mensais, veja abaixo:

  * disc space £1 per GB
  * online backup £1 per GB
  * CPU slice £2 per slice
  * data transfer £3 per GB
  * RSS memory £4 per 64MB

O pessoal de atendimento foi rápido no atendimento e o pagamento é feito por paypal, com ativação do ambiente no dia seguinte.

Claro que existem vantagens e desvantagens neste cenário:

### Vantagens

  * Servidor semi-dedicado
  * Solaris 10
  * Pode instalar o que você quiser
  * Escalabilidade quando necessário
  * Preço reduzido

### Desvantagens

  * Administração dos serviços instalados
  * Configurações de segurança por sua conta

Especialmente para mim (ou para vocês e suas empresas), os serviços úteis:

  * IMAP/POP/SMTP com suporte a SSL na autenticação e tráfego de mensagens
  * Usar tunnel SSH quando estiver em algum cliente e for necessário usar serviços com segurança: IM, navegação, etc.
  * Usar certificados digitais mesmo com webmail, para assinar mensagens

Caso vocês usem o serviço deles, deixe uma mensagem dizendo como foi ou envie um [email para mim](mailto:blog-comments[colocar_arroba]claudius[ponto]com[ponto]b r).