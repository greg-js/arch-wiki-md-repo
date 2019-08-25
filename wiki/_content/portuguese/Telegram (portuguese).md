**Status de tradução:** Esse artigo é uma tradução de [Telegram](/index.php/Telegram "Telegram"). Data da última tradução: 2019-07-27\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Telegram&diff=0&oldid=578091) na versão em inglês.

[Telegram](https://en.wikipedia.org/wiki/pt:Telegram_(aplicativo) é um serviço de mensagens instantâneas multiplataforma baseado em nuvem com criptografia ponto a ponto opcional. A criação de conta requer um número de telefone.

Os clientes oficiais são de código aberto, mas o código para versões recentes nem sempre é publicado imediatamente. O código do lado do servidor é proprietário.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Plugins de cliente de bate-papo](#Plugins_de_cliente_de_bate-papo)
    *   [1.2 Clientes gráficos](#Clientes_gráficos)
    *   [1.3 Clientes de linha de comando](#Clientes_de_linha_de_comando)
    *   [1.4 Clientes web](#Clientes_web)
*   [2 Dicas e truques](#Dicas_e_truques)
    *   [2.1 Recursos do Telegram sobre o Arch Linux](#Recursos_do_Telegram_sobre_o_Arch_Linux)
    *   [2.2 Contador de mensagens não lidas para o Telegram Desktop](#Contador_de_mensagens_não_lidas_para_o_Telegram_Desktop)

## Instalação

Você pode usar um dos seguintes métodos para usar o Telegram no Arch:

### Plugins de cliente de bate-papo

*   Ao usar os pacotes [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) ou [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/), uma conexão com o Telegram por meio de software de mensageria (gráficos ou de linha de comando) baseados em [libpurple](https://www.archlinux.org/packages/?name=libpurple) tal como [Pidgin](/index.php/Pidgin "Pidgin") é fornecida.
*   Aplicativos de mensageria que estão usando [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) tal como [empathy](https://www.archlinux.org/packages/?name=empathy) (o mensageiro padrão do [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)")) pode fazer uso do pacote [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), que fornece possibilidade de usar [libpurple](https://www.archlinux.org/packages/?name=libpurple) e, portanto, [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) para se conectar ao Telegram.
*   No ambiente [KDE](/index.php/KDE_(Portugu%C3%AAs) "KDE (Português)"), usar [telepathy-morse](https://www.archlinux.org/packages/?name=telepathy-morse) fornece a capacidade de conectar o mensageiro padrão ao Telegram.

### Clientes gráficos

O [aplicativo oficial](https://desktop.telegram.org/):

*   [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop), compilado pelo Arch Linux
*   [telegram-desktop-bin](https://aur.archlinux.org/packages/telegram-desktop-bin/), compilado pelo upstream
*   [telegram-desktop-systemqt-notoemoji](https://aur.archlinux.org/packages/telegram-desktop-systemqt-notoemoji/) Compilação experimental do Telegram Desktop usando o sistema Qt e emojis substituídos pelos de [Noto Color Emoji](https://github.com/googlei18n/noto-emoji).

**Dica:** Telegram usa Open Sans como a fonte padrão, o que fornece a dependência opcional [ttf-opensans](https://www.archlinux.org/packages/?name=ttf-opensans).

Clientes de terceiros:

*   [bettergram](https://aur.archlinux.org/packages/bettergram/)
*   [kepka-git](https://aur.archlinux.org/packages/kepka-git/)
*   [cutegram-git](https://aur.archlinux.org/packages/cutegram-git/)
*   [telegreat-git](https://aur.archlinux.org/packages/telegreat-git/)

### Clientes de linha de comando

*   [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/) fornece interface de linha de comando para conectar e usar o Telegram. Para mais informações sobre o programa, visite sua página no [Github](https://github.com/vysheng/tg).
*   [nctelegram-git](https://aur.archlinux.org/packages/nctelegram-git/) é uma interface de linha de comando para o Telegram baseado em [Ncurses](https://en.wikipedia.org/wiki/Ncurses "wikipedia:Ncurses") e precisa de [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/) para funcionar. Para mais informações sobre o programa, visite sua página no [Github](https://github.com/Nanoseb/ncTelegram).
*   [python-telegram-send](https://aur.archlinux.org/packages/python-telegram-send/) não é um cliente completo, mas é uma ferramenta de linha de comando para enviar diretamente mensagens ou arquivos via Telegram.

### Clientes web

*   O [Telegram Web](https://web.telegram.org) oficial.
*   [franz](https://aur.archlinux.org/packages/franz/) é um aplicativo web [código aberto](https://github.com/meetfranz/franz) que pode ser usado para interface web de vários software de mensageria instantânea como o [Telegram](https://en.wikipedia.org/wiki/pt:Telegram_(software) "wikipedia:pt:Telegram (software)"), [WhatsApp](https://en.wikipedia.org/wiki/pt:WhatsApp "wikipedia:pt:WhatsApp"), [Facebook](https://en.wikipedia.org/wiki/pt:Facebook "wikipedia:pt:Facebook") e mais.
*   [rambox-bin](https://aur.archlinux.org/packages/rambox-bin/) é uma alternativa ao Franz, também código aberto. Oferece todos os recursos de sua contraparte.
*   Use extensões do [Telegram Desktop](https://addons.mozilla.org/en-US/firefox/addon/telegram-desktop/) para o [Firefox](/index.php/Firefox "Firefox"), para conectar ao Telegram em seu navegador por meio da interface web.
*   Use o [aplicativo Telegram da Chrome Web Store](https://telegram.org/dl/webogram/chromeapp) para o [Chromium](/index.php/Chromium "Chromium"), para conectar ao Telegram em seu navegador por meio da interface web.

## Dicas e truques

### Recursos do Telegram sobre o Arch Linux

*   [Arch Linux](https://t.me/archlinuxgroup) - Grupo não oficial para discutir tudo sobre o Arch Linux.
*   [ArchWikiBot](https://t.me/archewikibot) - Bot inline para pesquisar por páginas do ArchWiki.
*   [Planet Arch Linux & News](https://t.me/planetarch) - Canal com atualizações recentes do Planet Arch e Latest News em um só lugar.
*   [Arch Linux: Recent package updates](https://t.me/archlinux_updates) - Canal com atualizações recentes de pacotes em repositórios do Arch Linux.
*   [Arch Linux News](https://t.me/archlinuxnews) - Canal com as últimas notícias do site do Arch *(não atualizado)*.
*   [Planet Arch](https://t.me/archplanet) - Canal com as últimas publicações do site do Planet Arch *(não atualizado)*.
*   [Archlinux.fr News](https://t.me/archlinuxfr) - Canal com as últimas publicações dos fóruns do Archlinux.fr e outras coisas sobre o Arch Linux.
*   [Archlinux.fr Chat](https://t.me/archlinux_FR) - Grupo não oficial para discutir tudo sobre o Arch Linux para usuários franceses.

### Contador de mensagens não lidas para o Telegram Desktop

Por padrão, somente o ícone na bandeja do sistema mostrará o número de mensagens não lidas. Se você quiser ter o ícone do aplicativo real para exibir também o contador de mensagens não lidas, poderá usar a integração do selo Unity, que também pode ser gerenciada pelo KDE e pelo GNOME. Para ativar a integração do Unity, você terá que instalar o [libunity](https://aur.archlinux.org/packages/libunity/) e iniciar o Telegram Desktop com a variável de ambiente `XDG_CURRENT_DESKTOP` configurada para `Unity`, por exemplo, copie o arquivo `.desktop` para `~/.local/share/applications/` e altere a linha `Exec` para iniciar o Telegram Desktop com o conjunto de variáveis de ambiente.