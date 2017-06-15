This article exists to catalog the growing set of software using the [XDG Base Directory Specification](http://standards.freedesktop.org/basedir-spec/latest/) introduced in 2003\. This is here to demonstrate the viability of this specification by listing commonly found dotfiles and their support status. For those not currently supporting the Base Directory Specification, workarounds will be demonstrated to emulate it instead.

The workarounds will be limited to anything not involving patching the source, executing code stored in [environment variables](/index.php/Environment_variable "Environment variable") or compile-time options. The rationale for this is that configurations should be portable across systems and having compile-time options prevent that.

Hopefully this will provide a source of information about exactly what certain kinds of dotfiles are and where they come from.

## Contents

*   [1 XDG Base Directory specification](#XDG_Base_Directory_specification)
    *   [1.1 User directories](#User_directories)
    *   [1.2 System directories](#System_directories)
*   [2 Contributing](#Contributing)
*   [3 Supported](#Supported)
*   [4 Partial](#Partial)
*   [5 Hardcoded](#Hardcoded)
*   [6 Library and language support](#Library_and_language_support)
*   [7 See also](#See_also)

## XDG Base Directory specification

Please read the [full specification](http://standards.freedesktop.org/basedir-spec/latest/). This section will attempt to break down the essence of what it tries to achieve.

Only `XDG_RUNTIME_DIR` is set by default through [pam_systemd](http://www.freedesktop.org/software/systemd/man/pam_systemd.html). It is up to the user to explicitly [define](/index.php/Define "Define") the other variables, using absolute paths that point to existing directories.

### User directories

*   `XDG_CONFIG_HOME`
    *   Where user-specific configurations should be written (analogous to `/etc`).
    *   Should default to `$HOME/.config`.

*   `XDG_CACHE_HOME`
    *   Where user-specific non-essential (cached) data should be written (analogous to `/var/cache`).
    *   Should default to `$HOME/.cache`.

*   `XDG_DATA_HOME`
    *   Where user-specific data files should be written (analogous to `/usr/share`).
    *   Should default to `$HOME/.local/share`.

*   `XDG_RUNTIME_DIR`
    *   Used for non-essential, user-specific data files such as sockets, named pipes, etc.
    *   Not required to have a default value; warnings should be issued if not set or equivalents provided.
    *   Must be owned by the user with an access mode of `0700`.
    *   Filesystem fully featured by standards of OS.
    *   Must be on the local filesystem.
    *   May be subject to periodic cleanup.
    *   Modified every 6 hours or set sticky bit if persistence is desired.
    *   Can only exist for the duration of the user's login.
    *   Should not store large files as it may be mounted as a tmpfs.

### System directories

*   `XDG_DATA_DIRS`
    *   List of directories seperated by `:` (analogous to `PATH`).
    *   Should default to `/usr/local/share:/usr/share`.

*   `XDG_CONFIG_DIRS`
    *   List of directories seperated by `:` (analogous to `PATH`).
    *   Should default to `/etc/xdg`.

## Contributing

When contributing make sure to use the correct section.

Nothing should require code evaluation (such as [vim](/index.php/Vim "Vim") and `VIMINIT`), patches or compile-time options to gain support and anything which does must be deemed hardcoded. Additionally if the process is too error prone or difficult, such as [Haskell's cabal](https://www.haskell.org/cabal/) or eclipse, they should also be considered as hardcoded.

*   The first column should be the project name, ideally the command name if it is not ambigious, linked to their website or an appropriate internal wiki article.

*   The second column is for any legacy files and directories the project had (one per line), this is done so people can find them even if they are no longer read.

*   In the third, try to find the commit or version a project switched to XDG Base Directory or any open discussions and include them in the next two columns (two per line).

*   The last column should include any appropriate workarounds or solutions. Please verify that your solution is correct and functional.

## Supported

| Application | Legacy Path | Supported Since | Discussion | Notes |
| [aerc](https://github.com/SirCmpwn/aerc) |
| [antimicro](https://github.com/Antimicro/antimicro/) | `~/.antimicro` | [edba864](https://github.com/Antimicro/antimicro/commit/edba864) | [[1]](https://github.com/Antimicro/antimicro/issues/5) |
| [aria2](/index.php/Aria2 "Aria2") | `~/.aria2` | [8bc1d37](https://github.com/tatsuhiro-t/aria2/commit/8bc1d37) | [[2]](https://github.com/tatsuhiro-t/aria2/issues/27) |
| [blender](/index.php/Blender "Blender") | `~/.blender` | [4293f473](http://git.blender.org/gitweb/gitweb.cgi/blender.git/commit/4293f473) | [[3]](https://developer.blender.org/T28943) |
| [burp](https://github.com/falconindy/burp) | [f2388e9](https://github.com/falconindy/burp/commit/f2388e9) |
| [chromium](/index.php/Chromium "Chromium") | `~/.chromium` | [23057](https://src.chromium.org/viewvc/chrome?revision=23057&view=revision) | [[4]](https://groups.google.com/forum/#!topic/chromium-dev/QekVQxF3nho) [[5]](https://code.google.com/p/chromium/issues/detail?id=16976) |
| [citra](http://citra-emu.org/) | `~/.citra-emu` | [f7c3193fec](https://github.com/citra-emu/citra/commit/f7c3193fec) | [[6]](https://github.com/citra-emu/citra/pull/575) |
| [composer](/index.php/PHP#Composer "PHP") | `~/.composer` | [1.0.0-beta1](https://github.com/composer/composer/releases/tag/1.0.0-beta1) | [[7]](https://github.com/composer/composer/pull/1407) |
| [cower](https://github.com/falconindy/cower) | [8b70805](https://github.com/falconindy/cower/commit/8b70805) |
| [d-feet](https://wiki.gnome.org/Apps/DFeet) | `~/.d-feet` | [7f6104b](https://git.gnome.org/browse/d-feet/commit/?id==7f6104b) |
| [dconf](https://wiki.gnome.org/dconf) |
| [dolphin-emu](/index.php/Dolphin_emulator "Dolphin emulator") | `~/.dolphin-emu` | [a498c68](https://github.com/dolphin-emu/dolphin/commit/a498c68) | [[8]](https://github.com/dolphin-emu/dolphin/pull/2304) |
| [dr14-meter](http://dr14tmeter.sourceforge.net) | [7e777ca64](https://github.com/simon-r/dr14_t.meter/commit/7e777ca645298ec898b3c76e3ec472ed6ed43e8a) | [[9]](https://github.com/simon-r/dr14_t.meter/pull/30) | Hardcoded `$HOME/.config/dr14meter` |
| [dunst](http://www.knopwob.org/dunst/index.html) | [78b6e2b1](https://github.com/knopwob/dunst/commit/78b6e2b1) | [[10]](https://github.com/knopwob/dunst/issues/22) |
| [dwb](/index.php/Dwb "Dwb") |
| [fish](/index.php/Fish "Fish") |
| [fontconfig](/index.php/Fontconfig "Fontconfig") | `~/.fontconfig`

`~/.fonts`

 | [8c255fb1](http://cgit.freedesktop.org/fontconfig/commit/?id=8c255fb1) | Use `"$XDG_DATA_HOME"/fonts` to store fonts instead. |
| [fontforge](http://fontforge.github.io/) | `~/.FontForge`

`~/.PfaEdit`

 | [e4c2cc7432](https://github.com/fontforge/fontforge/commit/e4c2cc7432) | [[11]](https://github.com/fontforge/fontforge/issues/847) [[12]](https://github.com/fontforge/fontforge/issues/991) |
| [freerdp](http://www.freerdp.com/) | `~/.freerdp` | [edf6e7258d](https://github.com/FreeRDP/FreeRDP/commit/edf6e7258d) |
| [gconf](https://projects.gnome.org/gconf) | `~/.gconf` | [fc28caa7](https://git.gnome.org/browse/gconf/commit/?id=fc28caa7) | [[13]](https://bugzilla.gnome.org/show_bug.cgi?id=674803) |
| [git](/index.php/Git "Git") | `~/.gitconfig` | [0d94427e](https://github.com/git/git/commit/0d94427e) |
| [gstreamer](http://gstreamer.freedesktop.org/) | `~/.gstreamer-0.10` | [4e36f93924cf](http://cgit.freedesktop.org/gstreamer/gstreamer/commit/?id=4e36f93924cf) | [[14]](https://bugzilla.gnome.org/show_bug.cgi?id=518597) |
| [gtk3](/index.php/Gtk "Gtk") |
| [htop](http://hisham.hm/htop/) | `~/.htoprc` | [93233a67](https://github.com/hishamhm/htop/commit/93233a67) |
| [i3](/index.php/I3 "I3") | `~/.i3` | [7c130fb54](http://code.stapelberg.de/git/i3/commit/?id=7c130fb54) |
| [i3status](http://i3wm.org/i3status/) | `~/.i3status.conf` | [c3f7fc4994](http://code.stapelberg.de/git/i3status/commit/?id=c3f7fc4994) |
| [imagemagick](http://www.imagemagick.org/script/index.php) |
| [inkscape](/index.php/Inkscape "Inkscape") | `~/.inkscape` | [0.47](http://wiki.inkscape.org/wiki/index.php/Release_notes/0.47#Preferences) | [[15]](https://bugs.launchpad.net/inkscape/+bug/199720) |
| [latexmk](https://www.ctan.org/pkg/latexmk?lang=en) | `~/.latexmkrc` |
| [lftp](http://lftp.yar.ru/) | `~/.lftp` | [21dc400](https://github.com/lavv17/lftp/commit/21dc400) | [[16]](https://www.mail-archive.com/lftp@uniyar.ac.ru/msg04301.html) |
| [lgogdownloader](https://github.com/Sude-/lgogdownloader/) | `~/.gogdownloader` | [d430af63d000](https://github.com/Sude-/lgogdownloader/commit/d430af63d000) | [[17]](https://github.com/Sude-/lgogdownloader/issues/4) |
| [LibreOffice](/index.php/LibreOffice "LibreOffice") | [a6f56f70](https://cgit.freedesktop.org/libreoffice/ure/commit/?id=a6f56f70a4930d3f71bd9c9b90fdd0ba20e4da5f) [25bd2eec](https://cgit.freedesktop.org/libreoffice/bootstrap/commit/?id=25bd2eec77ed774a37d1cddd0d72312e23d5e9fd) | [[18]](https://bugs.documentfoundation.org/show_bug.cgi?id=32263) |
| [livestreamer](/index.php/Livestreamer "Livestreamer") | `~/.livestreamerrc` | [ea805917](https://github.com/chrippa/livestreamer/commit/ea805917) | [[19]](https://github.com/chrippa/livestreamer/pull/106) |
| [llpp](/index.php/Llpp "Llpp") | [3ab86f0cb](http://repo.or.cz/w/llpp.git/commit/3ab86f0cb) | Currently llpp places the configuration directly under `XDG_CONFIG_HOME` instead of creating a directory. |
| [mc](/index.php/Mc "Mc") | `~/.mc` | [1b9957058](https://www.midnight-commander.org/changeset/1b9957058) [0b7115647](https://www.midnight-commander.org/changeset/0b7115647)

[ce401d797](https://www.midnight-commander.org/changeset/ce401d797)

 | [[20]](https://www.midnight-commander.org/ticket/1851) |
| [Mercurial](/index.php/Mercurial "Mercurial") | `~/.hgrc` | [354020079723](https://www.mercurial-scm.org/repo/hg/rev/354020079723) [4.2](https://www.mercurial-scm.org/wiki/Release4.2) | `XDG_CONFIG_HOME/hg/hgrc`. |
| [mesa](https://www.mesa3d.org/) | [87ab26b2ab](https://cgit.freedesktop.org/mesa/mesa/commit/?id=87ab26b2ab35a29d446ae66f1795d40c184c0739) | `XDG_CACHE_HOME/mesa` |
| [milkytracker](http://milkytracker.org/) | `~/.milkytracker_config` | [eb487c55](https://github.com/Deltafire/MilkyTracker/commit/eb487c55) | [[21]](https://github.com/Deltafire/MilkyTracker/issues/12) |
| [mintty](https://github.com/mintty/mintty) | `~/.minttyrc` | [cff1bd8f](https://github.com/mintty/mintty/commit/cff1bd8f) v2.3.7. | [[22]](https://github.com/mintty/mintty/issues/525) |
| [mpd](/index.php/Mpd "Mpd") | `~/.mpdconf` | [87b73284](http://git.musicpd.org/cgit/master/mpd.git/commit/?id=87b73284) |
| [mpv](/index.php/Mpv "Mpv") | `~/.mpv` | [cb250d490](https://github.com/mpv-player/mpv/commit/cb250d490) | [[23]](https://github.com/mpv-player/mpv/pull/864) |
| [mutt](/index.php/Mutt "Mutt") | `~/.mutt` | [42fee7585f](https://dev.mutt.org/trac/changeset/42fee7585f) | [[24]](http://dev.mutt.org/trac/ticket/3207) |
| [mypaint](http://mypaint.intilinux.com/) | `~/.mypaint` | [cf723b74cd](https://github.com/mypaint/mypaint/commit/cf723b74cd) |
| [ncmpcpp](/index.php/Ncmpcpp "Ncmpcpp") | `~/.ncmpcpp` | [38d9f811](https://github.com/arybczak/ncmpcpp/commit/38d9f811de888e512b0115f551a9679eab4607f9) [27cd86e0](https://github.com/arybczak/ncmpcpp/commit/27cd86e0638bba3a7a78e44ac40dc98a58d1d90d) | [[25]](https://github.com/arybczak/ncmpcpp/issues/79) [[26]](https://github.com/arybczak/ncmpcpp/issues/110) | `ncmpcpp_directory` should be set to avoid an `error.log` file in `~/.ncmpcpp`. |
| [neovim](/index.php/Neovim "Neovim") | `~/.nvim`

`~/.nvimlog`

`~/.nviminfo`

 | [1ca5646bb](https://github.com/neovim/neovim/commit/1ca5646bb) | [[27]](https://github.com/neovim/neovim/issues/78) [[28]](https://github.com/neovim/neovim/pull/3198) |
| [newsbeuter](/index.php/Newsbeuter "Newsbeuter") | `~/.newsbeuter` | [3c57824c5](https://github.com/akrennmair/newsbeuter/commit/3c57824c5) | [[29]](https://github.com/akrennmair/newsbeuter/pull/39) | It is required to create both directories [[30]](http://newsbeuter.org/doc/newsbeuter.html#_xdg_base_directory_support):

`$ mkdir -p "$XDG_DATA_HOME"/newsbeuter "$XDG_CONFIG_HOME"/newsbeuter`

 |
| [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP") | `~/.offlineimaprc` | [5150de5](https://github.com/OfflineIMAP/offlineimap/commit/5150de5) | [[31]](https://github.com/OfflineIMAP/offlineimap/issues/32) |
| [opentyrian](https://bitbucket.org/opentyrian/opentyrian/wiki/Home) | `~/.opentyrian` | [8d45ff2](https://bitbucket.org/opentyrian/opentyrian/commits/8d45ff2) | [[32]](https://web.archive.org/web/20140815181350/http://code.google.com/p/opentyrian/issues/detail?id=125) |
| [pcsx2](http://pcsx2.net/) | `~/.pcsx2` | [87f1e8f77](https://github.com/PCSX2/pcsx2/commit/87f1e8f77) [a9020c606](https://github.com/PCSX2/pcsx2/commit/a9020c606)

[3b22f0fb0](https://github.com/PCSX2/pcsx2/commit/3b22f0fb0) [0a012aec2](https://github.com/PCSX2/pcsx2/commit/0a012aec2)

 | [[33]](https://github.com/PCSX2/pcsx2/issues/352) [[34]](https://github.com/PCSX2/pcsx2/issues/381) |
| [pip](https://pip.pypa.io/) | `~/.pip` | [6.0](https://github.com/pypa/pip/blob/548a9136525815dff41acd845c558a0b36eb1c5f/NEWS.rst#60-2014-12-22) | [[35]](https://github.com/pypa/pip/issues/1733) |
| [ppsspp](http://www.ppsspp.org/) | `~/.ppsspp` | [132fe47c7d](https://github.com/hrydgard/ppsspp/commit/132fe47c7d) | [[36]](https://github.com/hrydgard/ppsspp/issues/4623) |
| [procps-ng](https://www.archlinux.org/packages/?name=procps-ng) | `~/.toprc` | [af53e170b9](https://gitlab.com/procps-ng/procps/commit/af53e170b9) | [[37]](https://gitlab.com/procps-ng/procps/merge_requests/38) [[38]](https://bugzilla.redhat.com/show_bug.cgi?id=1155265) |
| [orbment](https://github.com/Cloudef/orbment/) |
| [pacman](/index.php/Pacman "Pacman") | `~/.makepkg.conf` | [80eca94c8](https://projects.archlinux.org/pacman.git/commit/?id=80eca94c8) | [[39]](https://mailman.archlinux.org/pipermail/pacman-dev/2014-July/019178.html) |
| [PulseAudio](/index.php/PulseAudio "PulseAudio") | `~/.pulse`

`~/.pulse-cookie`

 | [59a8618dcd9](http://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=59a8618dcd9) [87ae8307057](http://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=87ae8307057)

[9ab510a6921](http://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=9ab510a6921) [4c195bcc9d5](http://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=4c195bcc9d5)

 | [[40]](https://bugzilla.redhat.com/show_bug.cgi?id=845607) |
| [pyroom](http://pyroom.org/index.html) |
| [qutebrowser](/index.php/Qutebrowser "Qutebrowser") |
| [qtile](/index.php/Qtile "Qtile") | [fd8686e](https://github.com/qtile/qtile/commit/fd8686e5b4e4fa20bb82039ed8a83768434585ec) [66d704b](https://github.com/qtile/qtile/commit/66d704bce83f631b3326f10a1bc9fc22f8e6a6fd)

[51cff01](https://github.com/qtile/qtile/commit/51cff019917b87bda696b381493f969ceb6cc350)

 | [[41]](https://github.com/qtile/qtile/pull/835) | Some optional bar widgets can create files and directories in non-compliant paths, but most often these are still configurable. |
| [rclone](https://www.archlinux.org/packages/?name=rclone) | `~/.rclone.conf` | [9d362589](https://github.com/ncw/rclone/commit/9d362589) | [[42]](https://github.com/ncw/rclone/issues/868) |
| [retroarch](http://www.libretro.com/) |
| [rr](http://rr-project.org/) | `~/.rr` | [02e7d41e](https://github.com/mozilla/rr/commit/02e7d41e) | [[43]](https://github.com/mozilla/rr/issues/1455) |
| [Snes9x](http://www.snes9x.com/) | `~/.snes9x` | [19864677](https://github.com/snes9xgit/snes9x/commit/93b5f11641fa22d4518f251d6e3db99219864677) | [[44]](https://github.com/snes9xgit/snes9x/issues/194) | By default configuration is blank, is intended that the user fill it at they will (throw the gui or manually) before launch a rom |
| [sublime-text-dev](https://aur.archlinux.org/packages/sublime-text-dev/) | Cache is placed in `$XDG_CONFIG_HOME/sublime-text-3/Cache` instead of expected `$XDG_CACHE_HOME/sublime-text-3`. |
| [surfraw](/index.php/Surfraw "Surfraw") | `~/.surfraw.conf`

`~/.surfraw.bookmarks`

 | [3e4591d8](http://anonscm.debian.org/cgit/surfraw/surfraw.git/commit/?id=3e4591d8) [bd8c427d](http://anonscm.debian.org/cgit/surfraw/surfraw.git/commit/?id=bd8c427d)

[f57fc718](http://anonscm.debian.org/cgit/surfraw/surfraw.git/commit/?id=f57fc718)

 |
| [sway](/index.php/Sway "Sway") | `~/.sway/config` | [614393c09](https://github.com/SirCmpwn/sway/commit/614393c09) | [[45]](https://github.com/SirCmpwn/sway/issues/5) |
| [systemd](/index.php/Systemd "Systemd") |
| [termite](/index.php/Termite "Termite") |
| [transmission](/index.php/Transmission "Transmission") | `~/.transmission` | [5517](https://trac.transmissionbt.com/changeset/5517) | [[46]](https://trac.transmissionbt.com/ticket/684) |
| [util-linux](https://www.kernel.org/pub/linux/utils/util-linux/) | [570b32100](http://git.kernel.org/cgit/utils/util-linux/util-linux.git/commit/?id=570b32100) |
| [uzbl](/index.php/Uzbl "Uzbl") | [c6fd63a](https://github.com/uzbl/uzbl/commit/c6fd63a) | [[47]](https://github.com/uzbl/uzbl/pull/150) |
| [vimb](http://fanglingsu.github.io/vimb/) |
| [VirtualBox](/index.php/VirtualBox "VirtualBox") | `~/.VirtualBox` | [4.3](https://www.virtualbox.org/ticket/5099?action=diff&version=7) | [[48]](https://www.virtualbox.org/ticket/5099) |
| [vis](http://martanne.github.io/vis/) | `~/.vis` | [[49]](https://github.com/martanne/vis/pull/303) | [68a25c75](https://github.com/martanne/vis/commit/68a25c751c0219ef5df589a19513e46a08965d5a)

[d138908c](https://github.com/martanne/vis/commit/d138908cf8149eb10120957271cd6979272b4730)

 |
| [VLC media player](/index.php/VLC_media_player "VLC media player") | `~/.vlcrc` | [16f32e15](http://git.videolan.org/?p=vlc.git;a=commit;h=16f32e1500887c0dcd33cb06ad71759a81a52878) | [[50]](https://trac.videolan.org/vlc/ticket/1267) |
| [warsow](https://www.warsow.gg/) | `~/.warsow-2.x` | [98ece3f](https://github.com/Qfusion/qfusion/commit/98ece3f) | [[51]](https://github.com/Qfusion/qfusion/issues/298) |
| [wireshark](/index.php/Wireshark "Wireshark") | `~/.wireshark` | [b0b53fa5](https://code.wireshark.org/review/gitweb?p=wireshark.git;a=commit;h=b0b53fa5937aa7ba258427ca0f3581dba725230d) |
| [xsettingsd](https://github.com/derat/xsettingsd) | `~/.xsettingsd` | [4ecd7be](https://github.com/derat/xsettingsd/commit/b4999f5e9e99224caf97d09f25ee731774ecd7be) |
| [xmonad](/index.php/Xmonad "Xmonad") | `~/.xmonad` | [40fc10b6](https://github.com/xmonad/xmonad/commit/40fc10b6a5682ce1d6ba7f0679962926ef6cfade) | [[52]](https://github.com/xmonad/xmonad/issues/61) [[53]](https://code.google.com/p/xmonad/issues/detail?id=484) | Alternatively the environments `XMONAD_CONFIG_HOME`, `XMONAD_DATA_HOME`, and `XMONAD_CACHE_HOME` are also available. |

## Partial

| Application | Legacy Path | Supported Since | Discussion | Notes |
| [abook](http://abook.sourceforge.net/) | `~/.abook` | `$ abook --config "$XDG_CONFIG_HOME"/abook/abookrc \`

`--datafile "$XDG_CACHE_HOME"/abook/addressbook`

 |
| [Anki](/index.php/Anki "Anki") | `~/Anki`

`~/Documents/Anki`

 | [[54]](https://github.com/dae/anki/pull/49) [[55]](https://github.com/dae/anki/pull/58) | `$ anki -b "$XDG_DATA_HOME"/Anki` |
| [aspell](/index.php/Aspell "Aspell") | `~/.aspell.conf` |
| [Atom](/index.php/Atom "Atom") | `~/.atom` | [[56]](https://github.com/atom/atom/issues/8281) | `$ export ATOM_HOME="$XDG_DATA_HOME"/atom` |
| [cargo](http://crates.io/) | `~/.cargo` | [[57]](https://github.com/rust-lang/cargo/pull/148) [[58]](https://github.com/rust-lang/cargo/issues/1734) [[59]](https://github.com/rust-lang/rfcs/pull/1615) | `$ export CARGO_HOME="$XDG_DATA_HOME"/cargo` |
| [ccache](/index.php/Ccache "Ccache") | `~/.ccache` | `$ export CCACHE_DIR="$XDG_CACHE_HOME"/ccache` |
| [ChezScheme](https://github.com/cisco/ChezScheme) | `~/.chezscheme_history` | `$ petite --eehistory "$XDG_DATA_HOME"/chezscheme/history` |
| [conky](/index.php/Conky "Conky") | `~/.conkyrc` | [00481ee](https://github.com/brndnmtthws/conky/commit/00481ee9a97025e8e2acd7303d080af1948f7980) | [[60]](https://github.com/brndnmtthws/conky/issues/144) | `$ conky --config="$XDG_CONFIG_HOME"/conky/conkyrc` |
| [coreutils](/index.php/Coreutils "Coreutils") | `~/.dircolors` | `$ source "$(dircolors "$XDG_CONFIG_HOME"/dircolors)"` |
| [crawl](http://www.dungeoncrawl.org/) | `~/.crawl` | The trailing slash is required:

`$ export CRAWL_DIR="$XDG_DATA_HOME"/crawl/`

 |
| [dict](/index.php/Dict "Dict") | `~/.dictrc` | `$ dict -c "$XDG_CONFIG_HOME"/dict/dictrc` |
| [ELinks](/index.php/ELinks "ELinks") | `~/.elinks` | `$ export ELINKS_CONFDIR="$XDG_CONFIG_HOME"/elinks` |
| [emscripten](http://kripken.github.io/emscripten-site/) | `~/.emscripten`

`~/.emscripten_sanity`

`~/.emscripten_ports`

`~/.emscripten_cache__last_clear`

 | [3624](https://github.com/kripken/emscripten/issues/3624) | `$ export EM_CONFIG="$XDG_CONFIG_HOME"/emscripten/config`

`$ export EM_CACHE="$XDG_CACHE_HOME"/emscripten/cache`

`$ export EM_PORTS="$XDG_DATA_HOME"/emscripten/cache`

`$ emcc --em-config "$XDG_CONFIG_HOME"/emscripten/config \ --em-cache "$XDG_CACHE_HOME"/emscripten/cache`

 |
| [gdb](http://www.gnu.org/software/gdb/) | `~/.gdbinit` | `$ gdb -nh -x "$XDG_CONFIG_HOME"/gdb/init` |
| [get_iplayer](https://github.com/get-iplayer/get_iplayer) | `~/.get_iplayer` | `$ export GETIPLAYERUSERPREFS="$XDG_DATA_HOME"/get_iplayer` |
| [GIMP](/index.php/GIMP "GIMP") | `~/.gimp-2.8`

`~/.thumbnails`

 | [60e0cfe](https://git.gnome.org/browse/gimp/commit/?id=60e0cfe) | [[61]](https://bugzilla.gnome.org/show_bug.cgi?id=166643) [[62]](https://mail.gnome.org/archives/gimp-developer-list/2012-October/msg00028.html) | `$ export GIMP2_DIRECTORY="$XDG_CONFIG_HOME"/gimp` |
| [gliv](http://guichaz.free.fr/gliv/) | `~/.glivrc` | `$ gliv --glivrc="$XDG_CONFIG_HOME"/gliv/glivrc` |
| [GnuPG](/index.php/GnuPG "GnuPG") | `~/.gnupg` | [[63]](https://bugs.gnupg.org/gnupg/issue1456) [[64]](https://bugs.gnupg.org/gnupg/issue1018) | `$ export GNUPGHOME="$XDG_CONFIG_HOME"/gnupg`

`$ gpg2 --homedir "$XDG_CONFIG_HOME"/gnupg`

 |
| [Google Earth](/index.php/Google_Earth "Google Earth") | `~/.googleearth` | Some paths can be changed with the `KMLPath` and `CachePath` options in `~/.config/Google/GoogleEarthPlus.conf` |
| [GQ LDAP client](https://sourceforge.net/projects/gqclient) | `~/.gq`

`~/.gq-state`

 | [1.51](https://sourceforge.net/p/gqclient/mailman/message/2053978) | `$ export GQRC="$XDG_CONFIG_HOME"/gqrc`

`$ export GQSTATE="$XDG_DATA_HOME"/gq/gq-state`

`$ mkdir -p "$(dirname "$GQSTATE")"`

 |
| [gradle](https://gradle.org/) | `~/.gradle` | [[65]](https://discuss.gradle.org/t/be-a-nice-freedesktop-citizen-move-the-gradle-to-the-appropriate-location-in-linux/2199) | `$ export GRADLE_USER_HOME="$XDG_DATA_HOME"/gradle` |
| [gtk](/index.php/Gtk "Gtk") | `~/.gtkrc` | `$ export GTK_RC_FILES="$XDG_CONFIG_HOME"/gtk-1.0/gtkrc` |
| [gtk2](/index.php/Gtk "Gtk") | `~/.gtkrc-2.0` | `$ export GTK2_RC_FILES="$XDG_CONFIG_HOME"/gtk-2.0/gtkrc` |
| [httpie](http://httpie.org) | `~/.httpie` | [[66]](https://github.com/jakubroztocil/httpie/issues/145) | `$ export HTTPIE_CONFIG_DIR="$XDG_CONFIG_HOME"/httpie` |
| [ipython](http://ipython.org)/[jupyter](/index.php/Jupyter "Jupyter") | `~/.ipython` | `$ export IPYTHONDIR="$XDG_CONFIG_HOME"/jupyter`

`$ export JUPYTER_CONFIG_DIR="$XDG_CONFIG_HOME"/jupyter`

 |
| [irssi](/index.php/Irssi "Irssi") | `~/.irssi` | [[67]](https://github.com/irssi/irssi/pull/511) | `$ irssi --config="$XDG_CONFIG_HOME"/irssi/config \`

`--home="$XDG_DATA_HOME"/irssi`

 |
| [isync](/index.php/Isync "Isync") | `~/.mbsyncrc` | `$ mbsync -c "$XDG_CONFIG_HOME"/isync/mbsyncrc` |
| [less](/index.php/Core_utilities#less "Core utilities") | `~/.lesshst` | `$ mkdir -p "$XDG_CACHE_HOME"/less`

`$ export LESSHISTFILE="$XDG_CACHE_HOME"/less/history`

`$ export LESSHISTFILE=-` can be used to disable this feature.

`$ export LESSKEY="$XDG_CONFIG_HOME"/less/lesskey`

 |
| [libdvdcss](http://www.videolan.org/developers/libdvdcss.html) | `~/.dvdcss` | [[68]](https://mailman.videolan.org/pipermail/libdvdcss-devel/2014-August/001022.html) | `$ export DVDCSS_CACHE="$XDG_DATA_HOME"/dvdcss` |
| [libice](https://www.x.org/releases/current/doc/libICE/ice.html) | `~/.ICEauthority` | [[69]](https://bugs.freedesktop.org/show_bug.cgi?id=49173) | `$ export ICEAUTHORITY="$XDG_RUNTIME_DIR"/ICEauthority` |
| [libx11](/index.php/Xorg "Xorg") | `~/.XCompose` | `$ export XCOMPOSEFILE="$XDG_CONFIG_HOME"/X11/xcompose` |
| [ltrace](http://ltrace.org/) | `~/.ltrace.conf` | `$ ltrace -F "$XDG_CONFIG_HOME"/ltrace/ltrace.conf` |
| [maven](https://www.archlinux.org/packages/?name=maven) | `~/.m2` | `$ mvn -gs "$XDG_CONFIG_HOME"/maven/settings.xml` `[settings.xml](http://maven.apache.org/settings.html)` 
```
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                      https://maven.apache.org/xsd/settings-1.0.0.xsd">
  ...
  <localRepository>${env.XDG_CACHE_HOME}/maven/repository</localRepository>
  ...
</settings>
```
 |
| [Mathematica](/index.php/Mathematica "Mathematica") | `~/.Mathematica` | `$ export MATHEMATICA_USERBASE="$XDG_CONFIG_HOME"/mathematica` |
| [mednafen](http://mednafen.sourceforge.net/) | `~/.mednafen` | `$ export MEDNAFEN_HOME="$XDG_CONFIG_HOME"/mednafen` |
| [moc](/index.php/Moc "Moc") | `~/.moc` | `$ mocp -M "$XDG_CONFIG_HOME"/moc`

`$ mocp -O MOCDir="$XDG_CONFIG_HOME"/moc`

 |
| [MPlayer](/index.php/MPlayer "MPlayer") | `~/.mplayer` | `$ export MPLAYER_HOME="$XDG_CONFIG_HOME"/mplayer` |
| [ncurses](https://www.archlinux.org/packages/?name=ncurses) | `~/.terminfo` | Precludes system path searching:

`$ export TERMINFO="$XDG_DATA_HOME"/terminfo`

`$ export TERMINFO_DIRS="$XDG_DATA_HOME"/terminfo:/usr/share/terminfo`

 |
| [ncmpc](http://www.musicpd.org/clients/ncmpc/) | `~/.ncmpc` | `ncmpc -f "$XDG_CONFIG_HOME"/ncmpc/config` |
| [NetBeans](/index.php/NetBeans "NetBeans") | `~/.netbeans` | [[70]](https://netbeans.org/bugzilla/show_bug.cgi?id=215961) | `$ netbeans --userdir "${XDG_CONFIG_HOME}"/netbeans` |
| [notmuch](/index.php/Notmuch "Notmuch") | `~/.notmuch-config` | [[71]](http://notmuchmail.org/pipermail/notmuch/2011/007007.html) | `$ export NOTMUCH_CONFIG="$XDG_CONFIG_HOME"/notmuch/notmuchrc`

`$ export NMBGIT="$XDG_DATA_HOME"/notmuch/nmbug`

 |
| [npm](https://www.archlinux.org/packages/?name=npm) | `~/.npm`

`~/.npmrc`

 | [[72]](https://github.com/npm/npm/issues/6675) | `$ export NPM_CONFIG_USERCONFIG=$XDG_CONFIG_HOME/npm/npmrc` `npmrc` 
```
cache=$XDG_CACHE_HOME/npm
prefix=$XDG_DATA_HOME/npm
```
 |
| [NVIDIA](/index.php/NVIDIA "NVIDIA"), [CUDA](/index.php/CUDA "CUDA") | `~/.nv` | `$ export __GL_SHADER_DISK_CACHE_PATH="$XDG_CACHE_HOME"/nv`

`$ export CUDA_CACHE_PATH="$XDG_CACHE_HOME"/nv`

 |
| [nvidia-settings](https://github.com/NVIDIA/nvidia-settings) | `~/.nvidia-settings-rc` | `$ nvidia-settings --config="$XDG_CONFIG_HOME"/nvidia/settings` |
| [openscad](http://www.openscad.org/) | `~/.OpenSCAD` | [7c3077b0f](https://github.com/openscad/openscad/commit/7c3077b0f) | [[73]](https://github.com/openscad/openscad/issues/125) | Does not fully honour XDG Base Directory Specification, see [[74]](https://github.com/openscad/openscad/issues/373)

Currently it [hard-codes](https://github.com/openscad/openscad/blob/master/src/PlatformUtils-posix.cc#L20) `~/.local/share`.

 |
| [OpenSSL](/index.php/OpenSSL "OpenSSL") | `~/.rnd` | Seeding file .rnd's location can be set with RANDFILE environment variable per [FAQ](https://www.openssl.org/docs/faq.html). |
| [pass](https://www.archlinux.org/packages/?name=pass) | `~/.password-store` | `$ export PASSWORD_STORE_DIR="$XDG_DATA_HOME"/pass` |
| [pidgin](https://www.archlinux.org/packages/?name=pidgin) | `~/.purple` | `$ pidgin --config="$XDG_DATA_HOME"/purple` |
| [PulseAudio](/index.php/PulseAudio "PulseAudio") | `~/.esd_auth` | Very likely generated by the `module-esound-protocol-unix.so` module. It can be configured to use a different location but it makes much more sense to just comment out this module in `/etc/pulse/default.pa` or `"$XDG_CONFIG_HOME"/pulse/default.pa`. |
| [python-setuptools](https://pypi.python.org/pypi/setuptools) | `~/.python-eggs` | `$ export PYTHON_EGG_CACHE="$XDG_CACHE_HOME"/python-eggs` |
| [readline](/index.php/Readline "Readline") | `~/.inputrc` | `$ export INPUTRC="$XDG_CONFIG_HOME"/readline/inputrc` |
| [rlwrap](http://utopia.knoware.nl/~hlub/uck/rlwrap/) | `~/.*_history` | [[75]](https://github.com/hanslub42/rlwrap/issues/25) | `$ export RLWRAP_HOME="$XDG_DATA_HOME"/rlwrap` |
| [sbt](http://www.scala-sbt.org/) | `~/.sbt`

`~/.ivy2`

 | `$ sbt -ivy "$XDG_DATA_HOME"/ivy2 -sbt-dir "$XDG_DATA_HOME"/sbt` |
| [screen](/index.php/Screen "Screen") | `~/.screenrc` | `$ export SCREENRC="$XDG_CONFIG_HOME"/screen/screenrc` |
| [stack](https://www.stackage.org/) | `~/.stack` | [[76]](https://github.com/commercialhaskell/stack/issues/342) | `$ export STACK_ROOT="$XDG_DATA_HOME"/stack` |
| [subversion](/index.php/Subversion "Subversion") | `~/.subversion` | [[77]](https://issues.apache.org/jira/browse/SVN-4599) [[78]](https://mail-archives.apache.org/mod_mbox/subversion-users/201204.mbox/%3c4F8FBCC6.4080205@ritsuka.org%3e)[[79]](http://mail-archives.apache.org/mod_mbox/subversion-dev/201509.mbox/%3c20150917222954.GA20331@teapot%3e) | `$ svn --config-dir "$XDG_CONFIG_HOME"/subversion` |
| [task](https://www.archlinux.org/packages/?name=task) | `~/.task`

`~/.taskrc`

 | `$ export TASKDATA="$XDG_DATA_HOME"/task`

`$ export TASKRC="$XDG_CONFIG_HOME"/task/taskrc`

 |
| [tig](http://jonas.nitro.dk/tig/) | `~/.tigrc` | `$ export TIGRC_USER="$XDG_CONFIG_HOME"/tig/tigrc` |
| [tiptop](http://tiptop.gforge.inria.fr/) | `~/.tiptoprc` | This will still expect the `.tiptoprc` file.

`$ tiptop -W "$XDG_CONFIG_HOME"/tiptop`

 |
| [tmux](/index.php/Tmux "Tmux") | `~/.tmux.conf` | [[80]](http://comments.gmane.org/gmane.comp.terminal-emulators.tmux.user/6013) [[81]](http://sourceforge.net/p/tmux/mailman/message/30619546/) | `$ tmux -f "$XDG_CONFIG_HOME"/tmux/tmux.conf`

`$ export TMUX_TMPDIR="$XDG_RUNTIME_DIR"`

 |
| [uncrustify](https://github.com/bengardner/uncrustify) | `~/.uncrustify.cfg` | `$ export UNCRUSTIFY_CONFIG="$XDG_CONFIG_HOME"/uncrustify/uncrustify.cfg` |
| [Unison](/index.php/Unison "Unison") | `~/.unison` | `$ export UNISON="$XDG_DATA_HOME"/unison` |
| [urxvtd](/index.php/Rxvt-unicode/Tips_and_tricks#Daemon-client "Rxvt-unicode/Tips and tricks") | `~/.urxvt/urxvtd-hostname` | `$ export RXVT_SOCKET="$XDG_RUNTIME_DIR"/urxvtd` |
| [WeeChat](/index.php/WeeChat "WeeChat") | `~/.weechat` | [[82]](http://savannah.nongnu.org/task/?10934) | `$ export WEECHAT_HOME="$XDG_CONFIG_HOME"/weechat`

`$ weechat -d "$XDG_CONFIG_HOME"/weechat`

 |
| [wget](/index.php/Wget "Wget") | `~/.wgetrc` | `$ export WGETRC="$XDG_CONFIG_HOME/wgetrc"` |
| [wine](/index.php/Wine "Wine") | `~/.wine` | [[83]](https://bugs.winehq.org/show_bug.cgi?id=20888) | [Winetricks](/index.php/Wine#Winetricks "Wine") uses XDG-alike location below for [WINEPREFIX](/index.php/Wine#WINEPREFIX "Wine") management:

`$ mkdir -p "$XDG_DATA_HOME"/wineprefixes`

`$ export WINEPREFIX="$XDG_DATA_HOME"/wineprefixes/default`

 |
| [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth) | `~/.Xauthority` | `$ export XAUTHORITY="$XDG_RUNTIME_DIR"/Xauthority` |
| [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit) | `~/.xinitrc`

`~/.xserverrc`

 | `$ export XINITRC="$XDG_CONFIG_HOME"/X11/xinitrc`

`$ export XSERVERRC="$XDG_CONFIG_HOME"/X11/xserverrc`

Note that these variables are respected by *xinit*, but not by *startx*.

 |
| [xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb) | `~/.Xresources`

`~/.Xdefaults`

 | Ultimately you [should be](http://superuser.com/questions/243914/xresources-or-xdefaults) using `Xresources` and since these resources are loaded via `xrdb` you can specify a path such as `$ xrdb -load ~/.config/X11/xresources`. |
| [xsel](http://www.vergenet.net/~conrad/software/xsel/) | `~/.xsel.log` | [[84]](https://github.com/kfish/xsel/issues/10) | `$ xsel --logfile "$XDG_CACHE_HOME"/xsel/xsel.log` |

## Hardcoded

| Application | Legacy Path | Discussion | Notes |
| [adb](/index.php/Adb "Adb") | `~/.android` |
| [AMule](/index.php/AMule "AMule") | `~/.aMule` |
| [Android Studio](https://developer.android.com/studio/index.html) | `~/.AndroidStudio2.3`

`~/.android`

`~/.java`

 |
| [anthy](https://osdn.net/projects/anthy/) | `~/.anthy` | [[85]](https://osdn.net/ticket/browse.php?group_id=14&tid=28397) |
| [Apache Directory Studio](https://directory.apache.org/studio/) | `~/.ApacheDirectoryStudio` |
| [Audacity](https://www.audacityteam.org/) | `~/.audacity-data` |
| [Avidemux](http://fixounet.free.fr/avidemux/) | `~/.avidemux6` |
| [bash](/index.php/Bash "Bash") | `~/.bashrc`

`~/.bash_history`

`~/.bash_profile`

`~/.bash_login`

`~/.bash_logout`

 | [[86]](http://savannah.gnu.org/support/?108134) | A specified `bashrc` can be sourced from `/etc/bashrc`

`$ export HISTFILE="$XDG_DATA_HOME"/bash/history`

 |
| [bazaar](/index.php/Bazaar "Bazaar") | `~/.bazaar`

`~/.bzr.log`

 |
| [cabal](https://www.haskell.org/cabal/) | `~/.cabal` | [[87]](https://github.com/haskell/cabal/issues/680) | See discussion for potential workarounds. It is not very easy or straightforward but may be possible to emulate Base Directory compliance. |
| [calibre](https://calibre-ebook.com/) | `~/Calibre Library` |
| [CUPS](/index.php/CUPS "CUPS") | `~/.cups` | [[88]](http://www.cups.org/str.php?L4243) |
| [darcs](/index.php/Darcs "Darcs") | `~/.darcs` | [[89]](http://bugs.darcs.net/issue2453) |
| [dbus](/index.php/Dbus "Dbus") | `~/.dbus` | [[90]](https://bugs.freedesktop.org/show_bug.cgi?id=35887) | This should be avoidable with kdbus [citation needed]. |
| [Dia](https://wiki.gnome.org/Apps/Dia) | `~/.dia` |
| [eclipse](/index.php/Eclipse "Eclipse") | `~/.eclipse` | [[91]](https://bugs.eclipse.org/bugs/show_bug.cgi?id=200809) | Option `-Dosgi.configuration.area=@user.home/.config/..` overrides but must be added to `"$ECLIPSE_HOME"/eclipse.ini"` rather than command line which means you must have write access to `$ECLIPSE_HOME`. (Arch Linux hard-codes `$ECLIPSE_HOME` in `/usr/bin/eclipse`) |
| [emacs](https://www.gnu.org/software/emacs/) | `~/.emacs`

`~/.emacs.d`

 | [[92]](http://debbugs.gnu.org/cgi/bugreport.cgi?bug=583) | It's possible to set `HOME`, but it has unexpected side effects. So far the most promising approach is modifying another Emacs environment variable to alter the load path and author your own site file which can manually load up your init file, but it changes the load process significantly. |
| [Fetchmail](http://www.fetchmail.info/) | `~/.fetchmailrc` |
| [Firefox](/index.php/Firefox "Firefox") | `~/.mozilla` | [[93]](https://bugzil.la/259356) |
| [GHC](https://www.haskell.org/ghc/) | `~/.ghc` | [[94]](https://ghc.haskell.org/trac/ghc/ticket/6077) |
| [GNU parallel](http://www.gnu.org/software/parallel/) | `~/.parallel` |
| [gtk-recordMyDesktop](http://recordmydesktop.sourceforge.net/about.php) | `~/.gtk-recordmydesktop` |
| [idris](http://www.idris-lang.org/) | `~/.idris` | [[95]](https://github.com/idris-lang/Idris-dev/pull/3456) |
| [julia](http://julialang.org/) | `~/.juliarc.jl`

`~/.julia_history`

 | [[96]](https://github.com/JuliaLang/julia/issues/4630) [[97]](https://github.com/JuliaLang/julia/issues/10016) |
| [Linux PAM](http://www.linux-pam.org/) | `~/.pam_environment` | Hardcoded in [modules/pam_env/pam_env.c](https://github.com/linux-pam/linux-pam/blob/master/modules/pam_env/pam_env.c) |
| [lldb](http://lldb.llvm.org/) | `~/.lldb`

`~/.lldbinit`

 |
| [mathomatic](http://www.mathomatic.org/) | `~/.mathomaticrc`

`~/.matho_history`

 | History can be moved by using `rlwrap mathomatic -r` with the `RLWRAP_HOME` environment set appropriately. |
| [milkytracker](http://www.milkytracker.org/) | `~/.milkytracker_config` | [[98]](https://github.com/Deltafire/MilkyTracker/issues/12) |
| [Minecraft](https://minecraft.net/) | `~/.minecraft` | [[99]](https://bugs.mojang.com/browse/MCL-2563) |
| [mongodb](https://www.mongodb.org/) | `~/.mongorc.js`

`~/.dbshell`

 | [[100]](https://jira.mongodb.org/browse/DOCS-5652?jql=text%20~%20%22.mongorc.js%22) | [This Stack Overflow thread](http://stackoverflow.com/a/22349050/4200039) suggests a partial workaround using command-line switch `--norc`. |
 `~/.netrc` | Like `~/.ssh`, many programs expect this file to be here. These include projects like curl (`CURLOPT_NETRC_FILE`), ftp (`NETRC`), s-nail (`NETRC`), etc. While some of them offer alternative configurable locations, many do not such as w3m, wget and lftp. |
| [NSS](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS) | `~/.pki` | [[101]](https://bugzilla.mozilla.org/show_bug.cgi?id=818686) |
| [OpenSSH](https://www.openssh.com/) | `~/.ssh` | [[102]](https://bugzilla.mindrot.org/show_bug.cgi?id=2050) | Assumed to be present by many ssh daemons and clients such as DropBear and OpenSSH. |
| [palemoon](https://www.palemoon.org/) | `~/.moonchild productions` | [[103]](https://forum.palemoon.org/viewtopic.php?f=5&t=9639) |
| [perf](https://perf.wiki.kernel.org/index.php/Main_Page) | `~/.debug` | Hardcoded in [tools/perf/util/config.c:18](https://github.com/torvalds/linux/blob/master/tools/perf/util/config.c#L18). |
| various [shells](/index.php/Shell "Shell") and [display managers](/index.php/Display_manager "Display manager") | `~/.profile` |
| [python](/index.php/Python "Python") | `~/.python_history` | All history from interactive sessions is saved to `~/.python_history` by default since [version 3.4](https://bugs.python.org/issue5845), custom path can still be set the same way as in older versions (see [this example](https://docs.python.org/3/library/readline.html?highlight=readline#example)). |
| [Qt Designer](https://doc.qt.io/qt-5/qtdesigner-manual.html) | `~/.designer` |
| [quodlibet](https://quodlibet.readthedocs.io/en/latest/) | `~/.quodlibet` |
| [racket](https://racket-lang.org/) | `~/.racketrc` |
| [RedNotebook](http://rednotebook.sourceforge.net/) | `~/.rednotebook` |
| [Remarkable](https://remarkableapp.github.io/linux.html) | `~/.remarkable` |
| [Scribus](https://www.scribus.net/) | `~/.scribus` |
| [SeaMonkey](http://www.seamonkey-project.org/) | `~/.mozilla` | [[104]](https://bugzil.la/726939) |
| [Skype](/index.php/Skype "Skype") < 5.0 | `~/.Skype` | [[105]](https://community.skype.com/t5/Linux-archive/Skype-violates-XDG-basedir-spec-on-linux/td-p/4175884) |
| [Solfege](https://www.gnu.org/software/solfege/solfege.html) | `~/.solfege`

`~/.solfegerc`

`~/lessonfiles`

 | [[106]](https://savannah.gnu.org/bugs/index.php?50251) |
| [SpamAssassin](https://spamassassin.apache.org/) | `~/.spamassassin` |
| [spectrwm](/index.php/Spectrwm "Spectrwm") | `~/.spectrwm` |
| [SQLite](/index.php/SQLite "SQLite") | `~/.sqlite_history`

`~/.sqliterc`

 | [[107]](https://unix.stackexchange.com/questions/306890/change-location-of-sqlite-history-file)[[108]](http://sqlite.1065341.n5.nabble.com/Customizing-the-location-of-the-sqlite-history-td87055.html) | `$ sqlite3 -init "$XDG_CONFIG_HOME"/sqlite3/sqliterc` |
| [Steam](/index.php/Steam "Steam") | `~/.steam` | [[109]](https://github.com/ValveSoftware/steam-for-linux/issues/1890) |
| [TeamSpeak](/index.php/TeamSpeak "TeamSpeak") | `~/.ts3client` |
| [TeXmacs](http://www.texmacs.org/) | `~/.TeXmacs` |
| [Thunderbird](/index.php/Thunderbird "Thunderbird") | `~/.thunderbird` | [[110]](https://bugzil.la/735285) |
| [tllocalmgr](https://git.archlinux.org/users/remy/texlive-localmanager.git/) | `~/.texlive` |
| [vim](/index.php/Vim "Vim") | `~/.vim`

`~/.vimrc`

`~/.viminfo`

 | Since [7.3.1178](https://github.com/vim/vim/commit/6a459902592e2a4ba68) vim will search for `~/.vim/vimrc` if `~/.vimrc` is not found.

`$ mkdir -p "$XDG_CACHE_HOME"/vim/{undo,swap,backup}`

 `"$XDG_CONFIG_HOME"/vim/vimrc` 
```
set undodir=$XDG_CACHE_HOME/vim/undo
set directory=$XDG_CACHE_HOME/vim/swap
set backupdir=$XDG_CACHE_HOME/vim/backup
set viminfo+='1000,n$XDG_CACHE_HOME/vim/viminfo
set runtimepath=$XDG_CONFIG_HOME/vim,$XDG_CONFIG_HOME/vim/after,$VIMRUNTIME

```
 `~/.profile` 
```
export VIMINIT=":source $XDG_CONFIG_HOME"/vim/vimrc

```

*   [https://tlvince.com/vim-respect-xdg](https://tlvince.com/vim-respect-xdg)

 |
| [vimperator](http://www.vimperator.org/) | `~/.vimperatorrc` | [[111]](http://www.mozdev.org/pipermail/vimperator/2009-October/004848.html) | `$ export VIMPERATOR_INIT=":source $XDG_CONFIG_HOME/vimperator/vimperatorrc"`

`$ export VIMPERATOR_RUNTIME="$XDG_CONFIG_HOME"/vimperator`

 |
| [wpa_cli](https://w1.fi/) | `~/.wpa_cli_history` |
| [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) | `~/.gnome` | For some reason the script `xdg-desktop-menu` hard-codes `gnome_user_dir="$HOME/.gnome/apps"`. This is used by [chromium](/index.php/Chromium "Chromium") amoung others. |
| [xombrero](https://opensource.conformal.com/wiki/xombrero) | `~/.xombrero` | [[112]](https://github.com/conformal/xombrero/issues/74) |
| [zsh](/index.php/Zsh "Zsh") | `~/.zshrc`

`~/.zprofile` `~/.zshenv`

`~/.zlogin` `~/.zlogout`

`~/.histfile`

 | [[113]](http://www.zsh.org/mla/workers/2013/msg00692.html) | Consider exporting `ZDOTDIR=$HOME/.config/zsh` in `~/.zshenv` (this is hardcoded due to the bootstrap problem). You could also add this to `/etc/zsh/zshenv` and avoid the need for any dotfiles in your `HOME`. Doing this however requires root privilege which may not be viable and is system-wide.

`$ export HISTFILE="$XDG_DATA_HOME"/zsh/history`

 |

## Library and language support

	C

	[C99: Cloudef's simple implementation](https://github.com/Cloudef/chck/tree/master/chck/xdg).

	Haskell

	Officially in [directory](https://hackage.haskell.org/package/directory) since 1.2.3.0 [ab9d0810ce](https://github.com/haskell/directory/commit/ab9d0810ce).

	[xdg-basedir](https://hackage.haskell.org/package/xdg-basedir)

	Perl

	[File-BaseDir](http://search.cpan.org/dist/File-BaseDir/lib/File/BaseDir.pm)

	[perl-file-xdg](https://github.com/Aerdan/perl-file-xdg)

	Python

	[pyxdg](http://freedesktop.org/wiki/Software/pyxdg/)

	Vala

	Builtin support via [GLib.Environment](http://valadoc.org/#!api=glib-2.0/GLib.Environment).

	See `get_user_cache_dir`, `get_user_data_dir`, `get_user_config_dir`, etc.

## See also

*   [GNOME Goal: XDG Base Directory Specification Usage](https://wiki.gnome.org/Initiatives/GnomeGoals/XDGConfigFolders)
*   [Rob Pike: "Dotfiles" being hidden is a UNIXv2 mistake](https://plus.google.com/+RobPikeTheHuman/posts/R58WgWwN9jp).
*   [systemd-path(1)](http://www.freedesktop.org/software/systemd/man/systemd-path.html)
*   [file-hierarchy(7)](http://www.freedesktop.org/software/systemd/man/file-hierarchy.html)
*   [Grawity's notes on dotfiles](https://github.com/grawity/dotfiles/blob/master/.dotfiles.notes).
*   [Grawity's notes on environment variables](https://github.com/grawity/dotfiles/blob/master/.environ.notes).
*   [ploum.net: Modify Your Application to use XDG Folders](https://ploum.net/207-modify-your-application-to-use-xdg-folders/).