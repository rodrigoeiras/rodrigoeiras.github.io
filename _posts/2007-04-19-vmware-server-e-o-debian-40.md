---
id: 6
title: VMware Server e o Debian 4.0
date: 2007-04-19T01:13:00-03:00
author: Rodrigo Eiras
layout: post
guid: http://www.rodrigoeiras.com/?p=6
permalink: /2007/04/19/vmware-server-e-o-debian-40/
aktt_notify_twitter:
  - 'yes'
categories:
  - Linux
  - Redes / Sistemas
tags:
  - debian
  - etch
  - Linux
  - opensource
  - vmware
---
VMware é um sistema de virtualização de servidores. Virtualização? Sim, você instala um sistema operacional normalmente em sua máquina (um linux né :D) e de dentro desta instalação você consegue criar (virtualizar) outros sistemas operacionais distintos. �? o que chamos de &#8220;Máquinas Virtuais&#8221;. O melhor de tudo, a mantenedora do VMware disponibilizou recentemente uma versão gratuita do seu programa, ou seja, um VMware server de graça!

Confesso que quando escutei falar disso um tempo atrás, não levei fé. Pensava que deveria ser muito instável e não valeria a pena. Pois bem, quebrei a cara. 🙂

Esses dias instalei um Debian 4 no meu trabalho. E, dentro dos planos, Eu deveria mudar dois sistemas já existentes para um máquina só, uma máquina melhor. O problema é que as duas máquinas, realizam aplicações semelhantes ao ponto de ter que haver alguns serviços exclusivos, que impossibilita a utilização de uma máquina somente para os dois serviços.

Pensando por esse lado, resolvi experimentar o tal do VMware. Instalei o Debian 4.0 e logo após comecei a configurar o VMware Server. Um programa muito bem organizado, com instalador excelente que adequa todos os arquivos do programa em seus devidos diretórios e ainda cria um arquivo de inicialização junto ao sistema, coisa que é raro hoje em dia em sistema Linux (Geralmente você tem que criar o script e dar permissões).

Bom, antes de falar mais, só uma observação: o VMware exige muita memória e espaço em disco. Então, queira ter isso de sobra. Usei uma máquina com 2 GB de memória RAM e 160 GB de HD, dedicado somente as Máquinas Virtuais.

Bom, por início, o VMware apresenta alguns requisitos para instalação: �? necessário o Kernel-Source, o Kernel-Headers e os Dev-Builds para a criação dos módulos das Máquinas Virtuais, e a única notícia ruim é essa. Pois, no meu caso, tive que fazer uma compilação do Kernel. (Essa compilação é para uso somente do VMware, não é usado para nenhum sistema real)

�? necessário também (embora, acho que não é obrigatório) a instalação de um ambiente gráfico no Linux para o uso do VMware Server Console. Utilizo o KDE, então segue os comandos abaixo para a instalação do mesmo:

  * apt-get install x-window-system-core
  * apt-get install kdm
  * apt-get install kde
  * apt-get install kde-i18n-ptbr

Segue os comandos para a instalação dos pacotes necessários no Debian:

  * apt-get install linux-source-2.6.18
  * apt-get install kernel-package
  * apt-get install build-essential

Pronto, instalados os pacotes, agora vamos prepará-los:

  * cd /usr/src
  * tar -xjvf linux-source-2.6.18.tar.bz2
  * ln -s linux-source-2.6.18 linux

Nos comandos acima, será descompactado o fonte do kernel e criado um link simbólico para /usr/src/linux

De posse disso, vamos agora compilar o kernel. Como somente precisamos do Kernel compilado para uso com o VMware, vamos copiar as configuração atuais, para não ter que entrar no menuconfig.

  * cp /boot/config-2.6.18-4-686 /usr/src/linux/.config

Atenção, o comando acima é para quem estiver usando máquina com processador Intel. Se você usa alguma máquina AMD, o nome do config do kernel geralmente é config-2.6.18-4-k7 (atenção a isso)

Segue os comando de compilação:

  * cd /usr/src/linux
  * make-kpkg &#8211;append-to-version &#8220;-4-686&#8221; &#8211;initrd &#8211;us &#8211;uc kernel_image

Atenção ao comando acima. Ele irá compilar o Kernel 2.6.18 e irá adicionar a string -4-686 ao nome da imagem. ISSO �? VITAL, ou o VMware irá recusar sua compilação. O comando irá gerar os headers e uma imagem comprimida do seu kernel. Se você usa processador AMD, altera o version para &#8220;-4-k7&#8221;, na verdade altere para a mesma forma que esta sua imagem do sistema. O meu Kernel é o kernel-image-2.6.18-4-686, logo por isso adicionei &#8220;-4-686&#8221;. Para conferir a versão do seu Kernel, entre no diretório /boot com o comando &#8220;ls&#8221; e veja a sequencia do arquivo vmlinuz. (vmlinuz-2.6.18-4-686), note &#8220;2.6.18-4-686&#8221;.

A compilação irá demorar um pouco. 🙂

Terminado isso, vamos a instalação do VMware. �? bem simples, e se você seguiu os comandos acima, basta ir seguindo as instruções na tela e confirmando. Para baixar o VMware é necessário entrar no site e fazer um registro para receber o serial number. [http://www.vmware.com](http://www.vmware.com/)

Procure em download por VMware Server (OpenSource)

Faça o download e descompacte o arquivo.

  * tar -xzvf vmware-xxxx-.tar.gz

Entre no diretorio:

  * cd vmware-server-distrib

Execute o script de instalação:

  * ./vmware-install.pl

Basta seguir os passos da instalação.

[]&#8217;s

Rodrigo Eiras