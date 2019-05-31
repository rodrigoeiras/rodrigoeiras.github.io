---
id: 337
title: 'Dica: Symantec Backup Exec 2010 R3 &#8211; Como fazer backup`s incrementais com sucesso de ambientes Linux/Unix'
date: 2012-12-06T13:36:19-03:00
author: @rsveiras
layout: post
guid: http://www.rodrigoeiras.eti.br/?p=337
permalink: /2012/12/06/dica-symantec-backup-exec-2010-r3-como-fazer-backups-incrementais-com-sucesso-de-ambientes-linuxunix/
categories:
  - Backup
  - Linux
tags:
  - backup
  - incremental
  - symantec
---
<p style="text-align: justify;">
  Essa dica vai para quem esta utilizando a ferramenta Backup Exec da Symantec para realizar backups automatizados.
</p>

<p style="text-align: justify;">
  Em se tratando de servidores Windows, não importa muito o procedimento, pois o agente remoto de backup funciona exatamente como é esperado nele, da forma que vou sugerir aqui ou da default.
</p>

<p style="text-align: justify;">
  Já no Linux, o agente RALUS, não funciona bem com o modo default de criação de tarefas de backup`s incrementais, ou seja, usando modo &#8220;archive bit&#8221;. Para contornar esse problema, pode-se utilizar tarefas com o modo de alteração por tempo, que o sistema usará para identificar arquivos modificados, a data de alteração do mesmo.
</p>

<p style="text-align: justify;">
  Para facilitar, crie políticas de backup separadas por plataformas ou então por servidores isolados, desta forma, você conseguirá customizar cada ambiente de acordo com sua particularidade.
</p>

<p style="text-align: justify;">
  <p style="text-align: justify;">
    É isso.
  </p>
  
  <p style="text-align: justify;">
    Abs!
  </p>
  
  <p style="text-align: justify;">
    <p>
    </p>