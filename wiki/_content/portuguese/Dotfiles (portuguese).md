**Status de tradução:** Esse artigo é uma tradução de [Dotfiles](/index.php/Dotfiles "Dotfiles"). Data da última tradução: 2019-10-09\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Dotfiles&diff=0&oldid=581367) na versão em inglês.

Artigos relacionados

*   [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support")
*   [X resources](/index.php/X_resources "X resources")

A configuração de aplicativos específica do usuário é tradicionalmente armazenada nos chamados [*dotfiles*](https://en.wikipedia.org/wiki/dotfile ou [uma ferramenta dedicada](#Ferramentas)) . Além de explicar como gerenciar seus dotfiles, este artigo também contém [uma lista de repositórios de dotfiles](#Repositórios_de_usuários) dos usuários do Arch Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Rastreando dotfiles diretamente com Git](#Rastreando_dotfiles_diretamente_com_Git)
*   [2 Configuração específica por host](#Configuração_específica_por_host)
    *   [2.1 Ferramentas](#Ferramentas)
    *   [2.2 Ferramentas interfaceando Git](#Ferramentas_interfaceando_Git)
*   [3 Repositórios de usuários](#Repositórios_de_usuários)
*   [4 Veja também](#Veja_também)

## Rastreando dotfiles diretamente com Git

O benefício de rastrear dotfiles diretamente com o Git é que ele requer apenas [Git](/index.php/Git "Git") e não envolve links simbólicos. A desvantagem é que [configuração específica por cada host](#Configuração_específica_por_host) geralmente requer a mesclagem de alterações em vários [ramos](/index.php/Git#Branching "Git") (*branches*).

A maneira mais simples de conseguir essa abordagem é inicializar um repositório [Git](/index.php/Git "Git") diretamente em seu diretório inicial e ignorar todos os arquivos por padrão com um padrão de [gitignore(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitignore.5) de `*`. Este método, no entanto, vem com duas desvantagens: ele pode se tornar confuso quando você tiver outros repositórios Git em seu diretório inicial (por exemplo, se você esquecer de inicializar um repositório que você subitamente opera em seu repositório dotfile) e você não poderá mais ver facilmente quais arquivos o diretório atual não é rastreado (porque eles são ignorados).

Um método alternativo sem essas desvantagens é o "método repository seco e alias" popularizado por [este comentário no Hacker News](https://news.ycombinator.com/item?id=11070797), que apenas usa três comandos para configurar:

```
$ git init --bare ~/.dotfiles
$ alias config='/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
$ config config status.showUntrackedFiles no

```

Você pode então gerenciar seus dotfiles com o [alias](/index.php/Alias "Alias") criado.

**Dica:** Para evitar fazer commit acidental de informações confidenciais, veja [Git#Filtering confidential information](/index.php/Git#Filtering_confidential_information "Git").

## Configuração específica por host

Um problema comum com a sincronização de arquivos de pontos em várias máquinas é a configuração específica para cada host.

Com [Git](/index.php/Git "Git") isso pode ser resolvido mantendo um ramo *master* para toda a configuração compartilhada, enquanto cada máquina individual possui um ramo específico da máquina com check-out. A configuração específica por host pode aplicada para um ramo específico da máquina; Quando a configuração compartilhada é modificada no ramo *master*, os ramos por máquina precisam ser *rebased* na parte superior do *master* atualizado.

Em scripts de configuração como [arquivos de configuração do shell](/index.php/Shell_de_linha_de_comando "Shell de linha de comando"), a lógica condicional pode ser usada. Por exemplo, scripts [Bash](/index.php/Bash "Bash") (por exemplo, `.bashrc`) podem aplicar configurações diferentes dependendo do nome da máquina (ou tipo, variável personalizada, etc.):

```
if [[ "$(hostname)" == "archlaptop" ]]; then
    # comandos específicos de laptop aqui
else
    # comandos de máquina desktop ou servidor
fi

```

Similarmente, também podem ser alcançados com [.Xresources](/index.php/.Xresources ".Xresources").[[1]](https://jnrowe.github.io/articles/tips/Sharing_Xresources_between_systems.html)

Se você achar que fazer *rebase* de ramos do Git é trabalhoso demais, você pode querer usar uma [ferramenta](#Ferramentas) que possui suporte a *agrupamento de arquivos*, ou se uma flexibilidade ainda maior é desejada, uma ferramenta que faz *processamento*.

### Ferramentas

	Agrupamento de arquivos

	Como arquivos de configuração podem ser agrupados para grupos de configuração (também chamados de perfis ou pacotes).

	Processamento

	Algumas ferramentas processam arquivos de configuração para permitir que eles sejam personalizados dependendo do host.

| Nome | Pacote | Escrito em | Agrupamento de arquivos | Processamento |
| [dot-templater](https://github.com/kesslern/dot-templater) | [dot-templater-git](https://aur.archlinux.org/packages/dot-templater-git/) | Rust | baseado em diretórios | sintaxe personalizada |
| [dotdrop](https://deadc0de.re/dotdrop/) | [dotdrop](https://aur.archlinux.org/packages/dotdrop/) | Python | arquivo de configuração | Jinja2 |
| [dotfiles](https://github.com/jbernard/dotfiles) | [dotfiles](https://aur.archlinux.org/packages/dotfiles/) | Python | [Não](https://github.com/jbernard/dotfiles/pull/24) | Não |
| [Dots](https://github.com/EvanPurkhiser/dots) | [dots-manager](https://aur.archlinux.org/packages/dots-manager/) | Python | baseado em diretórios | pontos de acréscimos personalizados |
| [chezmoi](https://github.com/twpayne/chezmoi) | [chezmoi](https://www.archlinux.org/packages/?name=chezmoi) | Go | baseado em diretórios | modelos em Go |
| [GNU Stow](https://www.gnu.org/software/stow/) | [stow](https://www.archlinux.org/packages/?name=stow) | Perl | baseado em diretórios[[2]](http://brandon.invergo.net/news/2012-05-26-using-gnu-stow-to-manage-your-dotfiles.html) | Não |
| [Mackup](https://github.com/lra/mackup) | [mackup](https://aur.archlinux.org/packages/mackup/) | Python | automático por aplicativo | Não |
| [mir.qualia](https://github.com/darkfeline/mir.qualia) | [mir.qualia](https://aur.archlinux.org/packages/mir.qualia/) | Python | Não | blocos personalizados |
| [rcm](https://github.com/thoughtbot/rcm) | [rcm](https://aur.archlinux.org/packages/rcm/) | Perl | baseado em diretórios (por host ou tag) | Não |

### Ferramentas interfaceando Git

Se você não estiver confortável com o [Git](/index.php/Git "Git"), você pode querer usar uma dessas ferramentas, que abstraem o sistema de controle de versão (mais ou menos).

| Nome | Pacote | Escrito em | Agrupamento de arquivos | Processamento |
| [dotgit](https://github.com/kobus-v-schoor/dotgit) | [dotgit](https://aur.archlinux.org/packages/dotgit/) | Bash | baseado em nome de arquivo | Não |
| [homeshick](https://github.com/andsens/homeshick) | [homeshick-git](https://aur.archlinux.org/packages/homeshick-git/) | Bash | direcionado a repositório | Não |
| [homesick](https://github.com/technicalpickles/homesick) | [homesick](https://aur.archlinux.org/packages/homesick/) | Ruby | direcionado a repositório | Não |
| [Pearl](https://github.com/pearl-core/pearl) | [pearl-git](https://aur.archlinux.org/packages/pearl-git/) | Bash | direcionado a repositório | Não |
| [vcsh](https://github.com/RichiH/vcsh) | [vcsh](https://aur.archlinux.org/packages/vcsh/) | Shell | direcionado a repositório | Não |
| [yadm](https://thelocehiliosan.github.io/yadm/) | [yadm-git](https://aur.archlinux.org/packages/yadm-git/) | Shell | baseado em nome de arquivo
(por classe, SO, hostname & usuário) [[3]](https://thelocehiliosan.github.io/yadm/docs/alternates) | Jinja2
(opcional)[[4]](https://thelocehiliosan.github.io/yadm/docs/alternates#jinja-templates) |

1.  Possui suporte a criptografia de arquivos confidenciais com [GPG](/index.php/GPG "GPG").[[5]](https://thelocehiliosan.github.io/yadm/docs/encryption)

## Repositórios de usuários

| Autor | Shell
(Estrutura
de shell) | WM / DE | Editor | Terminal | Multiplexador | Áudio | Monitor | E-mail | IRC |
| [alfunx](https://github.com/alfunx/.dotfiles) | zsh | awesome | vim | kitty | tmux | ncmpcpp/mpd | htop/lain | thunderbird |
| [peterzuger](https://gitlab.com/peterzuger/dotfiles) | zsh | i3-gaps | emacs | rxvt-unicode | screen | moc | htop |
| [Ambrevar](https://gitlab.com/Ambrevar/dotfiles) | Eshell | EXWM | Emacs | Emacs (Eshell) | Emacs TRAMP + dtach | EMMS | conky/dzen | mu4e | Circe |
| [awal](https://github.com/awalGarg/dotfiles) | fish | i3 | vim | st | tmux | i3status | The Lounge |
| [ayekat](https://github.com/ayekat/dotfiles) | zsh | karuiwm | vim | rxvt-unicode | tmux | ncmpcpp/mpd | karuibar | mutt | irssi |
| [bamos](https://github.com/bamos/dotfiles) | zsh | i3/xmonad | vim/emacs | rxvt-unicode | tmux | mpv/cmus | conky/xmobar | mutt | ERC |
| [brisbin33](https://github.com/pbrisbin/dotfiles) | [zsh](https://github.com/pbrisbin/oh-my-zsh) | [xmonad](https://github.com/pbrisbin/xmonad-config) | [vim](https://github.com/pbrisbin/vim-config) | rxvt-unicode | screen | dzen | [mutt](https://github.com/pbrisbin/mutt-config) | [irssi](https://github.com/pbrisbin/irssi-config) |
| [BVollmerhaus](https://gitlab.com/BVollmerhaus/dotfiles) | [fish](https://gitlab.com/BVollmerhaus/dotfiles/tree/master/config/fish-custom) | [i3-gaps](https://gitlab.com/BVollmerhaus/dotfiles/blob/master/config/i3/config) | [kakoune](https://gitlab.com/BVollmerhaus/dotfiles/blob/master/config/kak/kakrc) | rxvt-unicode | [polybar](https://gitlab.com/BVollmerhaus/dotfiles/blob/master/config/polybar/config) | thunderbird |
| [cinelli](https://github.com/cinelli/dotfiles) | zsh | dwm | vim | termite-git | pianobar | htop | mutt-kz | weechat |
| [dikiaap](https://github.com/dikiaap/dotfiles) | zsh | i3-gaps | neovim | kitty | i3blocks |
| [Earnestly](https://github.com/Earnestly/dotfiles) | zsh | i3/orbment | vim/emacs | termite | tmux | mpd | conky | mutt | weechat |
| [ErikBjare](https://github.com/ErikBjare/dotfiles) | zsh | xmonad/xfce4 | vim | terminator | tmux | xfce4-panel | weechat |
| [falconindy](https://github.com/falconindy/dotfiles) | bash | i3 | vim | rxvt-unicode | ncmpcpp | conky | mutt |
| [graysky](https://github.com/graysky2/configs/tree/master/dotfiles) | zsh | xfce4 | vim | terminal | ncmpcpp | personalizado | thunderbird |
| [hugdru](https://github.com/hugdru/dotfiles) | zsh | awesome | neovim | rxvt-unicode | tmux | thunderbird | weechat |
| [insanum](https://github.com/insanum/dotfiles) | bash | herbstluftwm | vim | evilvte | tmux | dzen | mutt-kz |
| [jasonwryan](https://bitbucket.org/jasonwryan/shiv/src) | bash/zsh | dwm | vim | rxvt-unicode | tmux | ncmpcpp | personalizado | mutt | irssi |
| [jdevlieghere](https://github.com/JDevlieghere/dotfiles/) | zsh | xmonad | vim | terminal | tmux | htop | mutt | weechat |
| [jelly](https://github.com/jelly/Dotfiles) | zsh | i3 | vim | termite | tmux | ncmpcpp | mutt-kz-git | weechat |
| [Jorengarenar](https://github.com/Jorengarenar/dotfiles) | bash | i3 | vim | xterm | mpv | i3blocks | aerc | weechat |
| [maximbaz](https://github.com/maximbaz/dotfiles) | zsh | i3-gaps | neovim | alacritty | tmux | py3status | thunderbird |
| [mehalter](https://gitlab.com/mehalter/dotfiles) | zsh | i3-gaps | neovim | termite | tmux | gpymusic | i3blocks, gotop | neomutt | weechat |
| [meskarune](https://github.com/meskarune/.dotfiles) | bash | herbstluftwm | vim | rxvt-unicode | screen | conky | weechat |
| [neersighted](https://github.com/neersighted/dotfiles) | fish | i3 | neovim | alacritty | tmux | ncmpcpp |
| [oibind](https://github.com/oibind/dotfiles) | fish | awesome | neovim | termite | htop-vim | weechat |
| [OK100](https://github.com/ok100/configs) | bash | dwm | vim | rxvt-unicode | cmus | conky, dzen | mutt | weechat |
| [pablox-cl](https://github.com/pablox-cl/dotfiles) | zsh (zplug) | gnome3 | neovim | kitty |
| [reisub0](https://github.com/reisub0/dot) | fish | qtile | neovim | kitty | mpd | conky |
| [sistematico](https://github.com/sistematico/majestic) | zsh/fish/bash | [i3-gaps](https://github.com/Airblader/i3) | vim/nano | termite | tmux | ncmpcpp | polybar | mutt | weechat |
| [sitilge](https://git.sitilge.id.lv/sitilge/dotfiles) | zsh | awesome | neovim | termite | thunderbird |
| [swalladge](https://github.com/swalladge/dotfiles) | zsh/bash | i3 | neovim/vim | termite | tmux | cmus | i3pystatus | mutt |
| [SyfiMalik](https://github.com/SyfiMalik/cfg.git) | zsh | i3 | vim | rxvt-unicode | tmux | mpd/ncmpcpp | polybar | mutt | weechat |
| [thiagowfx](https://github.com/thiagowfx/dotfiles) | bash | i3 | vim/emacs | tilix | i3blocks |
| [unexist](http://hg.subtle.de/dotfiles/file) | zsh | subtle | vim | rxvt-unicode | ncmpcpp | mutt | irssi |
| [vodik](https://github.com/vodik/dotfiles) | zsh | xmonad | vim | termite-git | tmux | ncmpcpp | personalizado | mutt | weechat |
| [w0ng](https://github.com/w0ng/dotfiles) | zsh | dwm | vim | rxvt-unicode | tmux | ncmpcpp | personalizado | mutt | irssi |
| [whitelynx](https://github.com/whitelynx/dotfiles) | fish | i3 | neovim | kitty | i3pystatus |
| [Wintervenom](https://github.com/Wintervenom/Configuration) | bash | herbstluftwm | vim | rxvt-unicode | screen | mpd ([mpc-utils](https://github.com/Wintervenom/Scripts/tree/master/audio/mpd)) | [hlwm-dzen2](https://github.com/Wintervenom/Scripts/blob/master/wm/herbstluftwm/hlwm-dzen2) | mutt | weechat |
| [wolfcore](https://github.com/wolfcore/dotfiles) | bash | dwm | vim | rxvt-unicode | tmux | cmus | personalizado | weechat |
| [zendeavor](https://github.com/zendeavor) | [zsh](https://github.com/zendeavor/config-stuff/tree/sandbag/zsh) | [i3](https://github.com/zendeavor/config-stuff/blob/sandbag/i3/config) | [vim](https://github.com/zendeavor/dotvim/tree/sandbag) | [rxvt-unicode](https://github.com/zendeavor/config-stuff/blob/sandbag/X11/Xresources#L14) | [tmux](https://github.com/zendeavor/config-stuff/tree/sandbag/tmux) | [ncmpcpp](https://github.com/zendeavor/config-stuff/blob/sandbag/ncmpcpp/config) | [i3status](https://github.com/zendeavor/config-stuff/blob/sandbag/i3/i3status.conf) | [weechat](https://github.com/zendeavor/config-stuff/tree/kiwi/weechat) |

## Veja também

*   [gregswiki:DotFiles](https://mywiki.wooledge.org/DotFiles "gregswiki:DotFiles")
*   [XMonad Config Archive](http://wiki.haskell.org/Xmonad/Config_archive)
*   [dotshare.it](http://dotshare.it)
*   [dotfiles.github.io](https://dotfiles.github.io/)
*   [terminal.sexy](https://terminal.sexy/) - Designer de esquema de cores do terminal