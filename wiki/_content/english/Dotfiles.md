Related articles

*   [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support")
*   [X resources](/index.php/X_resources "X resources")

This article collects user repositories with custom configuration files, commonly known as *dotfiles*.

## Contents

*   [1 Version control](#Version_control)
    *   [1.1 Using gitignore](#Using_gitignore)
    *   [1.2 Other tools](#Other_tools)
    *   [1.3 Maintaining dotfiles across multiple machines](#Maintaining_dotfiles_across_multiple_machines)
*   [2 Repositories](#Repositories)
*   [3 See also](#See_also)

## Version control

Managing dotfiles with [version control systems](/index.php/Version_control_system "Version control system") such as [Git](/index.php/Git "Git") helps to keep track of changes, share with others, and synchronize dotfiles across various hosts.

### Using gitignore

Keeping a [git directory](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository) inside the home folder allows to directly keep track of changes. It is recommended to selectively add file contents to the index with [git-add(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-add.1).

To prevent untracked files (appearing in commits and removed by [git-clean(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clean.1)), first exclude all files with [gitignore(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitignore.5):

 `~/.git/info/exclude`  `*` 

Then use `git add -f`, for example:

```
$ git add -f ~/.config/*

```

And commit the changes with [git-commit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-commit.1):

```
$ git commit -a

```

**Tip:** To avoid accidentally commiting confidential information, see [Git#Filtering confidential information](/index.php/Git#Filtering_confidential_information "Git").

### Other tools

*   **dotdrop** — A tool to manage your dotfiles across different hosts and saving them to git without duplicates.

	[https://github.com/deadc0de6/dotdrop](https://github.com/deadc0de6/dotdrop) || [dotdrop](https://aur.archlinux.org/packages/dotdrop/)

*   **dotfiles** — A tool to make managing your dotfile symlinks in $HOME easy, allowing you to keep all of them in a single directory.

	[https://github.com/jbernard/dotfiles](https://github.com/jbernard/dotfiles) || [dotfiles](https://aur.archlinux.org/packages/dotfiles/)

*   **dotgit** — A comprehensive solution to managing your dotfiles.

	[http://github.com/Cube777/dotgit](http://github.com/Cube777/dotgit) || [dotgit](https://aur.archlinux.org/packages/dotgit/)

*   **dots** — A portable tool for managing a single set of dotfiles in an organized fashion.

	[https://github.com/EvanPurkhiser/dots](https://github.com/EvanPurkhiser/dots) || [dots-manager](https://aur.archlinux.org/packages/dots-manager/)

*   **[etckeeper](/index.php/Etckeeper "Etckeeper")** — Intended to version-control system-wide configuration in /etc. Works by keeping track of permissions and modes which version-control software often ignores. Can use various SCM systems as a backend. Hooks can auto-commit changes to the repository before a system-upgrade.

	[http://etckeeper.branchable.com/](http://etckeeper.branchable.com/) || [etckeeper](https://www.archlinux.org/packages/?name=etckeeper)

*   **GNU Stow** — Can be used to symlink dotfiles from a repository into the $HOME tree. See [[1]](http://brandon.invergo.net/news/2012-05-26-using-gnu-stow-to-manage-your-dotfiles.html) for more information.

	[http://www.gnu.org/software/stow/](http://www.gnu.org/software/stow/) || [stow](https://www.archlinux.org/packages/?name=stow)

*   **homeshick** — git dotfiles synchronizer written in bash.

	[https://github.com/andsens/homeshick](https://github.com/andsens/homeshick) || [homeshick-git](https://aur.archlinux.org/packages/homeshick-git/)

*   **homesick** — Your home directory is your castle. Don't leave your dotfiles behind.

	[https://github.com/technicalpickles/homesick](https://github.com/technicalpickles/homesick) || [homesick](https://aur.archlinux.org/packages/homesick/)

*   **mackup** — a small Python utitlity to keep your application settings in sync.

	[https://github.com/lra/mackup](https://github.com/lra/mackup) || [mackup](https://aur.archlinux.org/packages/mackup/)

*   **Pearl** — Package manager for dotfiles, plugins, programs and any form of code accessible via git. Allow to easily share and sync packages across systems and have them ready to work out of the box.

	[https://github.com/pearl-core/pearl](https://github.com/pearl-core/pearl) || [pearl-git](https://aur.archlinux.org/packages/pearl-git/)

*   **rcm** — Can be used to symlink dotfiles from a repository into the $HOME tree.

	[https://github.com/thoughtbot/rcm](https://github.com/thoughtbot/rcm) || [rcm](https://aur.archlinux.org/packages/rcm/)

*   **vcsh** — Allows separating differents modules (e.g., Emacs config vs. zsh config) into individual repositories which can be maintained separately, as opposed to keeping all dotfiles in a single repository. Works with git only.

	[https://github.com/RichiH/vcsh](https://github.com/RichiH/vcsh) || [vcsh](https://aur.archlinux.org/packages/vcsh/)

*   **yadm** — Manages files across systems using a single Git repository. Provides a way to use alternate files on a specific OS or host. Supplies a method of encrypting confidential data so it can safely be stored in your repository.

	[https://github.com/TheLocehiliosan/yadm](https://github.com/TheLocehiliosan/yadm) || [yadm-git](https://aur.archlinux.org/packages/yadm-git/)

### Maintaining dotfiles across multiple machines

One way of maintaining dotfiles across various machines across various hosts while still allowing for per-host customizations, is by maintaining a master-branch for all shared configuration, while each individual machine has a machine-specific branch checked out. Host-specific configuration can be committed to the machine-specific branch; as shared configuration is added to the master-branch, the per-machine branches are then rebased on top of the updated master.

The drawback on having some of the configuration files in multiple branches is that you have to remember to maintain and synchronize changes. Use conditional logic to minimize the number of machine specific files. For example, bash scripts (i.e. `.bashrc`) can apply different configuration depending on the machine name (or type, custom variable, etc.):

```
if [[ "$(uname -n)" == "archlaptop" ]]; then
    # laptop specific commands here
else
    # desktop or server machine commands
fi

```

Another approach is to manage machine-specific configuration with tools based on template engines, e.g. [qualia](https://pypi.python.org/pypi/mir.qualia/) or [Dotdrop](https://github.com/deadc0de6/dotdrop). This approach requires less manual work and doesn't cause merge conflicts.

## Repositories

| Author | Shell (Shell framework) | WM / DE | Editor | Terminal | Multiplexer | Audio | Monitor | Mail | IRC |
| [alfunx](https://github.com/alfunx/.dotfiles) | zsh | awesome | vim | kitty | tmux | ncmpcpp/mpd | htop/lain | thunderbird |
| [Ambrevar](https://github.com/Ambrevar/dotfiles) | zsh | awesome | emacs | rxvt-unicode | cmus | htop/vicious | mutt |
| [awal](https://github.com/awalGarg/dotfiles) | fish | i3 | vim | st | tmux | i3status | The Lounge |
| [ayekat](https://github.com/ayekat/dotfiles) | zsh | karuiwm | vim | rxvt-unicode | tmux | ncmpcpp/mpd | karuibar | mutt | irssi |
| [bamos](https://github.com/bamos/dotfiles) | zsh | i3/xmonad | vim/emacs | rxvt-unicode | tmux | mpv/cmus | conky/xmobar | mutt | ERC |
| [brisbin33](https://github.com/pbrisbin/dotfiles) | [zsh](https://github.com/pbrisbin/oh-my-zsh) | [xmonad](https://github.com/pbrisbin/xmonad-config) | [vim](https://github.com/pbrisbin/vim-config) | rxvt-unicode | screen | dzen | [mutt](https://github.com/pbrisbin/mutt-config) | [irssi](https://github.com/pbrisbin/irssi-config) |
| [BVollmerhaus](https://gitlab.com/BVollmerhaus/dotfiles) | bash | [i3-gaps](https://gitlab.com/BVollmerhaus/dotfiles/blob/master/config/i3/config) | [kakoune](https://gitlab.com/BVollmerhaus/dotfiles/blob/master/config/kak/kakrc) | rxvt-unicode | [polybar](https://gitlab.com/BVollmerhaus/dotfiles/blob/master/config/polybar/config) | thunderbird |
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
| [maximbaz](https://github.com/maximbaz/dotfiles) | zsh | i3-gaps | neovim | kitty | py3status | thunderbird |
| [meskarune](https://github.com/meskarune/.dotfiles) | bash | herbstluftwm | vim | rxvt-unicode | screen | conky | weechat |
| [neersighted](https://github.com/neersighted/dotfiles) | zsh | i3 | vim | rxvt-unicode | tmux | ncmpcpp | htop | mutt | irssi |
| [OK100](https://github.com/ok100/configs) | bash | dwm | vim | rxvt-unicode | cmus | conky, dzen | mutt | weechat |
| [pablox-cl](https://github.com/pablox-cl/dotfiles) | zsh (zplug) | gnome3 | neovim | kitty |
| [reisub0](https://github.com/reisub0/dot) | bash | awesome | neovim | termite | mpd | conky |
| [sistematico](https://github.com/sistematico/majestic) | zsh/fish/bash | [i3-gaps](https://github.com/Airblader/i3) | vim/nano | termite | tmux | ncmpcpp | polybar | mutt | weechat |
| [sitilge](https://git.sitilge.id.lv/sitilge/dotfiles) | zsh | awesome | neovim | termite | thunderbird |
| [swalladge](https://github.com/swalladge/dotfiles) | zsh/bash | i3 | neovim/vim | termite | tmux | cmus | i3pystatus | mutt |
| [SyfiMalik](https://github.com/SyfiMalik/cfg) | zsh | i3 | vim | rxvt-unicode | tmux | ncmpcpp/mpd | polybar | mutt | weechat |
| [thiagowfx](https://github.com/thiagowfx/dotfiles) | bash/zsh | i3 | vim/emacs | rxvt-unicode | ncmpcpp | i3blocks |
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