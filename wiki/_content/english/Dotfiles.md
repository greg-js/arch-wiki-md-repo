Related articles

*   [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support")
*   [X resources](/index.php/X_resources "X resources")

User-specific application configuration is traditionally stored in so called [dotfiles](https://en.wikipedia.org/wiki/dotfile "wikipedia:dotfile") (files whose filename starts with a dot). It is common practice to track dotfiles with a [version control system](/index.php/Version_control_system "Version control system") such as [Git](/index.php/Git "Git") to keep track of changes and synchronize dotfiles across various hosts. There are various approaches to managing your dotfiles (e.g. directly tracking dotfiles in the home directory v.s. storing them in a subdirectory and symlinking/copying/generating files with a [shell](/index.php/Shell "Shell") script or [a dedicated tool](#Tools)). Apart from explaining how to manage your dotfiles this article also contains [a list of dotfile repositories](#User_repositories) from Arch Linux users.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Tracking dotfiles directly with Git](#Tracking_dotfiles_directly_with_Git)
*   [2 Host-specific configuration](#Host-specific_configuration)
*   [3 Tools](#Tools)
    *   [3.1 Tools wrapping Git](#Tools_wrapping_Git)
*   [4 User repositories](#User_repositories)
*   [5 See also](#See_also)

## Tracking dotfiles directly with Git

The benefit of tracking dotfiles directly with Git is that it only requires [Git](/index.php/Git "Git") and does not involve symlinks. The disadvantage is that [host-specific configuration](#Host-specific_configuration) generally requires merging changes into multiple [branches](/index.php/Git#Branching "Git").

The simplest way to achieve this approach is to initialize a [Git](/index.php/Git "Git") repository directly in your home directory and ignoring all files by default with a [gitignore(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitignore.5) pattern of `*`. This method however comes with two drawbacks: it can become confusing when you have other Git repositories in your home directory (e.g. if you forget to initialize a repository you suddenly operate on your dotfile repository) and you can no longer easily see which files in the current directory are untracked (because they are ignored).

An alternative method without these drawbacks is the "bare repository and alias method" popularized by [this Hacker News comment](https://news.ycombinator.com/item?id=11070797), which just takes three commands to set up:

```
$ git init --bare ~/.dotfiles
$ alias config='/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
$ config config status.showUntrackedFiles no

```

You can then manage your dotfiles with the created [alias](/index.php/Alias "Alias").

**Tip:** To avoid accidentally commiting confidential information, see [Git#Filtering confidential information](/index.php/Git#Filtering_confidential_information "Git").

## Host-specific configuration

A common problem with synchronizing dotfiles across various machines is host-specific configuration.

With [Git](/index.php/Git "Git") this can be solved by maintaining a master branch for all shared configuration, while each individual machine has a machine-specific branch checked out. Host-specific configuration can be committed to the machine-specific branch; when shared configuration is modified in the master branch, the per-machine branches need to be rebased on top of the updated master.

In configuration scripts like [shell configuration files](/index.php/Command-line_shell#Configuration_files "Command-line shell") conditional logic can be used. For example, [Bash](/index.php/Bash "Bash") scripts (i.e. `.bashrc`) can apply different configuration depending on the machine name (or type, custom variable, etc.):

```
if [[ "$(hostname)" == "archlaptop" ]]; then
    # laptop specific commands here
else
    # desktop or server machine commands
fi

```

Similar can also be achieved with [.Xresources](/index.php/.Xresources ".Xresources").[[1]](https://jnrowe.github.io/articles/tips/Sharing_Xresources_between_systems.html)

If you find rebasing Git branches too cumbersome, you may want to use a [tool](#Tools) that supports *file grouping*, or if even greater flexibility is desired, a tool that does *processing*.

## Tools

	File grouping

	How configuration files can be grouped to configuration groups (also called profiles or packages).

	Processing

	Some tools process configuration files to allow them to be customized depending on the host.

| Name | Package | Written in | File grouping | Processing |
| [dot-templater](https://github.com/kesslern/dot-templater) | [dot-templater-git](https://aur.archlinux.org/packages/dot-templater-git/) | Rust | directory-based | custom syntax |
| [dotdrop](https://deadc0de.re/dotdrop/) | [dotdrop](https://aur.archlinux.org/packages/dotdrop/) | Python | configuration file | Jinja2 |
| [dotfiles](https://github.com/jbernard/dotfiles) | [dotfiles](https://aur.archlinux.org/packages/dotfiles/) | Python | [No](https://github.com/jbernard/dotfiles/pull/24) | No |
| [Dots](https://github.com/EvanPurkhiser/dots) | [dots-manager](https://aur.archlinux.org/packages/dots-manager/) | Python | directory-based | custom append points |
| [chezmoi](https://github.com/twpayne/chezmoi) | [chezmoi](https://www.archlinux.org/packages/?name=chezmoi) | Go | directory-based | Go templates |
| [GNU Stow](https://www.gnu.org/software/stow/) | [stow](https://www.archlinux.org/packages/?name=stow) | Perl | directory-based[[2]](http://brandon.invergo.net/news/2012-05-26-using-gnu-stow-to-manage-your-dotfiles.html) | No |
| [Mackup](https://github.com/lra/mackup) | [mackup](https://aur.archlinux.org/packages/mackup/) | Python | automatic per application | No |
| [mir.qualia](https://github.com/darkfeline/mir.qualia) | [mir.qualia](https://aur.archlinux.org/packages/mir.qualia/) | Python | No | custom blocks |
| [rcm](https://github.com/thoughtbot/rcm) | [rcm](https://aur.archlinux.org/packages/rcm/) | Perl | directory-based (by host or tag) | No |

### Tools wrapping Git

If you are uncomfortable with [Git](/index.php/Git "Git"), you may want to use one of these tools, which abstract the version control system away (more or less).

| Name | Package | Written in | File grouping | Processing |
| [dotgit](https://github.com/kobus-v-schoor/dotgit) | [dotgit](https://aur.archlinux.org/packages/dotgit/) | Bash | filename-based | No |
| [homeshick](https://github.com/andsens/homeshick) | [homeshick-git](https://aur.archlinux.org/packages/homeshick-git/) | Bash | repository-wise | No |
| [homesick](https://github.com/technicalpickles/homesick) | [homesick](https://aur.archlinux.org/packages/homesick/) | Ruby | repository-wise | No |
| [Pearl](https://github.com/pearl-core/pearl) | [pearl-git](https://aur.archlinux.org/packages/pearl-git/) | Bash | repository-wise | No |
| [vcsh](https://github.com/RichiH/vcsh) | [vcsh](https://aur.archlinux.org/packages/vcsh/) | Shell | repository-wise | No |
| [yadm](https://thelocehiliosan.github.io/yadm/) | [yadm-git](https://aur.archlinux.org/packages/yadm-git/) | Shell | filename-based
(by class, OS, hostname & user) [[3]](https://thelocehiliosan.github.io/yadm/docs/alternates) | Jinja2
(optional)[[4]](https://thelocehiliosan.github.io/yadm/docs/alternates#jinja-templates) |

1.  Supports encryption of confidential files with [GPG](/index.php/GPG "GPG").[[5]](https://thelocehiliosan.github.io/yadm/docs/encryption)

## User repositories

| Author | Shell (Shell framework) | WM / DE | Editor | Terminal | Multiplexer | Audio | Monitor | Mail | IRC |
| [alfunx](https://github.com/alfunx/.dotfiles) | zsh | awesome | vim | kitty | tmux | ncmpcpp/mpd | htop/lain | thunderbird |
| [peterzuger](https://gitlab.com/peterzuger/dotfiles) | zsh | i3-gaps | emacs | rxvt-unicode | screen | moc | htop |
| [Ambrevar](https://gitlab.com/Ambrevar/dotfiles) | Eshell | EXWM | Emacs | Emacs (Eshell) | Emacs TRAMP + dtach | EMMS | conky/dzen | mu4e | Circe |
| [awal](https://github.com/awalGarg/dotfiles) | fish | i3 | vim | st | tmux | i3status | The Lounge |
| [ayekat](https://github.com/ayekat/dotfiles) | zsh | karuiwm | vim | rxvt-unicode | tmux | ncmpcpp/mpd | karuibar | mutt | irssi |
| [bamos](https://github.com/bamos/dotfiles) | zsh | i3/xmonad | vim/emacs | rxvt-unicode | tmux | mpv/cmus | conky/xmobar | mutt | ERC |
| [brisbin33](https://github.com/pbrisbin/dotfiles) | [zsh](https://github.com/pbrisbin/oh-my-zsh) | [xmonad](https://github.com/pbrisbin/xmonad-config) | [vim](https://github.com/pbrisbin/vim-config) | rxvt-unicode | screen | dzen | [mutt](https://github.com/pbrisbin/mutt-config) | [irssi](https://github.com/pbrisbin/irssi-config) |
| [BVollmerhaus](https://gitlab.com/BVollmerhaus/dotfiles) | [fish](https://gitlab.com/BVollmerhaus/dotfiles/tree/master/config/fish-custom) | [i3-gaps](https://gitlab.com/BVollmerhaus/dotfiles/blob/master/config/i3/config) | [kakoune](https://gitlab.com/BVollmerhaus/dotfiles/blob/master/config/kak/kakrc) | rxvt-unicode | [polybar](https://gitlab.com/BVollmerhaus/dotfiles/blob/master/config/polybar/config) | thunderbird |
| [cinelli](https://github.com/cinelli/dotfiles) | zsh | dwm | vim | termite-git | pianobar | htop | mutt-kz | weechat |
| [dikiaap](https://github.com/dikiaap/dotfiles) | zsh | i3-gaps | neovim | alacritty | tmux | i3blocks |
| [Earnestly](https://github.com/Earnestly/dotfiles) | zsh | i3/orbment | vim/emacs | termite | tmux | mpd | conky | mutt | weechat |
| [ErikBjare](https://github.com/ErikBjare/dotfiles) | zsh | xmonad/xfce4 | vim | terminator | tmux | xfce4-panel | weechat |
| [falconindy](https://github.com/falconindy/dotfiles) | bash | i3 | vim | rxvt-unicode | ncmpcpp | conky | mutt |
| [graysky](https://github.com/graysky2/configs/tree/master/dotfiles) | zsh | xfce4 | vim | terminal | ncmpcpp | custom | thunderbird |
| [hugdru](https://github.com/hugdru/dotfiles) | zsh | awesome | neovim | rxvt-unicode | tmux | thunderbird | weechat |
| [insanum](https://github.com/insanum/dotfiles) | bash | herbstluftwm | vim | evilvte | tmux | dzen | mutt-kz |
| [jasonwryan](https://bitbucket.org/jasonwryan/shiv/src) | bash/zsh | dwm | vim | rxvt-unicode | tmux | ncmpcpp | custom | mutt | irssi |
| [jdevlieghere](https://github.com/JDevlieghere/dotfiles/) | zsh | xmonad | vim | terminal | tmux | htop | mutt | weechat |
| [jelly](https://github.com/jelly/Dotfiles) | zsh | i3 | vim | termite | tmux | ncmpcpp | mutt-kz-git | weechat |
| [Jorengarenar](https://github.com/Jorengarenar/dotfiles) | bash | i3 | vim | xterm | mpv | i3blocks | aerc | weechat |
| [maximbaz](https://github.com/maximbaz/dotfiles) | zsh | i3-gaps | neovim | kitty | py3status | thunderbird |
| [mehalter](https://gitlab.com/mehalter/dotfiles) | zsh | i3-gaps | neovim | termite | tmux | gpymusic | i3blocks, gotop | neomutt | weechat |
| [meskarune](https://github.com/meskarune/.dotfiles) | bash | herbstluftwm | vim | rxvt-unicode | screen | conky | weechat |
| [neersighted](https://github.com/neersighted/dotfiles) | zsh | i3 | vim | rxvt-unicode | tmux | ncmpcpp | htop | mutt | irssi |
| [oibind](https://github.com/oibind/dotfiles) | fish | awesome | neovim | termite | htop-vim | weechat |
| [OK100](https://github.com/ok100/configs) | bash | dwm | vim | rxvt-unicode | cmus | conky, dzen | mutt | weechat |
| [pablox-cl](https://github.com/pablox-cl/dotfiles) | zsh (zplug) | gnome3 | neovim | kitty |
| [reisub0](https://github.com/reisub0/dot) | fish | qtile | neovim | kitty | mpd | conky |
| [sistematico](https://github.com/sistematico/majestic) | zsh/fish/bash | [i3-gaps](https://github.com/Airblader/i3) | vim/nano | termite | tmux | ncmpcpp | polybar | mutt | weechat |
| [sitilge](https://git.sitilge.id.lv/sitilge/dotfiles) | zsh | awesome | neovim | termite | thunderbird |
| [swalladge](https://github.com/swalladge/dotfiles) | zsh/bash | i3 | neovim/vim | termite | tmux | cmus | i3pystatus | mutt |
| [SyfiMalik](https://github.com/SyfiMalik/cfg) | zsh | i3 | vim | rxvt-unicode | tmux | ncmpcpp/mpd | polybar | mutt | weechat |
| [thiagowfx](https://github.com/thiagowfx/dotfiles) | bash | i3 | vim/emacs | tilix | i3blocks |
| [vodik](https://github.com/vodik/dotfiles) | zsh | xmonad | vim | termite-git | tmux | ncmpcpp | custom | mutt | weechat |
| [w0ng](https://github.com/w0ng/dotfiles) | zsh | dwm | vim | rxvt-unicode | tmux | ncmpcpp | custom | mutt | irssi |
| [whitelynx](https://github.com/whitelynx/dotfiles) | fish | i3 | neovim | kitty | i3pystatus |
| [Wintervenom](https://github.com/Wintervenom/Configuration) | bash | herbstluftwm | vim | rxvt-unicode | screen | mpd ([mpc-utils](https://github.com/Wintervenom/Scripts/tree/master/audio/mpd)) | [hlwm-dzen2](https://github.com/Wintervenom/Scripts/blob/master/wm/herbstluftwm/hlwm-dzen2) | mutt | weechat |
| [wolfcore](https://github.com/wolfcore/dotfiles) | bash | dwm | vim | rxvt-unicode | tmux | cmus | custom | weechat |
| [zendeavor](https://github.com/zendeavor) | [zsh](https://github.com/zendeavor/config-stuff/tree/sandbag/zsh) | [i3](https://github.com/zendeavor/config-stuff/blob/sandbag/i3/config) | [vim](https://github.com/zendeavor/dotvim/tree/sandbag) | [rxvt-unicode](https://github.com/zendeavor/config-stuff/blob/sandbag/X11/Xresources#L14) | [tmux](https://github.com/zendeavor/config-stuff/tree/sandbag/tmux) | [ncmpcpp](https://github.com/zendeavor/config-stuff/blob/sandbag/ncmpcpp/config) | [i3status](https://github.com/zendeavor/config-stuff/blob/sandbag/i3/i3status.conf) | [weechat](https://github.com/zendeavor/config-stuff/tree/kiwi/weechat) |

## See also

*   [gregswiki:DotFiles](https://mywiki.wooledge.org/DotFiles "gregswiki:DotFiles")
*   [XMonad Config Archive](http://wiki.haskell.org/Xmonad/Config_archive)
*   [dotshare.it](http://dotshare.it)
*   [dotfiles.github.io](https://dotfiles.github.io/)
*   [terminal.sexy](https://terminal.sexy/) - Terminal color scheme designer