---
id: 245
title: Dicas Thunderbird
date: 2010-07-07T23:20:28+00:00
author: Claudio Miranda
layout: post
permalink: /2010/07/Dicas-Thunderbird/
categories:
  - Diversos
---
Duas dicas sobre o cliente de email thunderbird 

## Mensagens de notificação em preto
  


Fiz o upgrade para a versão 3.1 e as mensagens de alerta do thunderbird no linux, aparecem sem conteúdo, tudo preto, como abaixo. 

![](/resources/claudio/20100707_thunderbird_alert_1.png)
  
  


Vi que é um <a target="_blank" href="https://bugzilla.mozilla.org/show_bug.cgi?id=561427">bug do thunderbird</a>, onde o problema é enviar mensagens de notificação sem um título. 

Para corrigir, abra o arquivo thunderbird-3.1/modules/activity/alertHook.js e altere a linha abaixo, para incluir a palavra &#8220;Alert&#8221; (2o argumento)
  
  


<pre>this.alertService.showAlertNotification("chrome://branding/content/icon48.png", "Alert",aMessage);
</pre>

Reinicie o thunderbird, para valer a alteração.
  
  


Então as mensagens irão aparecer corretamente. 

![](/resources/claudio/20100707_thunderbird_alert.png)
  
  


## Indexação de mensagens
  


O thunderbird tem uma opção que realiza a indexação de todas as mensagens, onde é possível efetuar buscas nos textos de todas as mensagens e exibir de uma maneira mais organizada em uma tela&nbsp; só. 

No entanto o arquivo de índice vai ficando bem grande e percebi que o thunderbird dá um crash toda vez que saio dele. Seguindo uma recomendação que vi em alguns fórums, desabilitei esta indexação e não ocorreu mais crash e o arquivo de índice não é usado mais. 

Note que isso não prejudica em nada a pesquisa que o thunderbird já faz. 

Para desabilitar vá na opção abaixo e desative-a.
  
  


Preferências -> Avançado -> Geral -> Ativar pesquisa global e indexação