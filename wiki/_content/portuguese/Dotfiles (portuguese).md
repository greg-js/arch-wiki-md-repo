Artigos relacionados

*   [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support")
*   [X resources](/index.php/X_resources "X resources")

Este artigo coleta repositórios de usuários com arquivos de configuração personalizados, comumente conhecidos como *dotfiles* (que poderia ser traduzido como "arquivos-ponto").

## Contents

*   [1 Controle de versão](#Controle_de_vers.C3.A3o)
    *   [1.1 Usando gitignore](#Usando_gitignore)
    *   [1.2 Outras ferramentas](#Outras_ferramentas)
    *   [1.3 Mantendo dotfiles em várias máquinas](#Mantendo_dotfiles_em_v.C3.A1rias_m.C3.A1quinas)
    *   [1.4 Informação confidencial](#Informa.C3.A7.C3.A3o_confidencial)
*   [2 Repositórios](#Reposit.C3.B3rios)
*   [3 Veja também](#Veja_tamb.C3.A9m)

## Controle de versão

A gerência de *dotfiles* com software de controle de versão, como o [Git](/index.php/Git "Git"), ajuda a acompanhar as alterações, compartilhar com outras pessoas e sincronizar os *dotfiles* entre vários hosts.

### Usando gitignore

Manter um [diretório git](https://git-scm.com/blog/2010/04/11/environment.html) dentro da pasta *home* permite acompanhar diretamente as alterações. Recomenda-se adicionar seletivamente o conteúdo do arquivo ao índice com [git-add(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-add.1).

Para evitar arquivos não rastreados (aparecerem em commits e removidos por [git-clean(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clean.1)), primeiro exclua todos os arquivos com [gitignore(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitignore.5):

 `~/.git/info/exclude`  `*` 

Então, use `git add -f`, por exemplo:

```
$ git add -f ~/.config/*

```

e faça commit as alterações com [git-commit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-commit.1):

```
$ git commit -a

```

### Outras ferramentas

*   **dotdrop** — Uma ferramenta para gerenciar diferentes versões de seus *dotfiles* em hosts diferentes.

	[https://github.com/deadc0de6/dotdrop](https://github.com/deadc0de6/dotdrop) || [dotdrop](https://aur.archlinux.org/packages/dotdrop/)

*   **dotfiles** — Uma ferramenta para facilitar o gerenciamento de links simbólicos para seus *dotfiles* em $HOME, permitindo que você mantenha todos eles em um único diretório.

	[https://github.com/jbernard/dotfiles](https://github.com/jbernard/dotfiles) || [dotfiles](https://aur.archlinux.org/packages/dotfiles/)

*   **dotgit** — Uma solução abrangente para gerenciar seus *dotfiles*.

	[http://github.com/Cube777/dotgit](http://github.com/Cube777/dotgit) || [dotgit](https://aur.archlinux.org/packages/dotgit/)

*   **dots** — Uma ferramenta portátil para gerenciar um único conjunto de *dotfiles* de forma organizada.

	[https://github.com/EvanPurkhiser/dots](https://github.com/EvanPurkhiser/dots) || [dots-manager](https://aur.archlinux.org/packages/dots-manager/)

*   **[etckeeper](/index.php/Etckeeper "Etckeeper")** — Destinado a configuração de todo o sistema de controle de versão no /etc. Funciona mantendo o controle de permissões e modos que o software de controle de versão geralmente ignora. Pode usar vários sistemas SCM como backend. Hooks podem autoconfirmar alterações no repositório antes de uma atualização do sistema.

	[http://etckeeper.branchable.com/](http://etckeeper.branchable.com/) || [etckeeper](https://www.archlinux.org/packages/?name=etckeeper)

*   **GNU Stow** — Pode ser usado para fazer um link simbólico para *dotfiles* de um repositório para a árvore $HOME. Consulte [[1]](http://brandon.invergo.net/news/2012-05-26-using-gnu-stow-to-manage-your-dotfiles.html) para mais informações.

	[http://www.gnu.org/software/stow/](http://www.gnu.org/software/stow/) || [stow](https://www.archlinux.org/packages/?name=stow)

*   **homeshick** — Sincronizador de *dotfiles* git escrito em bash.

	[https://github.com/andsens/homeshick](https://github.com/andsens/homeshick) || [homeshick-git](https://aur.archlinux.org/packages/homeshick-git/)

*   **homesick** — Seu diretório home é seu castelo. Não deixe seus dotfiles para trás.

	[https://github.com/technicalpickles/homesick](https://github.com/technicalpickles/homesick) || [homesick](https://aur.archlinux.org/packages/homesick/)

*   **mackup** — Um pequeno utilitário Python para manter as configurações do seu aplicativo em sincronia.

	[https://github.com/lra/mackup](https://github.com/lra/mackup) || [mackup](https://aur.archlinux.org/packages/mackup/)

*   **Pearl** — Gerenciador de pacotes para *dotfiles*, plugins, programas e qualquer forma de código acessível via git. Permite compartilhar e sincronizar pacotes facilmente através de sistemas e tê-los prontos para usar com facilidade.

	[https://github.com/pearl-core/pearl](https://github.com/pearl-core/pearl) || [pearl-git](https://aur.archlinux.org/packages/pearl-git/)

*   **rcm** — Pode ser usado para fazer link simbólicos para dotfiles de um repositório para árvore $HOME.

	[https://github.com/thoughtbot/rcm](https://github.com/thoughtbot/rcm) || [rcm](https://aur.archlinux.org/packages/rcm/)

*   **vcsh** — Permite a separação de módulos diferentes (por exemplo, configuração do Emacs vs. configuração de zsh) em repositórios individuais que podem ser mantidos separadamente, ao contrário de manter todos os arquivos de pontos em um único repositório. Funciona apenas com o git.

	[https://github.com/RichiH/vcsh](https://github.com/RichiH/vcsh) || [vcsh](https://aur.archlinux.org/packages/vcsh/)

*   **yadm** — Gerencia arquivos em sistemas usando um único repositório Git. Fornece uma maneira de usar arquivos alternativos em um sistema operacional ou host específico. Fornece um método de criptografar dados confidenciais para que possa ser armazenado com segurança em seu repositório.

	[https://github.com/TheLocehiliosan/yadm](https://github.com/TheLocehiliosan/yadm) || [yadm-git](https://aur.archlinux.org/packages/yadm-git/)

### Mantendo dotfiles em várias máquinas

Uma forma de manter os *dotfiles* em várias máquinas em vários hosts, permitindo a personalização por host, é manter um ramo mestre para toda a configuração compartilhada, enquanto cada máquina individual possui uma ramificação específica da máquina com check-out. A configuração específica do host pode ser confirmada na ramificação específica da máquina; como a configuração compartilhada é adicionada ao ramo mestre, as ramos por máquina são então *rebase*ados no mestre atualizado.

Outra abordagem é colocar configuração específica de máquina em blocos comentados especialmente para usar [qualia](https://pypi.python.org/pypi/mir.qualia/) para descomentá-los automaticamente cada um. Essa abordagem requer um trabalho menos manual e não causa conflitos de mesclagem.

### Informação confidencial

Ocasionalmente, o software pode manter senhas de texto simples em arquivos de configuração, em vez de depender de um chaveiro. Nesses casos, git sem qualquer filtro pode ser útil para evitar o commit acidental de informações confidenciais. Por exemplo, o arquivo a seguir atribui um filtro ao arquivo "some-dotfile":

 `.gitattributes` 
```
some-dotfile filter=remove-pass

```

Sempre que o arquivo "some-dotfile" verificado pelo git, o git invocará o filtro "remove-pass" no arquivo antes de ser verificado. O filtro deve ser definido no arquivo de configuração do git, p. ex.:

 `.git/config` 
```
[filter "remove-pass"]
clean = "sed -e 's/^password=.*/#password=TODO/'"

```

## Repositórios

| Autor | Shell (estrutura de shell) | WM / DE | Editor | Terminal | Multiplexador | Áudio | Monitor | E-mail | IRC |
| [Ambrevar](https://github.com/Ambrevar/dotfiles) | zsh | awesome | emacs | rxvt-unicode | cmus | htop/vicious | mutt |
| [awal](https://github.com/awalGarg/dotfiles) | fish | i3 | vim | st | tmux | i3status | The Lounge |
| [ayekat](https://github.com/ayekat/dotfiles) | zsh | karuiwm | vim | rxvt-unicode | tmux | ncmpcpp/mpd | karuibar | mutt | irssi |
| [bamos](https://github.com/bamos/dotfiles) | zsh | i3/xmonad | vim/emacs | rxvt-unicode | tmux | mpv/cmus | conky/xmobar | mutt | ERC |
| [brisbin33](https://github.com/pbrisbin/dotfiles) | [zsh](https://github.com/pbrisbin/oh-my-zsh) | [xmonad](https://github.com/pbrisbin/xmonad-config) | [vim](https://github.com/pbrisbin/vim-config) | rxvt-unicode | screen | dzen | [mutt](https://github.com/pbrisbin/mutt-config) | [irssi](https://github.com/pbrisbin/irssi-config) |
| [cinelli](https://github.com/cinelli/dotfiles) | zsh | dwm | vim | termite-git | pianobar | htop | mutt-kz | weechat |
| [dikiaap](https://github.com/dikiaap/dotfiles) | zsh | i3-gaps | neovim | alacritty | tmux | i3blocks |
| [Earnestly](https://github.com/Earnestly/dotfiles) | zsh | i3/orbment | vim/emacs | termite | tmux | mpd | conky | mutt | weechat |
| [ErikBjare](https://github.com/ErikBjare/dotfiles) | zsh | xmonad/xfce4 | vim | terminator | tmux | xfce4-panel | weechat |
| [falconindy](https://github.com/falconindy/dotfiles) | bash | i3 | vim | rxvt-unicode | ncmpcpp | conky | mutt |
| [graysky](https://github.com/graysky2/configs/tree/master/dotfiles) | zsh | xfce4 | vim | terminal | ncmpcpp | personalizado | thunderbird |
| [hugdru](https://github.com/hugdru/dotfiles) | zsh | awesome | neovim | rxvt-unicode | tmux | thunderbird | weechat |
| [insanum](https://github.com/insanum/dotfiles) | bash | herbstluftwm | vim | evilvte | tmux | dzen | mutt-kz |
| [jasonwryan](https://bitbucket.org/jasonwryan/shiv/src) | bash/zsh | dwm | vim | rxvt-unicode | tmux | ncmpcpp | personalizado | mutt | irrsi |
| [jdevlieghere](https://github.com/JDevlieghere/dotfiles/) | zsh | xmonad | vim | terminal | tmux | htop | mutt | weechat |
| [jelly](https://github.com/jelly/Dotfiles) | zsh | i3 | vim | termite | tmux | ncmpcpp | mutt-kz-git | weechat |
| [maximbaz](https://github.com/maximbaz/dotfiles) | zsh | i3-gaps | neovim | alacritty | tmux | py3status | thunderbird |
| [meskarune](https://github.com/meskarune/.dotfiles) | bash | herbstluftwm | vim | rxvt-unicode | screen | conky | weechat |
| [neersighted](https://github.com/neersighted/dotfiles) | zsh | i3 | vim | rxvt-unicode | tmux | ncmpcpp | htop | mutt | irssi |
| [OK100](https://github.com/ok100/configs) | bash | dwm | vim | rxvt-unicode | cmus | conky, dzen | mutt | weechat |
| [polyzen](https://github.com/polyzen/dotfiles) | zsh | i3 | vim | termite | tmux | i3status | weechat |
| [reisub0](https://github.com/reisub0/dot) | bash | awesome | neovim | termite | mpd | conky |
| [sistematico](https://github.com/sistematico/majestic) | zsh/fish/bash | [i3 Gaps](https://github.com/Airblader/i3) | vim/nano | termite | tmux | ncmpcpp | polybar | mutt | weechat |
| [swalladge](https://github.com/swalladge/dotfiles) | zsh/bash | i3 | neovim/vim | termite | tmux | cmus | i3pystatus | mutt |
| [thiagowfx](https://github.com/thiagowfx/dotfiles) | bash/zsh | i3 | vim/emacs | rxvt-unicode | ncmpcpp | i3blocks |
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
*   [terminal.sexy](https://terminal.sexy/) -Designer de esquema de cores do terminal