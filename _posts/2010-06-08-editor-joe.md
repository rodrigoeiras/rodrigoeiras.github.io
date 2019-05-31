---
id: 131
title: 'Editor &#8220;joe&#8221;'
date: 2010-06-08T15:30:15-03:00
author: @rsveiras
layout: post
guid: http://www.rodrigoeiras.eti.br/?p=131
permalink: /2010/06/08/editor-joe/
aktt_notify_twitter:
  - 'yes'
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - Geral
tags:
  - editor
  - joe
---
Apesar do &#8220;VIM&#8221; ser bem completo, às vezes gosto de utilizar o editor _joe_ para edições rápido no console do linux. Para quem não conhece, o mesmo é um clone do wordstar. Os comandos são todos parecidos ou iguais.

Quem quiser experimentar, no Debian basta instalar pelo _apt-get_.

> apt-get install joe

Os arquivos de configuração do _joe_ ficam /etc/joe

�? interessante é editar o arquivo /etc/joe/joerc e remover (eu acho) a função de backup do mesmo, que polui o sistema de arquivos e adicionar uma sintaxe de cores.

Procure por &#8220;Default Local Options&#8221;  e adicione as linhas:

> -syntax sh
> 
> -nobackups

[]&#8217;s!