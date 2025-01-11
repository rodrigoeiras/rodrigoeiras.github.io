---
id: 115
title: 'Postfix &#8211; Aplicando Patch &#8220;VDA&#8221;'
date: 2010-05-07T16:38:46-03:00
author: Rodrigo Eiras
permalink: /2010/05/07/postfix-aplicando-patch-vda/
categories:
  - Geral
  - Linux
  - Redes / Sistemas
tags:
  - debian
  - Linux
  - postfix
  - vda
---
Bem, chegou a hora de atualizar nosso servidor de e-mail.

Na verdade estamos mudando toda a topologia, mas isso fica para um próximo post. O fato é que como usamos OpenLDAP aqui na instituição, a quota de e-mail também é informada nos diretórios dele. Para isso ser possível no postfix, é necessário aplicar um patch chamado VDA. (<http://vda.sourceforge.net/>)

Meu cenário, Linux, é o Debian Lenny e os downloads estão sendo feitos em /usr/src

Recomendo o utilizar o fonte diretamente do Debian:

> apt-get source postfix

Ao término, ele estará depositado em /usr/src

No Debian 5 &#8211; Lenny, o Postfix é o de versão 2.5.5, por isso, vamos baixar o patch relacionado a esta  versão:

> wget http://vda.sourceforge.net/VDA/postfix-2.5.5-vda-ng.patch.gz

Se sua arquitetura é x64, baixe também o patch abaixo:

> wget http://vda.sourceforge.net/VDA/postfix-2.5.5-vda-ng-64bit.patch.gz

Entre no diretório onde esta o &#8220;source&#8221; do postfix e aplique o patch vda, e em seguida se for o seu caso, aplique o patch x64:

> cd /usr/src/postfix-2.5.5
>
> patch -p1 < /usr/src/postfix-2.5.5-vda-ng.patch.gz
>
> (Opcional x64): patch -p1 < /usr/src/postfix-2.5.5-vda-ng-64bit.patch.gz

Os patchs estão instalados.

Basta agora criar um pacote de instalação .deb

P.S.: Primeiro, é  necessário resolver essas dependências para a criação do pacote:

> <div id="_mcePaste">
>   apt-get install build-essential
> </div>
>
> <div>
>   apt-get install debhelper po-debconf lsb-release libdb-dev libldap2-dev libpcre3-dev libmysqlclient15-dev libmysqlclient14-dev libssl-dev libsasl2-dev libpq-dev libcdb-dev tinycdb hardening-wrapperapt-get install debhelper po-debconf lsb-release libdb-dev libldap2-dev libpcre3-dev libmysqlclient15-dev libmysqlclient14-dev libssl-dev libsasl2-dev libpq-dev libcdb-dev tinycdb hardening-wrapper
> </div>

<div>
  Agora sim podemos criar o pacote e em seguida instalar:
</div>

> <div>
>   cd /usr/src/postfix-2.5.5
> </div>
>
> <div>
>   dpkg-buildpackage
> </div>

<div>
  O comando de instalação é d<em>pkg -i nomedopacote </em> e os mesmos se encontram em /usr/src
</div>

<div>
  []&#8217;s!
</div>
