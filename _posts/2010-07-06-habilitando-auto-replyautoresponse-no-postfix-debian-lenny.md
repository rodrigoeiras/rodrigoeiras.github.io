---
id: 213
title: 'Habilitando Auto-Reply/Autoresponse no Postfix &#8211; Debian &#8220;Lenny&#8221;'
date: 2010-07-06T12:31:38-03:00
author: Rodrigo Eiras
permalink: /2010/07/06/habilitando-auto-replyautoresponse-no-postfix-debian-lenny/
categories:
  - Linux
  - Postfix
tags:
  - autoreply
  - autoresponse
  - Linux
  - mail
  - postfix
  - vacation
---
<p style="text-align: justify;">
O contador da empresa vai sair de férias.  
Sim, mas e daí?
</p>

<p style="text-align: justify;">
Pois bem, foi cogitado pelo meu coordenador se seria possível configurar uma resposta automática para o cara informando o seu período de férias a cada Email que chegasse. Pensei: &#8220;Deve precisar de banco de dados, plugins e um monte de parafernália para colocar isso para funcionar&#8221;. Então, resolvi pesquisar e o negócio é bem mais simples do que eu esperava.
</p>

<p style="text-align: justify;">
Primeiro, que pesquisando sobre um dos mais famosos, o &#8220;Vacation&#8221; encontrei bastante coisa, porém ele usa o procmail e em minha configuração eu utilizo o maildrop. Até achei alguns documentos sobre como usá-lo com maildrop, mas o negócio não seria automatizado e ficou um pouco gambiarra. Resolvi então pesquisar mais e foi quando achei o tal do &#8220;autoresponse&#8221;. Show!
</p>

<p style="text-align: justify;">
Ele interage diretamente com o Postfix e não é necessário qualquer configuração adicional para fazer funcionar, somente é necessário um requisito:

> Ter autenticação SASL funcionando.
</p>

Começando e sempre lembrando, o procedimento foi testado no Debian &#8220;Lenny&#8221;, mas provavelmente funcionará nas demais distribuições.

Faça o download da aplicação e descompacte em /usr/src  
<http://www.nefaria.com/scriptz/autoresponse-1.6.3.tar.gz>

> tar -xzvf autoresponse-1.6.3.tar.gz

Crie um usuário, o diretório padrão de operação e posteriormente configure as permissões do diretório do autoresponse conforme abaixo:

> useradd -d /var/spool/autoresponse -s /bin/false autoresponse
>
> mkdir -p /var/spool/autoresponse/log /var/spool/autoresponse/responses
>
> cp /usr/src/autoresponse/autoresponse /usr/local/sbin/
>
> chown -R autoresponse.autoresponse /var/spool/autoresponse
>
> chmod -R 0770 /var/spool/autoresponse

Criado o diretório, é necessário informar ao Postfix os passos a serem seguidos.  
Abra o arquivo master.cf e adicione abaixa da linha:

**smtp inet n &#8211; n &#8211; &#8211; smtpd**

> -o content_filter=autoresponder:dummy

Ou seja, a configuração acima ficará da seguinte forma:

> smtp inet n &#8211; n &#8211; &#8211; smtpd  
> -o content_filter=autoresponder:dummy

Adicione em seguida as seguintes linhas em **\# Other external delivery methods**

> autoresponder unix &#8211; n n &#8211; &#8211; pipe  
> flags=Fq user=autoresponse argv=/usr/local/sbin/autoresponse -s ${sender} -r ${recipient} -S ${sasl\_username} -C ${client\_address}

Salve o arquivo master.cf e saia do editor.

Abra agora o arquivo main.cf e adicione a seguinte linha:

> autoresponder\_destination\_recipient_limit = 1

Saia e salve.  
Em seguida, reinicie o postfix. **/etc/init.d/postfix restart**  
A configuração esta pronta no sistema, veja abaixo como ativar uma auto resposta.

**Ativando via Email**

Envie um email para **login+autoresponse@seudominio.com.br**  
Formate-o como quiser, inclusive e muito importa setar um assunto (subject). Por questões de segurança, é necessário que o email seja enviado do seu próprio email e autenticado via SASL.

Pronto, sua autoresposta esta configurada. Envie um Email de outro domínio ou de outra conta para seu endereço para testar.  
Para desativar a autoresposta, basta enviar um Email em branco da mesma forma, incluindo o subject.

**Comandos via Shell/Console**

&#8211; Para desabilitar a autoresposta:

autoresponse -d usuario@seudominio.com.br

&#8211; Para habilitar a autoresposta:

autoresponse -E usuario@seudominio.com.br

&#8211; Para deletar a autoresposta:

autoresponse -D usuario@seudominio.com.br

�? isso, aqui no nosso ambiente tem funcionado perfeitamente.  
Sugiro que vocês criem uma seção no site de vocês, junto as configurações de POP3/IMAP/SMTP uma seção explicando o funcionamento do recurso.

[]&#8217;s!
