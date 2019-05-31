---
id: 134
title: 'PHP5 e MS SQL Server &#8211; Configurando Acesso via ODBC no Debian 5 &#8211; &#8220;Lenny&#8221;'
date: 2010-06-10T14:42:30-03:00
author: @rsveiras
layout: post
guid: http://www.rodrigoeiras.eti.br/?p=134
permalink: /2010/06/10/php5-e-ms-sql-server-configurando-acesso-via-odbc-no-debian-5-lenny/
aktt_notify_twitter:
  - 'yes'
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - Linux
tags:
  - debian
  - freetds
  - Linux
  - odbc
  - sqlserver
---
A partir da nova versão do Debian, já é possível configurar o acesso ao MS SQL Server sem a necessidade de compilar pacotes do PHP para tal, basta usar o &#8220;FreeTDS&#8221; que já está disponível no próprio repositório _apt_.

Para começar, vamos instalar o FreeTDS e esteja ciente de fazer todos os comandos como **root**:

> apt-get install tdsodbc unixodbc php5-odbc freetds-dev php5-sybase

Instalado os pacotes, vamos criar o arquivo de template DSN:

> vim /etc/freetds/tds.driver.template

Adicione o seguinte conteúdo ao arquivo:

> [TDS]  
> Description = FreeTDS MSSQL Driver for Linux Debian 5 &#8211; &#8220;Lenny&#8221;  
> Driver = /usr/lib/odbc/libtdsodbc.so  
> Setup = /usr/lib/odbc/libtdsS.so 

Feito o passo acima, vamos registrar o ODBC no sistema.

> odbcinst -i -d -f /etc/freetds/tds.driver.template

Agora, vamos registrar a base que será acessada pelo ODBC.  
Lembrando que, cada base necessita de um ODBC diferente, então, se você possuir mais de uma, siga repetindo os comandos.  
Crie o arquivo:

> vim /etc/freetds/tds.dsn.template

Com o seguinte conteúdo:

> <div id="_mcePaste">
>   [DSN]
> </div>
> 
> <div id="_mcePaste">
>   Description     = Teste de ODBC &#8211; FreeTDS
> </div>
> 
> <div id="_mcePaste">
>   Driver          = TDS
> </div>
> 
> <div id="_mcePaste">
>   Trace           = No
> </div>
> 
> <div id="_mcePaste">
>   Database        = EIRAS
> </div>
> 
> <div id="_mcePaste">
>   Server          = 192.168.100.50
> </div>
> 
> <div id="_mcePaste">
>   Port            = 1433
> </div>

<div id="_mcePaste">
  Lembre de mudar o nome &#8220;DSN&#8221; acima. Esse nome será usado na aplicação para identificar o ODBC. Geralmente, ele possui o mesmo nome da base de dados. (database)
</div>

<div>
  Ok, os arquivo estão prontos.
</div>

<div>
  Vamos registrar os ODB&#8217;s e DSN&#8217;s no Linux:
</div>

> <div>
>   odbcinst -i -d -f /etc/freetds/tds.driver.template
> </div>
> 
> <div>
>   odbcinst -i -s -f /etc/freetds/tds.dsn.template
> </div>

<div>
  Os ODBC&#8217;s são registrados para os usuários que os criam (no nosso caso, o root), mas no caso, iremos deixar o registro para uso do sistema, pois será usado pelo apache. Então, iremos copiar o conteúdo para o arquivo de acesso global.
</div>

> <div>
>   cat /root/.odbc.ini >> /etc/odbc.ini
> </div>

<div>
  A partir de agora, iremos fazer o apache reconhecer o ODBC que foi criado. Abra o arquivo abaixo e adicione a linha:
</div>

> <div>
>   vim  /etc/php5/apache2/php.ini
> </div>
> 
> <div>
>   <ul>
>     <li>
>       extension = odbc.so
>     </li>
>   </ul>
> </div>

<div>
  Reinicie o Apache:
</div>

> <div>
>   /etc/init.d/apache2 restart
> </div>

<div>
  Pronto, a partir de agora seu ODBC deverá funcionar via PHP. Para testar o acesso via console, faça o comando:
</div>

> <div>
>   isql -v DSN sa senha
> </div>

<div>
  []&#8217;s!
</div>