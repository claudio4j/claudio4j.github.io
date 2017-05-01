---
id: 205
title: Tradução de aplicações
date: 2008-04-19T00:14:58+00:00
author: Claudio Miranda
layout: post
permalink: /2008/04/Traducao-de-aplicacoes/
categories:
  - Java
---
Você conhece termos como "bean de ligação", "gerenciador de cronometro", "ligação ao espaço de nomes JNDI", "Aplicativos corporativos" (este talvez seja mais fácil), relacionados a plataforma Java Enterprise Edition ?

Pois para mim, são termos novos para incorporar ao festival de palavras difusas.

Isso não é nada mais que a tradução da da interface web de administração de um servidor Java EE.

Veja um exemplo abaxo:&nbsp;</p> 

[<img border="0" src="/resources/claudio/080418-ws_ptbr1_sm.png" />](/resources/claudio/080418-ws_ptbr1.png "Clique para ampliar")
      
  
Clique na imagem para ampliar&nbsp;

Nesta situação, acredito que a tradução irá causar mais problemas do que ajudar, no longo prazo.
      


**Problemas**

  * Maior custo do produto (exige uma equipe para tradução)
        
    
  * Maior tempo para releases
        
    
  * Termos não são apropriados para buscas na internet (tente efetuar uma busca por "gerenciador de cronometro")
  * Confusão de termos para quem usou outro fornecedor
  * Documentação suplementar, estará em inglês
  * Produtos de terceiros em inglês

**Vantagens**

  * Capacidade de usar a ferramenta, para quem não entende de inglês básico

Não consegui encontrar outras vantagens, por favor, escreva no comentário se encontrar alguma outra vantagem.
      


Na seção de problemas, o que verifico ser o pior deles, é quando o usuário da interface de administração, encontra alguma exceção e efetua a busca na internet, vai encontrar nada ou pouca informação.

E em outras telas da interface, termos em inglês são usados, causando confusão para os que não possuem inglês básico. (Como seria a tradução do termo "listener" ?)

**Colocando um contexto na situação.**

Considere um profissional para usar a ferramenta. Ele é um profissional que irá lidar com conceitos e conhecimento em:
      


  * cluster
  * balanceamento de carga
  * topologia
  * instalação de aplicação
  * components e módulos
  * criptografia
  * configuração de rede
  * classpath e classloader
  * mapeamento de nomes
  * etc.

E para entender isso e ser responsável pelo pleno funcionamento do ambiente, certamente É uma pessoa com bons conhecimentos técnicos em diversas áreas de informática, e com certeza um profissional que deve ter lido algum livro em inglês e/ou artigos na internet em inglês. Logo a interface web de um servidor Java, é necessário apenas inglês instrumental e ainda assim relacionado a área de informática.

Na situação onde precisei usar a interface de administração, uma das primeiras coisas que fiz, foi alterar o idioma da interface, pois estava complicado em demasiado, tentar decifrar o que significava a tradução do termo.

**Javaum e feijões corporativos**
      


O que lembro ainda hoje e é motivo de risadas, foi no evento Sun Tech Days em 2002, durante uma palestra em inglês, quando um colega que estava com o fone da tradução simultânea, perguntou para mim o que significava javaum, mas não precisei explicar, após ele escutar o termo feijões corporativos.
      


&nbsp;

**Crítica**

Note que isso não é uma crítica ao incrível trabalho dos profissionais de tradução, que tem de lidar com esta situação de construir um dicionários de itens que não são passíveis de tradução, e não são pessoas técnicas.

Existem diversas ferramentas que precisam ser traduzidas, estas são as ferramentas para o usuário comum, usuário iniciante, ou pessoas que realmente não tem o inglês instrumental, mas desejam usar o sistema. Exemplo disso são os sistemas desktop (navegadores de internet, email, ferramentas desktop em geral).
      


Cito o NetBeans, como exemplo (onde tenho alguns colegas que participam da tradução), que é uma ferramenta que jovens que conhecem poucos termos em inglês e de informática, então diminue bastante a barreira de introdução à tecnologia.

Mas no longo prazo, o iniciante passa pelo intermediário e depois mais experiência, o que nesta fase, já passou pelo aprendizado da língua inglesa. O que vejo muito comum em fóruns e conversas de informática, é que sem o entendimento do idioma inglês na área de informática, o profissional terá poucas chances de sobreviver à evolução na carreira.
      


A minha crítica é para as empresas que querem traduzir este tipo de sistema, que como expliquei acima, não traz vantagens.
      


&nbsp;