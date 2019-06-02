---
id: 208
title: 'Habilitando checagem de SPF no Postfix &#8211; Debian &#8220;Lenny&#8221;'
date: 2010-07-02T15:58:51-03:00
author: Rodrigo Eiras
permalink: /2010/07/02/habilitando-checagem-de-spf-no-postfix-debian-lenny/
categories:
  - Linux
  - Postfix
tags:
  - debian
  - libspf
  - Linux
  - postfix
  - spf
---
<p style="text-align: justify;">
O SPF (Sender Police Framework) é uma tecnologia que informa a outros servidores de email quais endereços IP estão autorizados a enviar mensagens com seu domínio, evitando assim que outros servidores praticantes de SPAM, possam forjar e-mails em seu nome.

Não tratarei aqui em como publicar um registro SPF no DNS, mas posso pensar nisso para um próximo post.  
Para saberem mais sobre o SPF, sigam em: <http://www.antispam.br/admin/spf/>

Partindo do pressuposto que seu Postfix esteja já em funcionamento, instale o aplicativo.

> apt-get install postfix-policyd-spf-perl

Abra o arquivo main.cf

> vim /etc/postfix/main.cf

Adicione em **smtpd\_recipient\_restrictions**

> check\_policy\_service unix:private/policy

Insira a linha acima antes de regra de reject\_unauth\_destination, ou você poderá ter um open relay.  
Em seguida, abra o arquivo:

> vim /etc/postfix/master.cf

Adicione o seguinte conteúdo ao arquivo:

> \# spf check  
> policy unix &#8211; n n &#8211; &#8211; spawn  
> user=nobody argv=/usr/bin/perl /usr/sbin/postfix-policyd-spf-perl

Agora é só reinicializar o postfix.  
\# /etc/init.d/postfix restart

🙂

Abraços!
