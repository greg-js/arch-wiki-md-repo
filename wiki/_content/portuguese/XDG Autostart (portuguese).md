**Status de tradução:** Esse artigo é uma tradução de [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart"). Data da última tradução: 2018-10-01\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=XDG_Autostart&diff=0&oldid=545496) na versão em inglês.

A [especificação XDG Autostart](https://specifications.freedesktop.org/autostart-spec/autostart-spec-latest.html) define um método para [inicialização automática](/index.php/Inicializa%C3%A7%C3%A3o_autom%C3%A1tica "Inicialização automática") de [entradas de desktop](/index.php/Entradas_de_desktop "Entradas de desktop") comuns na inicialização de um [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop") e montagem de mídia removível, colocando-os em [#Diretórios](#Diretórios) específicos.

## Pré-requisitos

Você precisa usar um [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop") que oferece suporte a ela ou uma implementação dedicada, como [dex](https://www.archlinux.org/packages/?name=dex), [dapper](https://aur.archlinux.org/packages/dapper/) ou [fbautostart](https://aur.archlinux.org/packages/fbautostart/).

## Diretórios

Os diretórios Autostart na ordem de preferência são:

*   específico por usuário: `$XDG_CONFIG_HOME/autostart` (`~/.config/autostart` por padrão)
*   para todo o sistema: `$XDG_CONFIG_DIRS/autostart` (`/etc/xdg/autostart` por padrão)[[1]](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html#referencing)

[Entradas de desktop](/index.php/Entradas_de_desktop "Entradas de desktop") do sistema podem ser sobrescritos por entradas específicas por usuário com o nome de arquivo.

Para desabilitar uma entrada do sistema, crie uma entrada para sobrescrever contendo `Hidden=true`.

Para mais detalhes, leia [a especificação](https://specifications.freedesktop.org/autostart-spec/autostart-spec-latest.html).