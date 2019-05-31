---
id: 273
title: 'OpenLDAP no Debian 6 &#8211; &#8220;Squeeze&#8221;'
date: 2011-05-03T12:08:45-03:00
author: @rsveiras
layout: post
guid: http://www.rodrigoeiras.eti.br/?p=273
permalink: /2011/05/03/openldap-no-debian-6-squeeze/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - Linux
  - Redes / Sistemas
tags:
  - debian
  - debian6
  - openldap
  - slapd
---
<p style="text-align: justify;">
  Algumas pessoas já perceberam uma pequena mudança no OpenLDAP no Debian 6.
</p>

<p style="text-align: justify;">
  Pois bem, na verdade o sistema continua trabalhando da mesma forma, somente a forma de lidar com o slapd.conf que mudou.
</p>

<p style="text-align: justify;">
  Para começar, o slapd.conf não é mais criado na instalação do pacote, então devemos faze-los manualmente. Não entrarei em detalhes aqui dos parâmetros internos do arquivo, mas sim como gerar as configurações a partir dele. No meu caso, como eu já tinha um OpenLDAP funcionando e estou fazendo upgrade, copiei o meu em produção, porém, se você é um novo usuário, poderá pegar um exemplo em /usr/share/ldap/slapd.conf
</p>

<p style="text-align: justify;">
  É bom fazer um backup do diretório /etc/ldap/slapd.d antes de executar os comandos.
</p>

<p style="text-align: justify;">
  mv /etc/ldap/slapd.d /etc/ldap/slapd.d.original
</p>

<p style="text-align: justify;">
  mkdir /etc/ldap/slapd.d
</p>

<p style="text-align: justify;">
  <p style="text-align: justify;">
    Bom, feito isso, basta gerar a config (o comando é executado de dentro de /etc/ldap):
  </p>
  
  <p style="text-align: justify;">
    slaptest -f slapd.conf -F slapd.d
  </p>
  
  <p style="text-align: justify;">
    chown -R openldap.openldap /etc/ldap
  </p>
  
  <p style="text-align: justify;">
    <p style="text-align: justify;">
      []&#8217;s
    </p>
    
    <p style="text-align: justify;">
    </p>
    
    <p>
    </p>