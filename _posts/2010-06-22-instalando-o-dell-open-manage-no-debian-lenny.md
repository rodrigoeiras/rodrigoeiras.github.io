---
id: 167
title: 'Instalando o Dell Open Manage no Debian &#8220;Lenny&#8221;'
date: 2010-06-22T14:52:04-03:00
author: Rodrigo Eiras
permalink: /2010/06/22/instalando-o-dell-open-manage-no-debian-lenny/
categories:
  - Dell
  - Linux
  - Redes / Sistemas
tags:
  - debian
  - dell
  - lenny
  - Linux
  - openmanage
---
Quem trabalha com servidores Dell já reparou que o _Open Manage Server Administrator_ somente está disponível para os ambientes homologados pela Dell, no caso, o Microsoft Windows Server, o Novell SUSE Enterprise Linux e o Red Hat Enterprise Linux.

Pois bem, mas eu trabalho com Debian, como eu faço? �? possível?  
Sim, perfeitamente possível. Abaixo, você poderá ver alguns passos simples para poder colocá-lo funcionando em seu servidor.

Suponho que você já esteja com seu Debian 5 &#8220;Lenny&#8221; instalado e funcionando.  
A versão que iremos instalar aqui é a 6.0.1, compatível com o Debian 5, de acordo com estes repositórios.

> ftp://ftp.sara.nl/pub/sara-omsa/dists/dell6/sara/binary-i386/  
> ftp://ftp.sara.nl/pub/sara-omsa/dists/dell6/sara/binary-amd64/

**1)** Configurando o apt-get  
Para não termos problemas com os hash&#8217;s do arquivos, baixe as chaves.

> wget http://ftp.sara.nl/debian_sara.asc  
> apt-key add debian_sara.asc

Em seguida, adicione as linhas em /etc/apt/sources.list

> deb ftp://ftp.sara.nl/pub/sara-omsa dell6 sara

Agora, faça um update do repositório e instale o pacote Dell OMSA.

> apt-get update  
> apt-get install dellomsa

Pois bem, agora vem o único detalhe para colocá-lo funcionando e antes disso, sugiro reiniciar o seu servidor antes de continuar, no meu caso, fez diferença.

**2)** Se você utiliza o Lenny em compilação 32bits, não tem mistério, basta pular para a parte &#8220;3&#8221; e iniciar os serviços.

Caso você utiliza a compilação 64bits, como foi o meu caso, é necessário fazer um pequeno ajuste na distribuição, pois o sistema da Dell utiliza algumas bibliotecas de 32bits que não ficam disponíveis na versão 64bits.  
Será necessário fazer o download manualmente destas bibliotecas e copiá-la para os diretórios específicos.  
Segue:

> [libpam-modules](http://packages.debian.org/lenny/i386/libpam-modules/download)  
> [libsepol1](http://packages.debian.org/lenny/i386/libsepol1/download)  
> [libselinux1](http://packages.debian.org/lenny/i386/libselinux1/download)

Lembrando que os links acima, são da versão 32bits &#8220;stable&#8221; do Lenny. Se você usar qualquer outra versão, se atente a isso.  
Faça o download dos arquivos acima dentro do diretório /tmp

Após o download, é necessário **EXTRAIR** o conteúdo dos pacotes. (Importante: Não instale os pacotes ou você poderá danificar sua instalação do Debian.)  
Utilize os comandos abaixo:

> dpkg -x libpam-modules\_1.0.1-5+lenny1\_i386.deb /tmp  
> dpkg -x libselinux1\_2.0.65-5\_i386.deb /tmp  
> dpkg -x libsepol1\_2.0.30-2\_i386.deb /tmp

Feito isso, copie os seguintes arquivos para /lib32/security  
(Se não houver o diretório, crie-o)

> cp -R libsepol.so.1 /lib32/security  
> cp -R libselinux.so.1 /lib32/security  
> cp -R pam_unix.so /lib32/security  
> cp -R pam_nologin.so /lib32/security

Pronto, esta quase.  
Agora, abra o arquivo /etc/pam.d/omauth e veja se o conteúdo esta conforme abaixo:

> auth required /lib32/security/pam_unix.so nullok  
> auth required /lib32/security/pam_nologin.so  
> account required /lib32/security/pam_unix.so nullok

Se estiver tudo ok, saia do arquivo e faça o comando _ldconfig_

**3)** Iniciando os serviços:

> modprobe mptctl (Módulo para SAS/5i Storage Controller)
>
> /etc/init.d/instsvcdrv restart  
> /etc/init.d/dsm\_om\_connsvc restart  
> /etc/init.d/dsm\_om\_shrsvc restart  
> /etc/init.d/dsm\_sa\_ipmi

Se tudo ocorreu corretamente na sua instalação do Open Manage, acesse da seguinte forma:  
**https://SEU_IP:1311/**

Pronto, acesse com o usuário _root_ e a devida _senha_ e veja as configurações do seu servidor.  
[]&#8217;s!

[media-credit id=5 align=&#8221;aligncenter&#8221; width=&#8221;468&#8243;]<a href="http://www.rodrigoeiras.eti.br/2010/06/22/instalando-o-dell-open-manage-no-debian-lenny/dell/" rel="attachment wp-att-173"><img src="https://i2.wp.com/www.rodrigoeiras.eti.br/wp-content/uploads/2010/06/dell.jpg?resize=468%2C304" alt="" title="dell" width="468" height="304" class="size-full wp-image-173" srcset="https://i2.wp.com/www.rodrigoeiras.eti.br/wp-content/uploads/2010/06/dell.jpg?w=468 468w, https://i2.wp.com/www.rodrigoeiras.eti.br/wp-content/uploads/2010/06/dell.jpg?resize=300%2C194 300w" sizes="(max-width: 468px) 100vw, 468px" data-recalc-dims="1" /></a>[/media-credit]
