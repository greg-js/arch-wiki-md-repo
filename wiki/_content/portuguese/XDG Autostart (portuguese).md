A [especificação XDG Autostart](https://specifications.freedesktop.org/autostart-spec/autostart-spec-latest.html) define um padrão para [iniciar automaticamente](/index.php/Autostarting "Autostarting") [entradas desktop](/index.php/Desktop_entries "Desktop entries") comuns na inicialização de um [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop") e montagem de mídia removível, colocando-os em [#Diretórios](#Diret.C3.B3rios) específicos.

## Pré-requisitos

Você precisa usar um [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop") que oferece suporte a ela ou uma implementação dedicada, como [dex](https://www.archlinux.org/packages/?name=dex), [dapper](https://aur.archlinux.org/packages/dapper/) ou [fbautostart](https://aur.archlinux.org/packages/fbautostart/).

## Diretórios

Um ambiente de desktop compatível com XDG vai inciar automaticamente [entradas desktop](/index.php/Desktop_entries "Desktop entries") localizadas nos seguintes diretórios:

*   Todo o sistema: `$XDG_CONFIG_DIRS/autostart/` (`/etc/xdg/autostart/` por padrão)

*   [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") também inicia arquivos localizados em `/usr/share/gnome/autostart/`

*   Específico do usuário: `$XDG_CONFIG_HOME/autostart/` (`~/.config/autostart/` por padrão)

Os usuários podem sobrescrever [entradas desktop](/index.php/Desktop_entries "Desktop entries") destinada a todo sistema, copiando-as para o diretório específico do usuário.

Para mais detalhes, consulte [a especificação](http://standards.freedesktop.org/autostart-spec/autostart-spec-latest.html).