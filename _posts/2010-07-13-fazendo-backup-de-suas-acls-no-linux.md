---
id: 249
title: 'Fazendo Backup de suas ACL&#8217;s no Linux'
date: 2010-07-13T11:00:57-03:00
author: Rodrigo Eiras
permalink: /2010/07/13/fazendo-backup-de-suas-acls-no-linux/
categories:
  - Linux
tags:
  - acl
  - ext3
---
<p style="text-align: justify;">
Então, nós nunca nos preocupamos em fazer backup de ACL&#8217;s até o dia em que precisamos migrar o servidor por qualquer motivo. Não é? Pois bem, não foi diferente no meu caso.


Eu já tinha pensado que iria ter que refazer todas as ACL&#8217;s manualmente e resolvi pesquisar. SIM! Existe uma forma de fazer backup e restore das mesmas, e é bem simples.


* Exportando as ACL&#8217;s para um arquivo texto:

> spitfire:/# getfacl -R /home > /root/home.acl


O comando acima, exporta as ACL&#8217;s aplicadas no /home para um arquivo texto chamando &#8220;home.acl&#8221; dentro de /root.


* Depois, basta usar o comando para restaurar a partir do arquivo:

> spitfire:/# setfacl &#8211;restore /root/home.acl

Reparem que, o comando de &#8220;restore&#8221; deve ser feito no mesmo local de onde foi o backup, no meu caso na raiz (/).


</p>
