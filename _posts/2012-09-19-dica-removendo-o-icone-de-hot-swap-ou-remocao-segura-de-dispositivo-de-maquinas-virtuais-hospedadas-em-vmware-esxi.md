---
id: 283
title: 'Dica: Removendo o ícone de &#8220;Hot Swap&#8221; ou &#8220;Remoção Segura de Dispositivo&#8221; de máquinas virtuais hospedadas em VMware ESXi'
date: 2012-09-19T12:40:16-03:00
author: @rsveiras
layout: post
guid: http://www.rodrigoeiras.eti.br/?p=283
permalink: /2012/09/19/dica-removendo-o-icone-de-hot-swap-ou-remocao-segura-de-dispositivo-de-maquinas-virtuais-hospedadas-em-vmware-esxi/
aktt_notify_twitter:
  - 'yes'
aktt_tweeted:
  - "1"
categories:
  - Redes / Sistemas
  - Virtualização
  - VMware ESXi
tags:
  - esxi
  - hotswap
  - safe remove
  - vmware
---
<p style="text-align: justify;">
  Essa dica vai para você que acabou de instalar o VMware ESXi 4 ou 5 e quando foi criar uma máquina virtual windows, percebeu que apareceu um ícone na barra de tarefas, aquele mesmo ícone de remover pendrive com segurança. O Windows entende placas de redes e dispositivos SCSI provenientes do VMware como &#8220;hot swappable&#8221; e com isso, apresenta o ícone, que nesses casos, é totalmente inútil.
</p>

&nbsp;

<div class="mceMediaCredit mceTemp mceIEcenter" draggable="">
  <span class="media-credit-mce aligncenter" id="5" style="width: 222px;"><span class="media-credit-dt"><a href="http://www.rodrigoeiras.eti.br/2012/09/19/dica-removendo-o-icone-de-hot-swap-ou-remocao-segura-de-dispositivo-de-maquinas-virtuais-hospedadas-em-vmware-esxi/hotswap/" rel="attachment wp-att-284"><img class="size-full wp-image-284" title="hotswap" alt="" src="https://i0.wp.com/www.rodrigoeiras.eti.br/wp-content/uploads/2012/09/hotswap.jpg?resize=212%2C178" width="212" height="178" data-recalc-dims="1" /></a></span><span class="media-credit-dd">eiras | rodrigoeiras.eti.br</span></span>
</div>

&nbsp;

Para remover o ícone, faça o procedimento através do vSphere Client.

1) Conecte pelo vSphere Client ao Hypervisor ESXi.

2) Desligue a máquina virtual windows.

3) Clique com o botão direito na máquina virtual e posteriormente em &#8220;Edit Settings&#8221;

4) Clique na aba &#8220;Options&#8221;

5) Clique em &#8220;General&#8221; > &#8220;Configuration Parameters&#8221; > &#8220;Add Row&#8221; (Essa instrução irá abrir a possibilidade de você adicionar uma nova linha de parâmetro de configuração.

6) Insira uma nova linha com o seguinte nome e valor (um em cada coluna): _devices.hotplug_ = _false_

7) Inicie novamente a máquina virtual e o ícone terá desaparecido.

Espero que tenha ajudado.

[]&#8217;s