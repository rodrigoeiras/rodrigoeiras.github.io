---
published: true
---
## Aprenda a habilitar cedilha no Linux Mint. Apesar de parecer simples, a coisa não é bem documentada.

Você já deve ter reparado que é bem chato utilizar um teclado americano no Linux Mint caso seja necessário utilizar cedilha. Na verdade, o teclado e o layout existem no linux mint porém o módulo de cedilla vem desabilitado por padrão. Sim, thats sucks.

Para resolver isso, é necessário ativar o módulo no GTK.

Meu Linux Mint é o 19, mas deve funcionar nos demais.

Comece editando os arquivos abaixo:

**1)**

> sudo vim /usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules.cache

> sudo vim /usr/lib/x86_64-linux-gnu/gtk-2.0/2.10.0/immodules.cache

Nos arquivos acima, procure por cedilla e Cedilla e adiciona ao fim da linha :en
Exemplo abaixo:

_"cedilla" "Cedilla" "gtk30" "/usr/share/locale" "az:ca:co:fr:gv:oc:pt:sq:tr:wa:en"_

Faça isso nos dois arquivos acima, no GTK 2 e no GTK 3.

**2)**

Altere o arquivo Compose com o seguinte comando:

> sudo sed -i /usr/share/X11/locale/en_US.UTF-8/Compose -e 's/ć/ç/g' -e 's/Ć/Ç/g'

**3)**

Por último, adicione os módulos no arquivo /etc/environment para que possam ser carregados ao inicilizar.

> GTK_IM_MODULE=cedilla

> QT_IM_MODULE=cedilla


Feito isso, basta salvar e reiniciar e tudo estará como deve ser.
