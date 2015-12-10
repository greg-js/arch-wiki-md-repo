# dotfiles

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

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

[https://github.com/RichiH/vcsh](https://github.com/RichiH/vcsh) || [vcsh](https://aur.archlinux.org/packages/vcsh/)<sup><small>AUR</small></sup>

*   **etckeeper** — Intended to version-control system-wide configuration in /etc. Works by keeping track of permissions and modes which version-control software often ignores. Can use various SCM systems as a backend. Hooks can auto-commit changes to the repository before a system-upgrade; for pacman, these hooks currently have to be triggered manually.

[http://joeyh.name/code/etckeeper/](http://joeyh.name/code/etckeeper/) || [etckeeper](https://www.archlinux.org/packages/?name=etckeeper)

*   **GNU Stow** — Can be used to symlink dotfiles from a repository into the $HOME tree. See [[1]](http://brandon.invergo.net/news/2012-05-26-using-gnu-stow-to-manage-your-dotfiles.html) for more information.

[http://www.gnu.org/software/stow/](http://www.gnu.org/software/stow/) || [stow](https://www.archlinux.org/packages/?name=stow)

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

<table class="wikitable sortable">

<tbody>

<tr>

<th scope="col">Author</th>

<th scope="col">Shell</th>

<th scope="col">WM / DE</th>

<th scope="col">Editor</th>

<th scope="col">Terminal</th>

<th scope="col">Multiplexer</th>

<th scope="col">Audio</th>

<th scope="col">Monitor</th>

<th scope="col">Mail</th>

<th scope="col">IRC</th>

</tr>

<tr>

<th>[Ambrevar](https://bitbucket.org/ambrevar/dotfiles)</th>

<td>zsh</td>

<td>awesome</td>

<td>emacs</td>

<td>rxvt-unicode</td>

<td>cmus</td>

<td>htop/vicious</td>

<td>mutt</td>

</tr>

<tr>

<th>[bamos](https://github.com/bamos/dotfiles)</th>

<td>zsh</td>

<td>i3/xmonad</td>

<td>vim/emacs</td>

<td>rxvt-unicode</td>

<td>tmux</td>

<td>mpv/cmus</td>

<td>conky/xmobar</td>

<td>mutt</td>

<td>ERC</td>

</tr>

<tr>

<th>[brisbin33](https://github.com/pbrisbin/dotfiles)</th>

<td>[zsh](https://github.com/pbrisbin/oh-my-zsh)</td>

<td>[xmonad](https://github.com/pbrisbin/xmonad-config)</td>

<td>[vim](https://github.com/pbrisbin/vim-config)</td>

<td>rxvt-unicode</td>

<td>screen</td>

<td>dzen</td>

<td>[mutt](https://github.com/pbrisbin/mutt-config)</td>

<td>[irssi](https://github.com/pbrisbin/irssi-config)</td>

</tr>

<tr>

<th>[cinelli](https://github.com/cinelli/dotfiles)</th>

<td>zsh</td>

<td>dwm</td>

<td>vim</td>

<td>termite-git</td>

<td>pianobar</td>

<td>htop</td>

<td>mutt-kz</td>

<td>weechat</td>

</tr>

<tr>

<th>[Earnestly](https://github.com/Earnestly/dotfiles)</th>

<td>zsh</td>

<td>i3/orbment</td>

<td>vim/emacs</td>

<td>termite</td>

<td>tmux</td>

<td>mpd</td>

<td>conky</td>

<td>mutt</td>

<td>weechat</td>

</tr>

<tr>

<th>[ErikBjare](https://github.com/ErikBjare/dotfiles)</th>

<td>zsh</td>

<td>xmonad/xfce4</td>

<td>vim</td>

<td>terminator</td>

<td>tmux</td>

<td>xfce4-panel</td>

<td>weechat</td>

</tr>

<tr>

<th>[falconindy](https://github.com/falconindy/dotfiles)</th>

<td>bash</td>

<td>i3</td>

<td>vim</td>

<td>rxvt-unicode</td>

<td>ncmpcpp</td>

<td>conky</td>

<td>mutt</td>

</tr>

<tr>

<th>[graysky](https://github.com/graysky2/configs/tree/master/dotfiles)</th>

<td>zsh</td>

<td>xfce4</td>

<td>vim</td>

<td>terminal</td>

<td>ncmpcpp</td>

<td>custom</td>

<td>thunderbird</td>

</tr>

<tr>

<th>[gtmanfred](http://code.gtmanfred.com/cgit/dotfiles.git/tree/?h=tower)</th>

<td>zsh</td>

<td>dwm</td>

<td>vim</td>

<td>termite-git</td>

<td>tmux</td>

<td>mpd</td>

<td>conky</td>

<td>mutt</td>

<td>weechat</td>

</tr>

<tr>

<th>[insanum](https://github.com/insanum/dotfiles)</th>

<td>bash</td>

<td>herbstluftwm</td>

<td>vim</td>

<td>evilvte</td>

<td>tmux</td>

<td>dzen</td>

<td>mutt-kz</td>

</tr>

<tr>

<th>[izmntuk](https://github.com/izmntuk/archiso/tree/testing/configs/alter/airootfs/)</th>

<td>zsh</td>

<td>xfce4</td>

<td>vim</td>

<td>rxvt-unicode/yaft</td>

<td>tmux</td>

<td>cmus</td>

<td>xfce4-panel</td>

<td>irssi</td>

</tr>

<tr>

<th>[jasonwryan](https://bitbucket.org/jasonwryan/shiv/src)</th>

<td>bash/zsh</td>

<td>dwm</td>

<td>vim</td>

<td>rxvt-unicode</td>

<td>tmux</td>

<td>ncmpcpp</td>

<td>custom</td>

<td>mutt</td>

<td>irrsi</td>

</tr>

<tr>

<th>[jelly](https://github.com/jelly/Dotfiles)</th>

<td>zsh</td>

<td>i3</td>

<td>vim</td>

<td>termite</td>

<td>tmux</td>

<td>ncmpcpp</td>

<td>mutt-kz-git</td>

<td>weechat</td>

</tr>

<tr>

<th>[meskarune](https://github.com/meskarune/.dotfiles)</th>

<td>bash</td>

<td>herbstluftwm</td>

<td>vim</td>

<td>rxvt-unicode</td>

<td>screen</td>

<td>conky</td>

<td>weechat</td>

</tr>

<tr>

<th>[neersighted](https://github.com/neersighted/dotfiles)</th>

<td>zsh</td>

<td>i3</td>

<td>vim</td>

<td>rxvt-unicode</td>

<td>tmux</td>

<td>ncmpcpp</td>

<td>htop</td>

<td>mutt</td>

<td>irssi</td>

</tr>

<tr>

<th>[OK100](https://github.com/ok100/configs)</th>

<td>bash</td>

<td>dwm</td>

<td>vim</td>

<td>rxvt-unicode</td>

<td>cmus</td>

<td>conky, dzen</td>

<td>mutt</td>

<td>weechat</td>

</tr>

<tr>

<th>[unexist](http://hg.subtle.de/dotfiles/file)</th>

<td>zsh</td>

<td>subtle</td>

<td>vim</td>

<td>rxvt-unicode</td>

<td>ncmpcpp</td>

<td>mutt</td>

<td>irssi</td>

</tr>

<tr>

<th>[vodik](https://github.com/vodik/dotfiles)</th>

<td>zsh</td>

<td>xmonad</td>

<td>vim</td>

<td>termite-git</td>

<td>tmux</td>

<td>ncmpcpp</td>

<td>custom</td>

<td>mutt</td>

<td>weechat</td>

</tr>

<tr>

<th>[w0ng](https://github.com/w0ng/dotfiles)</th>

<td>zsh</td>

<td>dwm</td>

<td>vim</td>

<td>rxvt-unicode</td>

<td>tmux</td>

<td>ncmpcpp</td>

<td>custom</td>

<td>mutt</td>

<td>irssi</td>

</tr>

<tr>

<th>[Wintervenom](https://github.com/Wintervenom/Configuration)</th>

<td>bash</td>

<td>herbstluftwm</td>

<td>vim</td>

<td>rxvt-unicode</td>

<td>screen</td>

<td>mpd ([mpc-utils](https://github.com/Wintervenom/Scripts/tree/master/audio/mpd))</td>

<td>[hlwm-dzen2](https://github.com/Wintervenom/Scripts/blob/master/wm/herbstluftwm/hlwm-dzen2https://github.com/wolfcore/dotfiles)</td>

<td>mutt</td>

<td>weechat</td>

</tr>

<tr>

<th>[wolfcore](https://github.com/wolfcore/dotfiles)</th>

<td>bash</td>

<td>dwm</td>

<td>vim</td>

<td>rxvt-unicode</td>

<td>tmux</td>

<td>cmus</td>

<td>custom</td>

<td>weechat</td>

</tr>

<tr>

<th>[xfausto](https://github.com/xfausto/dotfiles)</th>

<td>zsh</td>

<td>dwm</td>

<td>vim</td>

<td>st</td>

<td>ncmpcpp</td>

<td>conky</td>

</tr>

<tr>

<th>[thiagowfx](https://github.com/thiagowfx/dotfiles)</th>

<td>bash/zsh</td>

<td>i3</td>

<td>vim/emacs</td>

<td>rxvt-unicode</td>

<td>ncmpcpp</td>

<td>i3blocks</td>

</tr>

<tr>

<th>[zendeavor](https://github.com/zendeavor)</th>

<td>[zsh](https://github.com/zendeavor/config-stuff/tree/sandbag/zsh)</td>

<td>[i3](https://github.com/zendeavor/config-stuff/blob/sandbag/i3/config)</td>

<td>[vim](https://github.com/zendeavor/dotvim/tree/sandbag)</td>

<td>[rxvt-unicode](https://github.com/zendeavor/config-stuff/blob/sandbag/X11/Xresources#L14)</td>

<td>[tmux](https://github.com/zendeavor/config-stuff/tree/sandbag/tmux)</td>

<td>[ncmpcpp](https://github.com/zendeavor/config-stuff/blob/sandbag/ncmpcpp/config)</td>

<td>[i3status](https://github.com/zendeavor/config-stuff/blob/sandbag/i3/i3status.conf)</td>

<td>[weechat](https://github.com/zendeavor/config-stuff/tree/kiwi/weechat)</td>

</tr>

<tr>

<th>[bstaletic](https://github.com/bstaletic)</th>

<td>[zsh](https://github.com/bstaletic/dotfiles/blob/master/.zshrc)</td>

<td>[dwm](https://github.com/bstaletic/dotfiles/blob/master/dwm/config.h)</td>

<td>[vim](https://github.com/bstaletic/dotfiles/blob/master/.vimrc)</td>

<td>terminator</td>

<td>screen</td>

<td>[ncmpcpp](https://github.com/bstaletic/blob/master/.ncmpcpp/config)</td>

<td>[conky](https://github.com/bstaletic/dotfiles/blob/master/.conkyrc)</td>

</tr>

</tbody>

</table>

## See also

*   [Dotfiles - Greg's Wiki](http://mywiki.wooledge.org/DotFiles)
*   [XMonad Config Archive](http://wiki.haskell.org/Xmonad/Config_archive)
*   [dotshare.it](http://dotshare.it)
*   [dotfiles.org](http://dotfiles.org)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2015-08-16]</sup> - [Copy of contents](http://techie.cat/all-contents-from-dotfiles-org/)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2015-08-16]</sup>
*   [dotfiles.github.io](https://dotfiles.github.io/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dotfiles&oldid=406222](https://wiki.archlinux.org/index.php?title=Dotfiles&oldid=406222)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Dotfiles](/index.php/Category:Dotfiles "Category:Dotfiles")