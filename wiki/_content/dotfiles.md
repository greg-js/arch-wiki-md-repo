# dotfiles

Related articles

*   [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support")

This article collects user repositories with custom configuration files, commonly known as _dotfiles_.

## Contents

*   [1 Version control](#Version_control)
    *   [1.1 Using gitignore](#Using_gitignore)
    *   [1.2 Other tools](#Other_tools)
    *   [1.3 Maintaining dotfiles across multiple machines](#Maintaining_dotfiles_across_multiple_machines)
    *   [1.4 Confidential information](#Confidential_information)
*   [2 Repositories](#Repositories)
*   [3 See also](#See_also)

## Version control

Managing dotfiles with version control software such as [Git](/index.php/Git "Git") helps to keep track of changes, share with others, and synchronize dotfiles across various hosts.

### Using gitignore

Keeping a [git directory](https://git-scm.com/blog/2010/04/11/environment.html) inside the home folder allows to directly keep track of changes. It is recommended to selectively add file contents to the index with [git add](http://git-scm.com/docs/git-add).

To prevent untracked files (appearing in commits and removed by [git clean](http://git-scm.com/docs/git-clean)), first exclude all files with [gitignore](http://git-scm.com/docs/gitignore):

 `~/.git/info/exclude`  `*` 

Then use `git add -f`, for example:

```
$ git add -f ~/.config/*

```

And [commit](http://git-scm.com/docs/git-commit) the changes:

```
$ git commit -a

```

### Other tools

*   **vcsh** — Allows separating differents modules (e.g., Emacs config vs. zsh config) into individual repositories which can be maintained separately, as opposed to keeping all dotfiles in a single repository. Works with git only.

NaN

*   **yadm** — Manages files across systems using a single Git repository. Provides a way to use alternate files on a specific OS or host. Supplies a method of encrypting confidential data so it can safely be stored in your repository.

NaN

*   **etckeeper** — Intended to version-control system-wide configuration in /etc. Works by keeping track of permissions and modes which version-control software often ignores. Can use various SCM systems as a backend. Hooks can auto-commit changes to the repository before a system-upgrade; for pacman, these hooks currently have to be triggered manually.

NaN

*   **GNU Stow** — Can be used to symlink dotfiles from a repository into the $HOME tree. See [[1]](http://brandon.invergo.net/news/2012-05-26-using-gnu-stow-to-manage-your-dotfiles.html) for more information.

NaN

### Maintaining dotfiles across multiple machines

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** This and the section below need a rewrite (Discuss in [Talk:Dotfiles#](https://wiki.archlinux.org/index.php/Talk:Dotfiles))

One way of maintaining dotfiles across various machines across various hosts while still allowing for per-host customizations, is by maintaining a master-branch for all shared configuration, while each individual machine has a machine-specific branch checked out. Host-specific configuration can be committed to the machine-specific branch; as shared configuration is added to the master-branch, the per-machine branches are then rebased on top of the updated master.

### Confidential information

Occasionally, software may keep plain-text passwords in configuration files, as opposed to hooking into a keyring. In these cases, git clean-filters may be handy to avoid accidentally commiting confidential information. E. g., the following .gitattributes file assigns a filter to the file “some-dotfile”:

```
# .gitattributes
some-dotfile filter=remove-pass

```

Whenever the file “some-dotfile” is checked into git, git will invoke the filter “remove-pass” on the file before checking it in. The filter must be defined in .git/config, e. g.:

```
[filter "remove-pass"]
clean = "sed -e 's/^password=.*/#password=TODO/'"

```

## Repositories

| Author | Shell | WM / DE | Editor | Terminal | Multiplexer | Audio | Monitor | Mail | IRC |
| [Ambrevar](https://bitbucket.org/ambrevar/dotfiles) | zsh | awesome | emacs | rxvt-unicode | cmus | htop/vicious | mutt |
| [bamos](https://github.com/bamos/dotfiles) | zsh | i3/xmonad | vim/emacs | rxvt-unicode | tmux | mpv/cmus | conky/xmobar | mutt | ERC |
| [brisbin33](https://github.com/pbrisbin/dotfiles) | [zsh](https://github.com/pbrisbin/oh-my-zsh) | [xmonad](https://github.com/pbrisbin/xmonad-config) | [vim](https://github.com/pbrisbin/vim-config) | rxvt-unicode | screen | dzen | [mutt](https://github.com/pbrisbin/mutt-config) | [irssi](https://github.com/pbrisbin/irssi-config) |
| [cinelli](https://github.com/cinelli/dotfiles) | zsh | dwm | vim | termite-git | pianobar | htop | mutt-kz | weechat |
| [drkhsh](https://github.com/drkh5h/dotfiles) | zsh | dwm | vim | rxvt-unicode | conky | mutt | weechat |
| [Earnestly](https://github.com/Earnestly/dotfiles) | zsh | i3/orbment | vim/emacs | termite | tmux | mpd | conky | mutt | weechat |
| [ErikBjare](https://github.com/ErikBjare/dotfiles) | zsh | xmonad/xfce4 | vim | terminator | tmux | xfce4-panel | weechat |
| [falconindy](https://github.com/falconindy/dotfiles) | bash | i3 | vim | rxvt-unicode | ncmpcpp | conky | mutt |
| [graysky](https://github.com/graysky2/configs/tree/master/dotfiles) | zsh | xfce4 | vim | terminal | ncmpcpp | custom | thunderbird |
| [gtmanfred](http://code.gtmanfred.com/cgit/dotfiles.git/tree/?h=tower) | zsh | dwm | vim | termite-git | tmux | mpd | conky | mutt | weechat |
| [insanum](https://github.com/insanum/dotfiles) | bash | herbstluftwm | vim | evilvte | tmux | dzen | mutt-kz |
| [izmntuk](https://github.com/izmntuk/archiso/tree/testing/configs/alter/airootfs/) | zsh | xfce4 | vim | rxvt-unicode/yaft | tmux | cmus | xfce4-panel | irssi |
| [jasonwryan](https://bitbucket.org/jasonwryan/shiv/src) | bash/zsh | dwm | vim | rxvt-unicode | tmux | ncmpcpp | custom | mutt | irrsi |
| [jelly](https://github.com/jelly/Dotfiles) | zsh | i3 | vim | termite | tmux | ncmpcpp | mutt-kz-git | weechat |
| [meskarune](https://github.com/meskarune/.dotfiles) | bash | herbstluftwm | vim | rxvt-unicode | screen | conky | weechat |
| [neersighted](https://github.com/neersighted/dotfiles) | zsh | i3 | vim | rxvt-unicode | tmux | ncmpcpp | htop | mutt | irssi |
| [OK100](https://github.com/ok100/configs) | bash | dwm | vim | rxvt-unicode | cmus | conky, dzen | mutt | weechat |
| [unexist](http://hg.subtle.de/dotfiles/file) | zsh | subtle | vim | rxvt-unicode | ncmpcpp | mutt | irssi |
| [vodik](https://github.com/vodik/dotfiles) | zsh | xmonad | vim | termite-git | tmux | ncmpcpp | custom | mutt | weechat |
| [w0ng](https://github.com/w0ng/dotfiles) | zsh | dwm | vim | rxvt-unicode | tmux | ncmpcpp | custom | mutt | irssi |
| [Wintervenom](https://github.com/Wintervenom/Configuration) | bash | herbstluftwm | vim | rxvt-unicode | screen | mpd ([mpc-utils](https://github.com/Wintervenom/Scripts/tree/master/audio/mpd)) | [hlwm-dzen2](https://github.com/Wintervenom/Scripts/blob/master/wm/herbstluftwm/hlwm-dzen2https://github.com/wolfcore/dotfiles) | mutt | weechat |
| [wolfcore](https://github.com/wolfcore/dotfiles) | bash | dwm | vim | rxvt-unicode | tmux | cmus | custom | weechat |
| [xfausto](https://github.com/xfausto/dotfiles) | zsh | dwm | vim | st | ncmpcpp | conky |
| [thiagowfx](https://github.com/thiagowfx/dotfiles) | bash/zsh | i3 | vim/emacs | rxvt-unicode | ncmpcpp | i3blocks |
| [zendeavor](https://github.com/zendeavor) | [zsh](https://github.com/zendeavor/config-stuff/tree/sandbag/zsh) | [i3](https://github.com/zendeavor/config-stuff/blob/sandbag/i3/config) | [vim](https://github.com/zendeavor/dotvim/tree/sandbag) | [rxvt-unicode](https://github.com/zendeavor/config-stuff/blob/sandbag/X11/Xresources#L14) | [tmux](https://github.com/zendeavor/config-stuff/tree/sandbag/tmux) | [ncmpcpp](https://github.com/zendeavor/config-stuff/blob/sandbag/ncmpcpp/config) | [i3status](https://github.com/zendeavor/config-stuff/blob/sandbag/i3/i3status.conf) | [weechat](https://github.com/zendeavor/config-stuff/tree/kiwi/weechat) |
| [bstaletic](https://github.com/bstaletic) | [zsh](https://github.com/bstaletic/dotfiles/blob/master/.zshrc) | [dwm](https://github.com/bstaletic/dotfiles/blob/master/dwm/config.h) | [vim](https://github.com/bstaletic/dotfiles/blob/master/.vimrc) | terminator | screen | [ncmpcpp](https://github.com/bstaletic/blob/master/.ncmpcpp/config) | [conky](https://github.com/bstaletic/dotfiles/blob/master/.conkyrc) |

## See also

*   [Dotfiles - Greg's Wiki](http://mywiki.wooledge.org/DotFiles)
*   [XMonad Config Archive](http://wiki.haskell.org/Xmonad/Config_archive)
*   [dotshare.it](http://dotshare.it)
*   [dotfiles.org](http://dotfiles.org)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2015-08-16]</sup> - [Copy of contents](http://techie.cat/all-contents-from-dotfiles-org/)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2015-08-16]</sup>
*   [dotfiles.github.io](https://dotfiles.github.io/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dotfiles&oldid=417127](https://wiki.archlinux.org/index.php?title=Dotfiles&oldid=417127)"