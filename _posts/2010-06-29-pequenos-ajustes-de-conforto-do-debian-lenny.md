---
id: 203
title: 'Pequenos ajustes de conforto do Debian &#8220;Lenny&#8221;'
date: 2010-06-29T15:35:50-03:00
author: @rsveiras
layout: post
guid: http://www.rodrigoeiras.eti.br/?p=203
permalink: /2010/06/29/pequenos-ajustes-de-conforto-do-debian-lenny/
aktt_notify_twitter:
  - 'no'
  - 'no'
categories:
  - Linux
tags:
  - debian
  - vim
---
Provavelmente isso funciona nas demais versões, mas não testei.

Para fazer o VIM como editor padrão do sistema para programas como &#8220;crontab&#8221;, edite o arquivo ~/.bashrc e adicione a linha:

> export EDITOR=/usr/bin/vim 

Neste mesmo arquivo, você pode descomentar as linhas:

> <div id="_mcePaste">
>   export LS_OPTIONS=&#8217;&#8211;color=auto&#8217;
> </div>
> 
> <div id="_mcePaste">
>   eval &#8220;`dircolors`&#8221;
> </div>
> 
> <div id="_mcePaste">
>   alias ls=&#8217;ls $LS_OPTIONS&#8217;
> </div>
> 
> <div id="_mcePaste">
>   alias ll=&#8217;ls $LS_OPTIONS -l&#8217;
> </div>
> 
> <div id="_mcePaste">
>   alias l=&#8217;ls $LS_OPTIONS -lA&#8217;
> </div>

Isso deixará o comando &#8220;ls&#8221; com definições coloridas.  
[]&#8217;s!