---
id: 394
title: Melhorias no console gráfico Wildfly 8
date: 2014-02-12T13:03:47+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=394
permalink: /2014/02/melhorias-no-console-grafico-wildfly-8/
categories:
  - Dicas
  - Java
---
Foi liberado a versão final do <a href="http://wildfly.org/downloads/" target="_blank">Wildfly 8</a>, o servidor de aplicativos Java EE 7 do JBoss.

Em Janeiro, <a href="https://github.com/hal/core/pull/10" target="_blank">fiz uma contribuição</a> para o <a href="https://github.com/hal/core" target="_blank">HAL</a>, console gráfico de gerenciamento do Wildfly 8, com algumas pequenas melhorias

Filtro de pesquisa indiferente de maiúsculas/minúsculas na lista de deployments.

Filtro de pesquisa de texto em qualquer posição da String (antes pesquisa apenas no início da String), na janela de deployments.

[<img class="alignnone size-full wp-image-395" alt="deploy_filter" src="/wp-content/uploads/2014/02/deploy_filter.png" width="748" height="320" srcset="http://claudius.com.br/wp-content/uploads/2014/02/deploy_filter.png 748w, http://claudius.com.br/wp-content/uploads/2014/02/deploy_filter-300x128.png 300w, http://claudius.com.br/wp-content/uploads/2014/02/deploy_filter-730x312.png 730w" sizes="(max-width: 748px) 100vw, 748px" />](/wp-content/uploads/2014/02/deploy_filter.png)

Ordenação insensível de maiúsculas/minúsculas na lista de deployments.

[<img class="alignnone size-full wp-image-399" alt="deploy_sort" src="/wp-content/uploads/2014/02/deploy_sort.png" width="761" height="408" srcset="http://claudius.com.br/wp-content/uploads/2014/02/deploy_sort.png 761w, http://claudius.com.br/wp-content/uploads/2014/02/deploy_sort-300x160.png 300w, http://claudius.com.br/wp-content/uploads/2014/02/deploy_sort-730x391.png 730w" sizes="(max-width: 761px) 100vw, 761px" />](/wp-content/uploads/2014/02/deploy_sort.png)
  
Filtro de pesquisa indiferente de maiúsculas/minúsculas na lista de propriedades.

Filtro de pesquisa de texto em qualquer posição da String (antes pesquisa apenas no início da String), na janela de propriedades.

Ordenação insensível de maiúsculas/minúsculas na lista de propriedades.
  
[<img class="alignnone size-full wp-image-398" alt="env_props_filter" src="/wp-content/uploads/2014/02/env_props_filter.png" width="989" height="366" srcset="http://claudius.com.br/wp-content/uploads/2014/02/env_props_filter.png 989w, http://claudius.com.br/wp-content/uploads/2014/02/env_props_filter-300x111.png 300w, http://claudius.com.br/wp-content/uploads/2014/02/env_props_filter-730x270.png 730w" sizes="(max-width: 989px) 100vw, 989px" />](/wp-content/uploads/2014/02/env_props_filter.png)

Teste de datasource, no modo domain (já existia no modo standalone).

Flush de datasource, no modo domain (já existia no modo standalone).

[<img class="alignnone size-full wp-image-397" alt="ds_teste_flush" src="/wp-content/uploads/2014/02/ds_teste_flush.png" width="1078" height="568" srcset="http://claudius.com.br/wp-content/uploads/2014/02/ds_teste_flush.png 1078w, http://claudius.com.br/wp-content/uploads/2014/02/ds_teste_flush-300x158.png 300w, http://claudius.com.br/wp-content/uploads/2014/02/ds_teste_flush-1024x539.png 1024w, http://claudius.com.br/wp-content/uploads/2014/02/ds_teste_flush-730x384.png 730w" sizes="(max-width: 1078px) 100vw, 1078px" />](/wp-content/uploads/2014/02/ds_teste_flush.png)

Ao associar um deployment para os grupos de servidores, foi adicionado um texto, informando que o usuário pode usar ctrl+click para selecionar múltiplos checkbox. Por ser botões checkbox, intuitivamente o usuário apenas clica nos checkbox, mas isso não seleciona vários checkbox. É necessário o ctrl+click, por isso o texto de ajuda.
  
[<img class="alignnone size-full wp-image-396" alt="assign_help" src="/wp-content/uploads/2014/02/assign_help.png" width="502" height="294" srcset="http://claudius.com.br/wp-content/uploads/2014/02/assign_help.png 502w, http://claudius.com.br/wp-content/uploads/2014/02/assign_help-300x175.png 300w" sizes="(max-width: 502px) 100vw, 502px" />](/wp-content/uploads/2014/02/assign_help.png)

&nbsp;