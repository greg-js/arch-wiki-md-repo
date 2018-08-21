Related articles

*   [dotfiles](/index.php/Dotfiles "Dotfiles")
*   [XDG user directories](/index.php/XDG_user_directories "XDG user directories")

This article exists to catalog the growing set of software using the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html) introduced in 2003\. This is here to demonstrate the viability of this specification by listing commonly found dotfiles and their support status. For those not currently supporting the Base Directory Specification, workarounds will be demonstrated to emulate it instead.

The workarounds will be limited to anything not involving patching the source, executing code stored in [environment variables](/index.php/Environment_variables "Environment variables") or compile-time options. The rationale for this is that configurations should be portable across systems and having compile-time options prevent that.

Hopefully this will provide a source of information about exactly what certain kinds of dotfiles are and where they come from.

## Contents

*   [1 XDG Base Directory specification](#XDG_Base_Directory_specification)
    *   [1.1 User directories](#User_directories)
    *   [1.2 System directories](#System_directories)
*   [2 Contributing](#Contributing)
*   [3 Supported](#Supported)
*   [4 Partial](#Partial)
*   [5 Hardcoded](#Hardcoded)
    *   [5.1 Won't fix](#Won.27t_fix)
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

Nothing should require code evaluation (such as [vim](/index.php/Vim "Vim") and `VIMINIT`), patches or compile-time options to gain support and anything which does must be deemed hardcoded. Additionally if the process is too error prone or difficult, such as [Haskell's cabal](https://www.haskell.org/cabal/) or Eclipse, they should also be considered as hardcoded.

*   The first column should be either a link to an internal article, a [Template:Pkg](/index.php/Template:Pkg "Template:Pkg") or a [Template:AUR](/index.php/Template:AUR "Template:AUR").
*   The second column is for any legacy files and directories the project had (one per line), this is done so people can find them even if they are no longer read.
*   In the third, try to find the commit or version a project switched to XDG Base Directory or any open discussions and include them in the next two columns (two per line).
*   The last column should include any appropriate workarounds or solutions. Please verify that your solution is correct and functional.

## Supported

| Application | Legacy Path | Supported Since | Discussion | Notes |
| [aerc-git](https://aur.archlinux.org/packages/aerc-git/) |
| [antimicro](https://aur.archlinux.org/packages/antimicro/) | `~/.antimicro` | [edba864](https://github.com/Antimicro/antimicro/commit/edba864) | [[1]](https://github.com/Antimicro/antimicro/issues/5) |
| [aria2](/index.php/Aria2 "Aria2") | `~/.aria2` | [8bc1d37](https://github.com/tatsuhiro-t/aria2/commit/8bc1d37) | [[2]](https://github.com/tatsuhiro-t/aria2/issues/27) |
| [asunder](https://www.archlinux.org/packages/?name=asunder) | 

`~/.asunder
~/.asunder_album_artist
~/.asunder_album_genre
~/.asunder_album_title`

 | [2.9.0](https://littlesvr.ca/bugs/show_bug.cgi?id=31) | [[3]](https://littlesvr.ca/bugs/show_bug.cgi?id=52) | Uses `XDG_CONFIG_HOME/asunder/asunder` for `~/.asunder` and `XDG_CACHE_HOME/asunder/asunder_album_...` for the other 3 files. Legacy paths are not removed after migration, they have to be deleted manually. |
| [Blender](/index.php/Blender "Blender") | `~/.blender` | [4293f473](http://git.blender.org/gitweb/gitweb.cgi/blender.git/commit/4293f473) | [[4]](https://developer.blender.org/T28943) |
| [burp](https://github.com/falconindy/burp) | [f2388e9](https://github.com/falconindy/burp/commit/f2388e9) |
| [calibre](https://www.archlinux.org/packages/?name=calibre) |
| [Chromium](/index.php/Chromium "Chromium") | `~/.chromium` | [23057](https://src.chromium.org/viewvc/chrome?revision=23057&view=revision) | [[5]](https://groups.google.com/forum/#!topic/chromium-dev/QekVQxF3nho) [[6]](https://code.google.com/p/chromium/issues/detail?id=16976) |
| [citra-git](https://aur.archlinux.org/packages/citra-git/) | `~/.citra-emu` | [f7c3193fec](https://github.com/citra-emu/citra/commit/f7c3193fec) | [[7]](https://github.com/citra-emu/citra/pull/575) |
| [Composer](/index.php/PHP#Composer "PHP") | `~/.composer` | [1.0.0-beta1](https://github.com/composer/composer/releases/tag/1.0.0-beta1) | [[8]](https://github.com/composer/composer/pull/1407) |
| [cower](https://aur.archlinux.org/packages/cower/) | [8b70805](https://github.com/falconindy/cower/commit/8b70805) |
| [d-feet](https://www.archlinux.org/packages/?name=d-feet) | `~/.d-feet` | [7f6104b](https://git.gnome.org/browse/d-feet/commit/?id==7f6104b) |
| [dconf](https://www.archlinux.org/packages/?name=dconf) |
| [Dolphin emulator](/index.php/Dolphin_emulator "Dolphin emulator") | `~/.dolphin-emu` | [a498c68](https://github.com/dolphin-emu/dolphin/commit/a498c68) | [[9]](https://github.com/dolphin-emu/dolphin/pull/2304) |
| [dr14_tmeter](https://aur.archlinux.org/packages/dr14_tmeter/) | [7e777ca64](https://github.com/simon-r/dr14_t.meter/commit/7e777ca645298ec898b3c76e3ec472ed6ed43e8a) | [[10]](https://github.com/simon-r/dr14_t.meter/pull/30) | `XDG_CONFIG_HOME/dr14tmeter/` |
| [dunst](https://www.archlinux.org/packages/?name=dunst) | [78b6e2b1](https://github.com/knopwob/dunst/commit/78b6e2b1) | [[11]](https://github.com/knopwob/dunst/issues/22) |
| [dwb](/index.php/Dwb "Dwb") |
| [fish](/index.php/Fish "Fish") |
| [fontconfig](/index.php/Fontconfig "Fontconfig") | 

`~/.fontconfig
~/.fonts`

 | [8c255fb1](http://cgit.freedesktop.org/fontconfig/commit/?id=8c255fb1) | Use `"$XDG_DATA_HOME"/fonts` to store fonts instead. |
| [fontforge](https://www.archlinux.org/packages/?name=fontforge) | 

`~/.FontForge
~/.PfaEdit`

 | [e4c2cc7432](https://github.com/fontforge/fontforge/commit/e4c2cc7432) | [[12]](https://github.com/fontforge/fontforge/issues/847) [[13]](https://github.com/fontforge/fontforge/issues/991) |
| [freerdp](https://www.archlinux.org/packages/?name=freerdp) | `~/.freerdp` | [edf6e7258d](https://github.com/FreeRDP/FreeRDP/commit/edf6e7258d) |
| [Gajim](/index.php/Gajim "Gajim") | `~/.gajim` | [3e777ea](https://dev.gajim.org/gajim/gajim/commit/3e777ea8f120dc58d4e65ce501ab3ab3785a5d40) | [[14]](https://dev.gajim.org/gajim/gajim/issues/2149) |
| [gconf](https://www.archlinux.org/packages/?name=gconf) | `~/.gconf` | [fc28caa7](https://git.gnome.org/browse/gconf/commit/?id=fc28caa7) | [[15]](https://bugzilla.gnome.org/show_bug.cgi?id=674803) |
| [GIMP](/index.php/GIMP "GIMP") | 

`~/.gimp-x.y
~/.thumbnails`

 | [60e0cfe](https://git.gnome.org/browse/gimp/commit/?id=60e0cfe) [483505f](https://git.gnome.org/browse/gimp/commit/?id=483505f) | [[16]](https://bugzilla.gnome.org/show_bug.cgi?id=166643) [[17]](https://bugzilla.gnome.org/show_bug.cgi?id=646644) |
| [Git](/index.php/Git "Git") | `~/.gitconfig` | [0d94427e](https://github.com/git/git/commit/0d94427e) |
| [GStreamer](/index.php/GStreamer "GStreamer") | `~/.gstreamer-0.10` | [4e36f93924cf](http://cgit.freedesktop.org/gstreamer/gstreamer/commit/?id=4e36f93924cf) | [[18]](https://bugzilla.gnome.org/show_bug.cgi?id=518597) |
| [gtk3](/index.php/Gtk "Gtk") |
| [htop](https://www.archlinux.org/packages/?name=htop) | `~/.htoprc` | [93233a67](https://github.com/hishamhm/htop/commit/93233a67) |
| [i3](/index.php/I3 "I3") | `~/.i3` | [7c130fb54](http://code.stapelberg.de/git/i3/commit/?id=7c130fb54) |
| [i3status](https://www.archlinux.org/packages/?name=i3status) | `~/.i3status.conf` | [c3f7fc4994](http://code.stapelberg.de/git/i3status/commit/?id=c3f7fc4994) |
| [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) |
| [Inkscape](/index.php/Inkscape "Inkscape") | `~/.inkscape` | [0.47](http://wiki.inkscape.org/wiki/index.php/Release_notes/0.47#Preferences) | [[19]](https://bugs.launchpad.net/inkscape/+bug/199720) |
| [latexmk](https://www.ctan.org/pkg/latexmk?lang=en) | `~/.latexmkrc` |
| [lftp](https://www.archlinux.org/packages/?name=lftp) | `~/.lftp` | [21dc400](https://github.com/lavv17/lftp/commit/21dc400) | [[20]](https://www.mail-archive.com/lftp@uniyar.ac.ru/msg04301.html) |
| [lgogdownloader](https://aur.archlinux.org/packages/lgogdownloader/) | `~/.gogdownloader` | [d430af63d000](https://github.com/Sude-/lgogdownloader/commit/d430af63d000) | [[21]](https://github.com/Sude-/lgogdownloader/issues/4) |
| [LibreOffice](/index.php/LibreOffice "LibreOffice") | [a6f56f70](https://cgit.freedesktop.org/libreoffice/ure/commit/?id=a6f56f70a4930d3f71bd9c9b90fdd0ba20e4da5f) [25bd2eec](https://cgit.freedesktop.org/libreoffice/bootstrap/commit/?id=25bd2eec77ed774a37d1cddd0d72312e23d5e9fd) | [[22]](https://bugs.documentfoundation.org/show_bug.cgi?id=32263) |
| [Livestreamer](/index.php/Livestreamer "Livestreamer") | `~/.livestreamerrc` | [ea805917](https://github.com/chrippa/livestreamer/commit/ea805917) | [[23]](https://github.com/chrippa/livestreamer/pull/106) |
| [llpp](/index.php/Llpp "Llpp") | [3ab86f0cb](http://repo.or.cz/w/llpp.git/commit/3ab86f0cb) | Currently llpp places the configuration directly under `XDG_CONFIG_HOME` instead of creating a directory. |
| [mc](/index.php/Mc "Mc") | `~/.mc` | [1b9957058](https://www.midnight-commander.org/changeset/1b9957058) [0b7115647](https://www.midnight-commander.org/changeset/0b7115647)

[ce401d797](https://www.midnight-commander.org/changeset/ce401d797)

 | [[24]](https://www.midnight-commander.org/ticket/1851) |
| [Mercurial](/index.php/Mercurial "Mercurial") | `~/.hgrc` | [354020079723](https://www.mercurial-scm.org/repo/hg/rev/354020079723) [4.2](https://www.mercurial-scm.org/wiki/Release4.2) | `XDG_CONFIG_HOME/hg/hgrc`. |
| [mesa](https://www.archlinux.org/packages/?name=mesa) | [87ab26b2ab](https://cgit.freedesktop.org/mesa/mesa/commit/?id=87ab26b2ab35a29d446ae66f1795d40c184c0739) | `XDG_CACHE_HOME/mesa` |
| [milkytracker](https://www.archlinux.org/packages/?name=milkytracker) | `~/.milkytracker_config` | [eb487c55](https://github.com/Deltafire/MilkyTracker/commit/eb487c55) | [[25]](https://github.com/Deltafire/MilkyTracker/issues/12) |
| [mintty](https://github.com/mintty/mintty) | `~/.minttyrc` | [cff1bd8f](https://github.com/mintty/mintty/commit/cff1bd8f) v2.3.7. | [[26]](https://github.com/mintty/mintty/issues/525) |
| [mpd](/index.php/Mpd "Mpd") | `~/.mpdconf` | [87b73284](http://git.musicpd.org/cgit/master/mpd.git/commit/?id=87b73284) |
| [mpv](/index.php/Mpv "Mpv") | `~/.mpv` | [cb250d490](https://github.com/mpv-player/mpv/commit/cb250d490) | [[27]](https://github.com/mpv-player/mpv/pull/864) |
| [mutt](/index.php/Mutt "Mutt") | `~/.mutt` | [42fee7585f](https://dev.mutt.org/trac/changeset/42fee7585f) | [[28]](http://dev.mutt.org/trac/ticket/3207) |
| [mypaint](https://www.archlinux.org/packages/?name=mypaint) | `~/.mypaint` | [cf723b74cd](https://github.com/mypaint/mypaint/commit/cf723b74cd) |
| [nano](/index.php/Nano "Nano") | `~/.nano/` `~/.nanorc` | [036fc403](http://git.savannah.gnu.org/cgit/nano.git/commit/?id=c16e79b612eb8e061a4bd0b5f187c37a036fc403) | [[29]](https://savannah.gnu.org/patch/?8523) |
| [ncmpcpp](/index.php/Ncmpcpp "Ncmpcpp") | `~/.ncmpcpp` | [38d9f811](https://github.com/arybczak/ncmpcpp/commit/38d9f811de888e512b0115f551a9679eab4607f9) [27cd86e0](https://github.com/arybczak/ncmpcpp/commit/27cd86e0638bba3a7a78e44ac40dc98a58d1d90d) | [[30]](https://github.com/arybczak/ncmpcpp/issues/79) [[31]](https://github.com/arybczak/ncmpcpp/issues/110) | `ncmpcpp_directory` should be set to avoid an `error.log` file in `~/.ncmpcpp`. |
| [np2kai-git](https://aur.archlinux.org/packages/np2kai-git/) | 

`~/.config/np2kai
~/.config/xnp2kai`

 | [56a1cc2](https://github.com/AZO234/NP2kai/commit/56a1cc2f41e26e41c4dc341f33a0aff590cba0fa) | [Pull Request #50](https://github.com/AZO234/NP2kai/pull/50) |
| [Neovim](/index.php/Neovim "Neovim") | `~/.nvim`

`~/.nvimlog`

`~/.nviminfo`

 | [1ca5646bb](https://github.com/neovim/neovim/commit/1ca5646bb) | [[32]](https://github.com/neovim/neovim/issues/78) [[33]](https://github.com/neovim/neovim/pull/3198) |
| [newsbeuter](/index.php/Newsbeuter "Newsbeuter") | `~/.newsbeuter` | [3c57824c5](https://github.com/akrennmair/newsbeuter/commit/3c57824c5) | [[34]](https://github.com/akrennmair/newsbeuter/pull/39) | It is required to create both directories [[35]](http://newsbeuter.org/doc/newsbeuter.html#_xdg_base_directory_support):

`$ mkdir -p "$XDG_DATA_HOME"/newsbeuter "$XDG_CONFIG_HOME"/newsbeuter`

 |
| [NVIDIA](/index.php/NVIDIA "NVIDIA") | `~/.nv` |
| [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP") | `~/.offlineimaprc` | [5150de5](https://github.com/OfflineIMAP/offlineimap/commit/5150de5) | [[36]](https://github.com/OfflineIMAP/offlineimap/issues/32) |
| [opentyrian](https://aur.archlinux.org/packages/opentyrian/) | `~/.opentyrian` | [8d45ff2](https://bitbucket.org/opentyrian/opentyrian/commits/8d45ff2) | [[37]](https://web.archive.org/web/20140815181350/http://code.google.com/p/opentyrian/issues/detail?id=125) |
| [pcsx2](https://www.archlinux.org/packages/?name=pcsx2) | `~/.pcsx2` | [87f1e8f77](https://github.com/PCSX2/pcsx2/commit/87f1e8f77) [a9020c606](https://github.com/PCSX2/pcsx2/commit/a9020c606)

[3b22f0fb0](https://github.com/PCSX2/pcsx2/commit/3b22f0fb0) [0a012aec2](https://github.com/PCSX2/pcsx2/commit/0a012aec2)

 | [[38]](https://github.com/PCSX2/pcsx2/issues/352) [[39]](https://github.com/PCSX2/pcsx2/issues/381) |
| [pip](https://pip.pypa.io/) | `~/.pip` | [6.0](https://github.com/pypa/pip/blob/548a9136525815dff41acd845c558a0b36eb1c5f/NEWS.rst#60-2014-12-22) | [[40]](https://github.com/pypa/pip/issues/1733) |
| [powershell](https://aur.archlinux.org/packages/powershell/) | [6.0](https://docs.microsoft.com/en-us/powershell/scripting/whats-new/what-s-new-in-powershell-core-60#filesystem) |
| [ppsspp](https://www.archlinux.org/packages/?name=ppsspp) | `~/.ppsspp` | [132fe47c7d](https://github.com/hrydgard/ppsspp/commit/132fe47c7d) | [[41]](https://github.com/hrydgard/ppsspp/issues/4623) |
| [procps-ng](https://www.archlinux.org/packages/?name=procps-ng) | `~/.toprc` | [af53e170b9](https://gitlab.com/procps-ng/procps/commit/af53e170b9) | [[42]](https://gitlab.com/procps-ng/procps/merge_requests/38) [[43]](https://bugzilla.redhat.com/show_bug.cgi?id=1155265) |
| [orbment](https://github.com/Cloudef/orbment/) |
| [pacman](/index.php/Pacman "Pacman") | `~/.makepkg.conf` | [80eca94c8](https://projects.archlinux.org/pacman.git/commit/?id=80eca94c8) | [[44]](https://mailman.archlinux.org/pipermail/pacman-dev/2014-July/019178.html) |
| [Panda3D](https://github.com/panda3d/panda3d) | `~/.panda3d` | [2b537d2](https://github.com/panda3d/panda3d/commit/2b537d2) |
| [PulseAudio](/index.php/PulseAudio "PulseAudio") | 

`~/.pulse
~/.pulse-cookie`

 | [59a8618dcd9](http://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=59a8618dcd9) [87ae8307057](http://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=87ae8307057)

[9ab510a6921](http://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=9ab510a6921) [4c195bcc9d5](http://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=4c195bcc9d5)

 | [[45]](https://bugzilla.redhat.com/show_bug.cgi?id=845607) |
| [pyroom](http://pyroom.org/index.html) |
| [qutebrowser](/index.php/Qutebrowser "Qutebrowser") |
| [qtile](/index.php/Qtile "Qtile") | [fd8686e](https://github.com/qtile/qtile/commit/fd8686e5b4e4fa20bb82039ed8a83768434585ec) [66d704b](https://github.com/qtile/qtile/commit/66d704bce83f631b3326f10a1bc9fc22f8e6a6fd)

[51cff01](https://github.com/qtile/qtile/commit/51cff019917b87bda696b381493f969ceb6cc350)

 | [[46]](https://github.com/qtile/qtile/pull/835) | Some optional bar widgets can create files and directories in non-compliant paths, but most often these are still configurable. |
| [rclone](https://www.archlinux.org/packages/?name=rclone) | `~/.rclone.conf` | [9d362589](https://github.com/ncw/rclone/commit/9d362589) | [[47]](https://github.com/ncw/rclone/issues/868) |
| [retroarch](https://www.archlinux.org/packages/?name=retroarch) |
| [rr](https://aur.archlinux.org/packages/rr/) | `~/.rr` | [02e7d41e](https://github.com/mozilla/rr/commit/02e7d41e) | [[48]](https://github.com/mozilla/rr/issues/1455) |
| [rTorrent](/index.php/RTorrent "RTorrent") | `~/.rtorrent.rc` | [6a8d332b](https://github.com/rakshasa/rtorrent/commit/6a8d332b) |
| [Skype](https://www.skype.com/) | `~/.Skype` | 8.0 |
| [snes9x](https://www.archlinux.org/packages/?name=snes9x) | `~/.snes9x` | [19864677](https://github.com/snes9xgit/snes9x/commit/93b5f11641fa22d4518f251d6e3db99219864677) | [[49]](https://github.com/snes9xgit/snes9x/issues/194) | By default configuration is blank, is intended that the user fill it at they will (throw the gui or manually) before launch a rom |
| [sublime-text-dev](https://aur.archlinux.org/packages/sublime-text-dev/) | Cache is placed in `$XDG_CONFIG_HOME/sublime-text-3/Cache` instead of expected `$XDG_CACHE_HOME/sublime-text-3`. |
| [surfraw](/index.php/Surfraw "Surfraw") | 

`~/.surfraw.conf
~/.surfraw.bookmarks`

 | [3e4591d8](http://anonscm.debian.org/cgit/surfraw/surfraw.git/commit/?id=3e4591d8) [bd8c427d](http://anonscm.debian.org/cgit/surfraw/surfraw.git/commit/?id=bd8c427d)

[f57fc718](http://anonscm.debian.org/cgit/surfraw/surfraw.git/commit/?id=f57fc718)

 |
| [sway](/index.php/Sway "Sway") | `~/.sway/config` | [614393c09](https://github.com/SirCmpwn/sway/commit/614393c09) | [[50]](https://github.com/SirCmpwn/sway/issues/5) |
| [systemd](/index.php/Systemd "Systemd") |
| [termite](/index.php/Termite "Termite") |
| [tmuxinator](https://aur.archlinux.org/packages/tmuxinator/) | `~/.tmuxinator` | [2636923](https://github.com/tmuxinator/tmuxinator/pull/511/commits/263692349f1142c0edcacfbefae541cbc0e7b44e) | [[51]](https://github.com/tmuxinator/tmuxinator/pull/511) |
| [Transmission](/index.php/Transmission "Transmission") | `~/.transmission` | [5517](https://trac.transmissionbt.com/changeset/5517) | [[52]](https://trac.transmissionbt.com/ticket/684) |
| [util-linux](https://www.archlinux.org/packages/?name=util-linux) | [570b32100](http://git.kernel.org/cgit/utils/util-linux/util-linux.git/commit/?id=570b32100) |
| [Uzbl](/index.php/Uzbl "Uzbl") | [c6fd63a](https://github.com/uzbl/uzbl/commit/c6fd63a) | [[53]](https://github.com/uzbl/uzbl/pull/150) |
| [vimb](https://aur.archlinux.org/packages/vimb/) |
| [VirtualBox](/index.php/VirtualBox "VirtualBox") | `~/.VirtualBox` | [4.3](https://www.virtualbox.org/ticket/5099?action=diff&version=7) | [[54]](https://www.virtualbox.org/ticket/5099) |
| [vis](https://www.archlinux.org/packages/?name=vis) | `~/.vis` | [[55]](https://github.com/martanne/vis/pull/303) | [68a25c75](https://github.com/martanne/vis/commit/68a25c751c0219ef5df589a19513e46a08965d5a)

[d138908c](https://github.com/martanne/vis/commit/d138908cf8149eb10120957271cd6979272b4730)

 |
| [VLC](/index.php/VLC "VLC") | `~/.vlcrc` | [16f32e15](http://git.videolan.org/?p=vlc.git;a=commit;h=16f32e1500887c0dcd33cb06ad71759a81a52878) | [[56]](https://trac.videolan.org/vlc/ticket/1267) |
| [warsow](https://www.archlinux.org/packages/?name=warsow) | `~/.warsow-2.x` | [98ece3f](https://github.com/Qfusion/qfusion/commit/98ece3f) | [[57]](https://github.com/Qfusion/qfusion/issues/298) |
| [Wireshark](/index.php/Wireshark "Wireshark") | `~/.wireshark` | [b0b53fa5](https://code.wireshark.org/review/gitweb?p=wireshark.git;a=commit;h=b0b53fa5937aa7ba258427ca0f3581dba725230d) |
| [xsettingsd](https://aur.archlinux.org/packages/xsettingsd/) | `~/.xsettingsd` | [4ecd7be](https://github.com/derat/xsettingsd/commit/b4999f5e9e99224caf97d09f25ee731774ecd7be) |
| [xmonad](/index.php/Xmonad "Xmonad") | `~/.xmonad` | [40fc10b6](https://github.com/xmonad/xmonad/commit/40fc10b6a5682ce1d6ba7f0679962926ef6cfade) | [[58]](https://github.com/xmonad/xmonad/issues/61) [[59]](https://code.google.com/p/xmonad/issues/detail?id=484) | Alternatively the environments `XMONAD_CONFIG_HOME`, `XMONAD_DATA_HOME`, and `XMONAD_CACHE_HOME` are also available. |
| [xsel](https://www.archlinux.org/packages/?name=xsel) | `~/.xsel.log` | [ee7b4811](https://github.com/kfish/xsel/commit/ee7b48111be2e2117b201962e9d1c0e1f9804ed4) | [[60]](https://github.com/kfish/xsel/issues/10) |
| [yarn](https://www.archlinux.org/packages/?name=yarn) | 

`~/.yarnrc
~/.yarn/
~/.yarncache/
~/.yarn-config/`

 | [2d454b55](https://github.com/yarnpkg/yarn/commit/2d454b552d447a0f79a04e4e451e926e1c0a29e7) | [[61]](https://github.com/yarnpkg/yarn/pull/5336) |

## Partial

| Application | Legacy Path | Supported Since | Discussion | Notes |
| [abook](http://abook.sourceforge.net/) | `~/.abook` | `$ abook --config "$XDG_CONFIG_HOME"/abook/abookrc --datafile "$XDG_CACHE_HOME"/abook/addressbook` |
| [Anki](/index.php/Anki "Anki") | 

`~/Anki
~/Documents/Anki`

 | [[62]](https://github.com/dae/anki/pull/49) [[63]](https://github.com/dae/anki/pull/58) | `$ anki -b "$XDG_DATA_HOME"/Anki` |
| [aspell](/index.php/Aspell "Aspell") | `~/.aspell.conf` | `$ export ASPELL_CONF="per-conf $XDG_CONFIG_HOME/aspell/aspell.conf; personal $XDG_CONFIG_HOME/aspell/en.pws; repl $XDG_CONFIG_HOME/aspell/en.prepl"` |
| [Atom](/index.php/Atom "Atom") | `~/.atom` | [[64]](https://github.com/atom/atom/issues/8281) | `$ export ATOM_HOME="$XDG_DATA_HOME"/atom` |
| [aws-cli](https://www.archlinux.org/packages/?name=aws-cli) | `~/.aws` | [1.7.45](https://github.com/aws/aws-cli/commit/fc5961ea2cc0b5976ac9f777e20e4236fd7540f5) | [[65]](https://github.com/aws/aws-cli/issues/2433) | 

`$ export AWS_SHARED_CREDENTIALS_FILE="$XDG_CONFIG_HOME"/aws/credentials
$ export AWS_CONFIG_FILE="$XDG_CONFIG_HOME"/aws/config`

 |
| [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) | `~/.bash_completion` | `$ export BASH_COMPLETION_USER_FILE="$XDG_CONFIG_HOME"/bash-completion/bash_completion` |
| [bazaar](/index.php/Bazaar "Bazaar") | 

`~/.bazaar
~/.bzr.log`

 | [2.3.0](https://bugs.launchpad.net/bzr/+bug/195397/comments/15) | [[66]](https://bugs.launchpad.net/bzr/+bug/195397) | Discussion in upstream bug states that bazaar wil use `~/.config/bazaar` if it exists. The logfile `~/.bzr.log` might still be written. |
| [Ruby#Bundler](/index.php/Ruby#Bundler "Ruby") | `~/.bundle` | [[67]](https://github.com/bundler/bundler/pull/6024) [[68]](https://github.com/bundler/bundler/issues/4333) | `$ export BUNDLE_USER_CONFIG="$XDG_CONFIG_HOME"/bundle BUNDLE_USER_CACHE="$XDG_CACHE_HOME"/bundle BUNDLE_USER_PLUGIN="$XDG_DATA_HOME"/bundle` |
| [cargo](http://crates.io/) | `~/.cargo` | [[69]](https://github.com/rust-lang/cargo/issues/1734) [[70]](https://github.com/rust-lang/rfcs/pull/1615) [[71]](https://github.com/rust-lang/cargo/pull/5183) [[72]](https://github.com/rust-lang/cargo/pull/148) | `$ export CARGO_HOME="$XDG_DATA_HOME"/cargo` |
| [ccache](/index.php/Ccache "Ccache") | `~/.ccache` | `$ export CCACHE_DIR="$XDG_CACHE_HOME"/ccache` |
| [ChezScheme](https://github.com/cisco/ChezScheme) | `~/.chezscheme_history` | `$ petite --eehistory "$XDG_DATA_HOME"/chezscheme/history` |
| [conky](/index.php/Conky "Conky") | `~/.conkyrc` | [00481ee](https://github.com/brndnmtthws/conky/commit/00481ee9a97025e8e2acd7303d080af1948f7980) | [[73]](https://github.com/brndnmtthws/conky/issues/144) | `$ conky --config="$XDG_CONFIG_HOME"/conky/conkyrc` |
| [coreutils](/index.php/Coreutils "Coreutils") | `~/.dircolors` | `$ source "$(dircolors "$XDG_CONFIG_HOME"/dircolors)"` |
| [crawl](http://www.dungeoncrawl.org/) | `~/.crawl` | The trailing slash is required:

`$ export CRAWL_DIR="$XDG_DATA_HOME"/crawl/`

 |
| [CUDA](/index.php/CUDA "CUDA") | `~/.nv` | `$ export CUDA_CACHE_PATH="$XDG_CACHE_HOME"/nv` |
| [dict](/index.php/Dict "Dict") | `~/.dictrc` | `$ dict -c "$XDG_CONFIG_HOME"/dict/dictrc` |
| [Docker](/index.php/Docker "Docker") | `~/.docker` | `$ export DOCKER_CONFIG="$XDG_CONFIG_HOME"/docker` |
| [Docker Machine](https://docs.docker.com/machine/overview/) | `~/.docker/machine` | `$ export MACHINE_STORAGE_PATH="$XDG_DATA_HOME"/docker-machine` |
| [ELinks](/index.php/ELinks "ELinks") | `~/.elinks` | `$ export ELINKS_CONFDIR="$XDG_CONFIG_HOME"/elinks` |
| [emscripten](http://kripken.github.io/emscripten-site/) | 

`~/.emscripten
~/.emscripten_sanity
~/.emscripten_ports
~/.emscripten_cache__last_clear`

 | [[74]](https://github.com/kripken/emscripten/issues/3624) | 

`$ export EM_CONFIG="$XDG_CONFIG_HOME"/emscripten/config
$ export EM_CACHE="$XDG_CACHE_HOME"/emscripten/cache
$ export EM_PORTS="$XDG_DATA_HOME"/emscripten/cache
$ emcc --em-config "$XDG_CONFIG_HOME"/emscripten/config --em-cache "$XDG_CACHE_HOME"/emscripten/cache`

 |
| [freecad](https://www.freecadweb.org/) | `~/.FreeCAD` | [[75]](https://www.freecadweb.org/tracker/view.php?id=2956) | `$ freecad -u "$XDG_CONFIG_HOME"/FreeCAD/user.cfg -s "$XDG_CONFIG_HOME"/FreeCAD/system.cfg` |
| [gdb](http://www.gnu.org/software/gdb/) | `~/.gdbinit` | `$ gdb -nh -x "$XDG_CONFIG_HOME"/gdb/init` |
| [get_iplayer](https://github.com/get-iplayer/get_iplayer) | `~/.get_iplayer` | `$ export GETIPLAYERUSERPREFS="$XDG_DATA_HOME"/get_iplayer` |
| [getmail](/index.php/Getmail "Getmail") | `~/.getmail/getmailrc` | `$ getmail --rcfile="$XDG_CONFIG_HOME/getmail/getmailrc" --getmaildir="$XDG_DATA_HOME/getmail"` |
| [gliv](http://guichaz.free.fr/gliv/) | `~/.glivrc` | `$ gliv --glivrc="$XDG_CONFIG_HOME"/gliv/glivrc` |
| [GnuPG](/index.php/GnuPG "GnuPG") | `~/.gnupg` | [[76]](https://bugs.gnupg.org/gnupg/issue1456) [[77]](https://bugs.gnupg.org/gnupg/issue1018) | 

`$ export GNUPGHOME="$XDG_CONFIG_HOME"/gnupg
$ gpg2 --homedir "$XDG_CONFIG_HOME"/gnupg`

 |
| [Google Earth](/index.php/Google_Earth "Google Earth") | `~/.googleearth` | Some paths can be changed with the `KMLPath` and `CachePath` options in `~/.config/Google/GoogleEarthPlus.conf` |
| [GQ LDAP client](https://sourceforge.net/projects/gqclient) | 

`~/.gq
~/.gq-state`

 | [1.51](https://sourceforge.net/p/gqclient/mailman/message/2053978) | 

`$ export GQRC="$XDG_CONFIG_HOME"/gqrc
$ export GQSTATE="$XDG_DATA_HOME"/gq/gq-state
$ mkdir -p "$(dirname "$GQSTATE")"`

 |
| [gradle](https://gradle.org/) | `~/.gradle` | [[78]](https://discuss.gradle.org/t/be-a-nice-freedesktop-citizen-move-the-gradle-to-the-appropriate-location-in-linux/2199) | `$ export GRADLE_USER_HOME="$XDG_DATA_HOME"/gradle` |
| [gtk](/index.php/Gtk "Gtk") | `~/.gtkrc` | `$ export GTK_RC_FILES="$XDG_CONFIG_HOME"/gtk-1.0/gtkrc` |
| [gtk2](/index.php/Gtk "Gtk") | `~/.gtkrc-2.0` | `$ export GTK2_RC_FILES="$XDG_CONFIG_HOME"/gtk-2.0/gtkrc` |
| [httpie](http://httpie.org) | `~/.httpie` | [[79]](https://github.com/jakubroztocil/httpie/issues/145) | `$ export HTTPIE_CONFIG_DIR="$XDG_CONFIG_HOME"/httpie` |
| [ipython](http://ipython.org)/[jupyter](/index.php/Jupyter "Jupyter") | `~/.ipython` | 

`$ export IPYTHONDIR="$XDG_CONFIG_HOME"/jupyter
$ export JUPYTER_CONFIG_DIR="$XDG_CONFIG_HOME"/jupyter`

 |
| [irb](https://ruby-doc.org/stdlib/libdoc/irb/rdoc/IRB.html) | `~/.irbrc` |  `~/.profile`  `$ export IRBRC="$XDG_CONFIG_HOME"/irb/irbrc`  `"$XDG_CONFIG_HOME"/irb/irbrc` 
```
IRB.conf[:SAVE_HISTORY] ||= 1000
IRB.conf[:HISTORY_FILE] ||= File.join(ENV["XDG_DATA_HOME"], "irb", "history")
```
 |
| [irssi](/index.php/Irssi "Irssi") | `~/.irssi` | [[80]](https://github.com/irssi/irssi/pull/511) | `$ irssi --config="$XDG_CONFIG_HOME"/irssi/config --home="$XDG_DATA_HOME"/irssi` |
| [isync](/index.php/Isync "Isync") | `~/.mbsyncrc` | `$ mbsync -c "$XDG_CONFIG_HOME"/isync/mbsyncrc` |
| [Java](/index.php/Java "Java") (OpenJDK) | `~/.java/.userPrefs` | `$ export _JAVA_OPTIONS=-Djava.util.prefs.userRoot="$XDG_CONFIG_HOME"/java` |
| [less](/index.php/Core_utilities#less "Core utilities") | `~/.lesshst` | 

`$ mkdir -p "$XDG_CACHE_HOME"/less
$ export LESSKEY="$XDG_CONFIG_HOME"/less/lesskey
$ export LESSHISTFILE="$XDG_CACHE_HOME"/less/history`

`$ export LESSHISTFILE=-` can be used to disable this feature.

 |
| [libdvdcss](http://www.videolan.org/developers/libdvdcss.html) | `~/.dvdcss` | [[81]](https://mailman.videolan.org/pipermail/libdvdcss-devel/2014-August/001022.html) | `$ export DVDCSS_CACHE="$XDG_DATA_HOME"/dvdcss` |
| [libice](https://www.x.org/releases/current/doc/libICE/ice.html) | `~/.ICEauthority` | [[82]](https://bugs.freedesktop.org/show_bug.cgi?id=49173) | `$ export ICEAUTHORITY="$XDG_CACHE_HOME"/ICEauthority`

Make sure `XDG_CACHE_HOME` is set beforehand to directory user running [Xorg](/index.php/Xorg "Xorg") has write access to.

**Do not** use `XDG_RUNTIME_DIR` as it is available **after** login. Display managers that launch [Xorg](/index.php/Xorg "Xorg") (like [GDM](/index.php/GDM "GDM")) will repeatedly fail otherwise.

 |
| [libx11](/index.php/Xorg "Xorg") | 

`~/.XCompose
~/.compose-cache`

 | 

`$ export XCOMPOSEFILE="$XDG_CONFIG_HOME"/X11/xcompose
$ export XCOMPOSECACHE="$XDG_CACHE_HOME"/X11/xcompose`

 |
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
| [MOC](/index.php/MOC "MOC") | `~/.moc` | 

`$ mocp -M "$XDG_CONFIG_HOME"/moc
$ mocp -O MOCDir="$XDG_CONFIG_HOME"/moc`

 |
| [most](https://www.jedsoft.org/most/) | `~/.mostrc` | `$ export MOST_INITFILE="$XDG_CONFIG_HOME"/mostrc` |
| [MPlayer](/index.php/MPlayer "MPlayer") | `~/.mplayer` | `$ export MPLAYER_HOME="$XDG_CONFIG_HOME"/mplayer` |
| [msmtp](/index.php/Msmtp "Msmtp") | `~/.msmtprc` | `$ msmtp -C "$XDG_CONFIG_HOME"/msmtp/msmtprc` |
| [MySQL](/index.php/MySQL "MySQL") | `~/.mysql_history` | `$ export MYSQL_HISTFILE="$XDG_DATA_HOME"/mysql_history` |
| [ncurses](https://www.archlinux.org/packages/?name=ncurses) | `~/.terminfo` | Precludes system path searching:

`$ export TERMINFO="$XDG_DATA_HOME"/terminfo
$ export TERMINFO_DIRS="$XDG_DATA_HOME"/terminfo:/usr/share/terminfo`

 |
| [ncmpc](http://www.musicpd.org/clients/ncmpc/) | `~/.ncmpc` | `ncmpc -f "$XDG_CONFIG_HOME"/ncmpc/config` |
| [Netbeans](/index.php/Netbeans "Netbeans") | `~/.netbeans` | [[83]](https://netbeans.org/bugzilla/show_bug.cgi?id=215961) | `$ netbeans --userdir "${XDG_CONFIG_HOME}"/netbeans` |
| [Node.js](/index.php/Node.js "Node.js") | `~/.node_repl_history` | `$ export NODE_REPL_HISTORY="$XDG_DATA_HOME"/node_repl_history` [[84]](https://nodejs.org/api/repl.html#repl_environment_variable_options) |
| [notmuch](/index.php/Notmuch "Notmuch") | `~/.notmuch-config` | [[85]](http://notmuchmail.org/pipermail/notmuch/2011/007007.html) | 

`$ export NOTMUCH_CONFIG="$XDG_CONFIG_HOME"/notmuch/notmuchrc
$ export NMBGIT="$XDG_DATA_HOME"/notmuch/nmbug`

 |
| [npm](https://www.archlinux.org/packages/?name=npm) | 

`~/.npm
~/.npmrc`

 | [[86]](https://github.com/npm/npm/issues/6675) | `$ export NPM_CONFIG_USERCONFIG=$XDG_CONFIG_HOME/npm/npmrc` `npmrc` 
```
prefix=${XDG_DATA_HOME}/npm
cache=${XDG_CACHE_HOME}/npm
tmp=${XDG_RUNTIME_DIR}/npm
init-module=${XDG_CONFIG_HOME}/npm/config/npm-init.js

```

`prefix` is unnecessary (and unsupported) if Node.js is installed by [nvm](https://aur.archlinux.org/packages/nvm/).

 |
| [nvidia-settings](https://github.com/NVIDIA/nvidia-settings) | `~/.nvidia-settings-rc` | `$ nvidia-settings --config="$XDG_CONFIG_HOME"/nvidia/settings` |
| [nvm](https://aur.archlinux.org/packages/nvm/) | `~/.nvm` | `$ export NVM_DIR="$XDG_DATA_HOME"/nvm` |
| [Octave](/index.php/Octave "Octave") | 

`~/octave
~/.octave_packages
~/.octave_hist`

 | 

`$ export OCTAVE_HISTFILE="$XDG_CACHE_HOME/octave-hsts"
$ export OCTAVE_SITE_INITFILE="$XDG_CONFIG_HOME/octave/octaverc"`

 `$XDG_CONFIG_HOME/octave/octaverc` 
```
source /usr/share/octave/site/m/startup/octaverc;
pkg prefix ~/.local/share/octave/packages ~/.local/share/octave/packages;
pkg local_list /home/<your username>/.local/share/octave/octave_packages;

```

The `local_list` option must be given an absolute path.

 |
| [openscad](http://www.openscad.org/) | `~/.OpenSCAD` | [7c3077b0f](https://github.com/openscad/openscad/commit/7c3077b0f) | [[87]](https://github.com/openscad/openscad/issues/125) | Does not fully honour XDG Base Directory Specification, see [[88]](https://github.com/openscad/openscad/issues/373)

Currently it [hard-codes](https://github.com/openscad/openscad/blob/master/src/PlatformUtils-posix.cc#L20) `~/.local/share`.

 |
| [OpenSSL](/index.php/OpenSSL "OpenSSL") | `~/.rnd` | Seeding file .rnd's location can be set with RANDFILE environment variable per [FAQ](https://www.openssl.org/docs/faq.html). |
| [GNU parallel](http://www.gnu.org/software/parallel/) | `~/.parallel` | [20170422](https://git.savannah.gnu.org/cgit/parallel.git/commit/?id=685018f532f4e2d24b84eb28d5de3d759f0d1af1) | `$ export PARALLEL_HOME="$XDG_CONFIG_HOME"/parallel` |
| [Pass](/index.php/Pass "Pass") | `~/.password-store` | `$ export PASSWORD_STORE_DIR="$XDG_DATA_HOME"/pass` |
| [Pidgin](/index.php/Pidgin "Pidgin") | `~/.purple` | [[89]](https://developer.pidgin.im/ticket/4911) | `$ pidgin --config="$XDG_DATA_HOME"/purple` |
| [postgresql](https://www.postgresql.org/) | 

`~/.psqlrc
~/.psql_history
~/.pgpass
~/.pg_service.conf`

 | 9.2 | [[90]](https://www.postgresql.org/docs/current/static/app-psql.html) [[91]](https://www.postgresql.org/docs/current/static/libpq-envars.html) | 

`$ export PSQLRC="$XDG_CONFIG_HOME/pg/psqlrc"
$ export PSQL_HISTORY="$XDG_CACHE_HOME/pg/psql_history"
$ export PGPASSFILE="$XDG_CONFIG_HOME/pg/pgpass"
$ export PGSERVICEFILE="$XDG_CONFIG_HOME/pg/pg_service.conf"`

It is required to create both directories `$ mkdir "$XDG_CONFIG_HOME/pg" && mkdir "$XDG_CACHE_HOME/pg"`

 |
| [PulseAudio](/index.php/PulseAudio "PulseAudio") | `~/.esd_auth` | Very likely generated by the `module-esound-protocol-unix.so` module. It can be configured to use a different location but it makes much more sense to just comment out this module in `/etc/pulse/default.pa` or `"$XDG_CONFIG_HOME"/pulse/default.pa`. |
| [pylint](https://www.pylint.org/) | `~/.pylint.d` | [[92]](https://github.com/PyCQA/pylint/issues/1364) | `$ export PYLINTHOME="$XDG_CACHE_HOME"/pylint` |
| [python-setuptools](https://pypi.python.org/pypi/setuptools) | `~/.python-eggs` | `$ export PYTHON_EGG_CACHE="$XDG_CACHE_HOME"/python-eggs` |
| [readline](/index.php/Readline "Readline") | `~/.inputrc` | `$ export INPUTRC="$XDG_CONFIG_HOME"/readline/inputrc` |
| [rlwrap](http://utopia.knoware.nl/~hlub/uck/rlwrap/) | `~/.*_history` | [[93]](https://github.com/hanslub42/rlwrap/issues/25) | `$ export RLWRAP_HOME="$XDG_DATA_HOME"/rlwrap` |
| [RubyGems](https://rubygems.org/) | `~/.gem` | 

`$ export GEM_HOME="$XDG_DATA_HOME"/gem
$ export GEM_SPEC_CACHE="$XDG_CACHE_HOME"/gem`

 |
| [rustup](https://www.rustup.rs/) | `~/.rustup` | [[94]](https://github.com/rust-lang-nursery/rustup.rs/issues/247) | `$ export RUSTUP_HOME="$XDG_DATA_HOME"/rustup` |
| [sbt](http://www.scala-sbt.org/) | `~/.sbt`

`~/.ivy2`

 | [[95]](https://github.com/sbt/sbt/issues/3681) | `$ sbt -ivy "$XDG_DATA_HOME"/ivy2 -sbt-dir "$XDG_DATA_HOME"/sbt` (beware [[96]](https://github.com/sbt/sbt/issues/3598)) |
| [screen](/index.php/Screen "Screen") | `~/.screenrc` | `$ export SCREENRC="$XDG_CONFIG_HOME"/screen/screenrc` |
| [stack](https://www.stackage.org/) | `~/.stack` | [[97]](https://github.com/commercialhaskell/stack/issues/342) | `$ export STACK_ROOT="$XDG_DATA_HOME"/stack` |
| [subversion](/index.php/Subversion "Subversion") | `~/.subversion` | [[98]](https://issues.apache.org/jira/browse/SVN-4599) [[99]](https://mail-archives.apache.org/mod_mbox/subversion-users/201204.mbox/%3c4F8FBCC6.4080205@ritsuka.org%3e)[[100]](http://mail-archives.apache.org/mod_mbox/subversion-dev/201509.mbox/%3c20150917222954.GA20331@teapot%3e) | `$ svn --config-dir "$XDG_CONFIG_HOME"/subversion` |
| [task](https://www.archlinux.org/packages/?name=task) | 

`~/.task
~/.taskrc`

 | 

`$ export TASKDATA="$XDG_DATA_HOME"/task
$ export TASKRC="$XDG_CONFIG_HOME"/task/taskrc`

 |
| [tig](http://jonas.nitro.dk/tig/) | `~/.tigrc` | `$ export TIGRC_USER="$XDG_CONFIG_HOME"/tig/tigrc` |
| [tiptop](http://tiptop.gforge.inria.fr/) | `~/.tiptoprc` | This will still expect the `.tiptoprc` file.

`$ tiptop -W "$XDG_CONFIG_HOME"/tiptop`

 |
| [tmux](/index.php/Tmux "Tmux") | `~/.tmux.conf` | [[101]](http://comments.gmane.org/gmane.comp.terminal-emulators.tmux.user/6013) [[102]](http://sourceforge.net/p/tmux/mailman/message/30619546/) | `$ tmux -f "$XDG_CONFIG_HOME"/tmux/tmux.conf`

`$ export TMUX_TMPDIR="$XDG_RUNTIME_DIR"`

 |
| [uncrustify](https://github.com/bengardner/uncrustify) | `~/.uncrustify.cfg` | `$ export UNCRUSTIFY_CONFIG="$XDG_CONFIG_HOME"/uncrustify/uncrustify.cfg` |
| [Unison](/index.php/Unison "Unison") | `~/.unison` | `$ export UNISON="$XDG_DATA_HOME"/unison` |
| [urxvtd](/index.php/Rxvt-unicode/Tips_and_tricks#Daemon-client "Rxvt-unicode/Tips and tricks") | `~/.urxvt/urxvtd-hostname` | `$ export RXVT_SOCKET="$XDG_RUNTIME_DIR"/urxvtd` |
| [Vagrant](/index.php/Vagrant "Vagrant") | 

`~/.vagrant.d
~/.vagrant.d/aliases`

 | [[103]](https://www.vagrantup.com/docs/other/environmental-variables.html) | 

`$ export VAGRANT_HOME="$XDG_DATA_HOME"/vagrant
$ export VAGRANT_ALIAS_FILE="$XDG_DATA_HOME"/vagrant/aliases`

 |
| [WeeChat](/index.php/WeeChat "WeeChat") | `~/.weechat` | [[104]](http://savannah.nongnu.org/task/?10934) | 

`$ export WEECHAT_HOME="$XDG_CONFIG_HOME"/weechat
$ weechat -d "$XDG_CONFIG_HOME"/weechat`

 |
| [wget](/index.php/Wget "Wget") | 

`~/.wgetrc
~/.wget-hsts`

 | 

`$ export WGETRC="$XDG_CONFIG_HOME/wgetrc"
$ wget --hsts-file="$XDG_CACHE_HOME/wget-hsts"`

 |
| [wine](/index.php/Wine "Wine") | `~/.wine` | [[105]](https://bugs.winehq.org/show_bug.cgi?id=20888) | [Winetricks](/index.php/Wine#Winetricks "Wine") uses XDG-alike location below for [WINEPREFIX](/index.php/Wine#WINEPREFIX "Wine") management:

`$ mkdir -p "$XDG_DATA_HOME"/wineprefixes
$ export WINEPREFIX="$XDG_DATA_HOME"/wineprefixes/default`

 |
| [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth) | `~/.Xauthority` | `$ export XAUTHORITY="$XDG_RUNTIME_DIR"/Xauthority` |
| [xinit](/index.php/Xinit "Xinit") | 

`~/.xinitrc
~/.xserverrc`

 | 

`$ export XINITRC="$XDG_CONFIG_HOME"/X11/xinitrc
$ export XSERVERRC="$XDG_CONFIG_HOME"/X11/xserverrc`

Note that these variables are respected by *xinit*, but not by *startx*. Instead, specify the filename as an argument:

`$ startx "$XDG_CONFIG_HOME/X11/xinitrc" -- vt1`

 |
| [xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb) | 

`~/.Xresources
~/.Xdefaults`

 | Ultimately you [should be](http://superuser.com/questions/243914/xresources-or-xdefaults) using `Xresources` and since these resources are loaded via `xrdb` you can specify a path such as `$ xrdb -load ~/.config/X11/xresources`. |

## Hardcoded

| Application | Legacy Path | Discussion | Notes |
| [adb](/index.php/Adb "Adb") | `~/.android/` | [[106]](https://developer.android.com/studio/command-line/variables.html#android_sdk_root) | `$ export ANDROID_SDK_HOME="$XDG_CONFIG_HOME"/android` |
| [AMule](/index.php/AMule "AMule") | `~/.aMule` |
| [Android Studio](https://developer.android.com/studio/index.html) | 

`~/.AndroidStudio2.3
~/.android/
~/.java/`

 |
| [anthy](https://osdn.net/projects/anthy/) | `~/.anthy` | [[107]](https://osdn.net/ticket/browse.php?group_id=14&tid=28397) |
| [Apache Directory Studio](https://directory.apache.org/studio/) | `~/.ApacheDirectoryStudio` |
| [ARandR](https://christian.amsuess.com/tools/arandr/) | `~/.screenlayout` |
| [Audacity](https://www.audacityteam.org/) | `~/.audacity-data/` |
| [Avidemux](http://fixounet.free.fr/avidemux/) | `~/.avidemux6` |
| [cabal](https://www.haskell.org/cabal/) | `~/.cabal/` | [[108]](https://github.com/haskell/cabal/issues/680) | See discussion for potential workarounds. It is not very easy or straightforward but may be possible to emulate Base Directory compliance. |
| [chatty](https://aur.archlinux.org/packages/chatty/) | `~/.chatty/` | [[109]](https://github.com/chatty/chatty/issues/273) |
| [cryptomator](https://aur.archlinux.org/packages/cryptomator/) | `~/.Cryptomator` | [[110]](https://github.com/cryptomator/cryptomator/issues/710) |
| [darcs](/index.php/Darcs "Darcs") | `~/.darcs/` | [[111]](http://bugs.darcs.net/issue2453) |
| [dbus](/index.php/Dbus "Dbus") | `~/.dbus/` | [[112]](https://bugs.freedesktop.org/show_bug.cgi?id=35887) | This should be avoidable with kdbus [citation needed]. |
| [Dia](https://wiki.gnome.org/Apps/Dia) | `~/.dia/` |
| [eclipse](/index.php/Eclipse "Eclipse") | `~/.eclipse/` | [[113]](https://bugs.eclipse.org/bugs/show_bug.cgi?id=200809) | Option `-Dosgi.configuration.area=@user.home/.config/..` overrides but must be added to `"$ECLIPSE_HOME"/eclipse.ini"` rather than command line which means you must have write access to `$ECLIPSE_HOME`. (Arch Linux hard-codes `$ECLIPSE_HOME` in `/usr/bin/eclipse`) |
| [emacs](https://www.gnu.org/software/emacs/) | 

`~/.emacs
~/.emacs.d/`

 | [[114]](http://debbugs.gnu.org/cgi/bugreport.cgi?bug=583) | It's possible to set `HOME`, but it has unexpected side effects. So far the most promising approach is modifying another Emacs environment variable to alter the load path and author your own site file which can manually load up your init file, but it changes the load process significantly. |
| [Fetchmail](http://www.fetchmail.info/) | `~/.fetchmailrc` |
| [Firefox](/index.php/Firefox "Firefox") | `~/.mozilla/` | [[115]](https://bugzil.la/259356) |
| [GHC](https://www.haskell.org/ghc/) | `~/.ghc` | [[116]](https://ghc.haskell.org/trac/ghc/ticket/6077) |
| [Goldendict](/index.php/Goldendict "Goldendict") | `~/.goldendict/` | [[117]](https://github.com/goldendict/goldendict/issues/151) |
| [gramps](https://www.archlinux.org/packages/?name=gramps) | `~/.gramps/` | [[118]](https://gramps-project.org/bugs/view.php?id=8025) |
| [grsync](https://www.archlinux.org/packages/?name=grsync) | `~/.grsync/` | [[119]](https://sourceforge.net/p/grsync/feature-requests/15/) |
| [gtk-recordMyDesktop](http://recordmydesktop.sourceforge.net/about.php) | `~/.gtk-recordmydesktop` |
| [hplip](https://www.archlinux.org/packages/?name=hplip) | `~/.hplip/` | [https://bugs.launchpad.net/hplip/+bug/307152](https://bugs.launchpad.net/hplip/+bug/307152) |
| [idris](http://www.idris-lang.org/) | `~/.idris` | [[120]](https://github.com/idris-lang/Idris-dev/pull/3456) |
| [Java](/index.php/Java "Java") (OpenJDK) | `~/.java/fonts`, `~/.java/webview` | [[121]](https://bugzilla.redhat.com/show_bug.cgi?id=1154277) |
| [julia](http://julialang.org/) | 

`~/.juliarc.jl
~/.julia_history`

 | [[122]](https://github.com/JuliaLang/julia/issues/4630) [[123]](https://github.com/JuliaLang/julia/issues/10016) |
| [Linux PAM](http://www.linux-pam.org/) | `~/.pam_environment` | [[124]](https://github.com/linux-pam/linux-pam/issues/7) | Hardcoded in [modules/pam_env/pam_env.c](https://github.com/linux-pam/linux-pam/blob/master/modules/pam_env/pam_env.c) |
| [lldb](http://lldb.llvm.org/) | 

`~/.lldb
~/.lldbinit`

 |
| [mathomatic](http://www.mathomatic.org/) | 

`~/.mathomaticrc
~/.matho_history`

 | History can be moved by using `rlwrap mathomatic -r` with the `RLWRAP_HOME` environment set appropriately. |
| [Minecraft](https://minecraft.net/) | `~/.minecraft/` | [[125]](https://bugs.mojang.com/browse/MCL-2563) |
| [mongodb](https://www.mongodb.org/) | 

`~/.mongorc.js
~/.dbshell`

 | [[126]](https://jira.mongodb.org/browse/DOCS-5652?jql=text%20~%20%22.mongorc.js%22) | [This Stack Overflow thread](http://stackoverflow.com/a/22349050/4200039) suggests a partial workaround using command-line switch `--norc`. |
 `~/.netrc` | Like `~/.ssh`, many programs expect this file to be here. These include projects like curl (`CURLOPT_NETRC_FILE`), ftp (`NETRC`), s-nail (`NETRC`), etc. While some of them offer alternative configurable locations, many do not such as w3m, wget and lftp. |
| [node-gyp](https://github.com/nodejs/node-gyp) | `~/.node-gyp` | [[127]](https://github.com/nodejs/node-gyp/issues/175) [[128]](https://github.com/nodejs/node-gyp/issues/21) [[129]](https://github.com/nodejs/node-gyp/issues/1124) | Discussion seems as though partial support may soon be added. |
| [NSS](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS) | `~/.pki` | [[130]](https://bugzilla.mozilla.org/show_bug.cgi?id=818686) |
| [palemoon](https://www.palemoon.org/) | `~/.moonchild productions` | [[131]](https://forum.palemoon.org/viewtopic.php?f=5&t=9639) |
| [perf](https://perf.wiki.kernel.org/index.php/Main_Page) | `~/.debug` | Hardcoded in [tools/perf/util/config.c:29](https://github.com/torvalds/linux/blob/master/tools/perf/util/config.c#L29). |
| various [shells](/index.php/Shell "Shell") and [display managers](/index.php/Display_manager "Display manager") | `~/.profile` |
| [python](/index.php/Python "Python") | `~/.python_history` | All history from interactive sessions is saved to `~/.python_history` by default since [version 3.4](https://bugs.python.org/issue5845), custom path can still be set the same way as in older versions (see [this example](https://docs.python.org/3/library/readline.html?highlight=readline#example)). |
| [Qt Designer](https://doc.qt.io/qt-5/qtdesigner-manual.html) | `~/.designer` |
| [Quod Libet](https://quodlibet.readthedocs.io/en/latest/) | `~/.quodlibet` | [[132]](https://github.com/quodlibet/quodlibet/issues/138) |
| [racket](https://racket-lang.org/) | `~/.racketrc` |
| [RedNotebook](http://rednotebook.sourceforge.net/) | `~/.rednotebook` |
| [Remarkable](https://remarkableapp.github.io/linux.html) | `~/.remarkable` |
| [Ren'Py](https://www.renpy.org/) | `~/.renpy` | [[133]](https://github.com/renpy/renpy/issues/1377) |
| [SANE](/index.php/SANE "SANE") | `~/.sane/` | `scanimage` creates a `.cal` file there |
| [Scribus](https://www.scribus.net/) | `~/.scribus` |
| [SeaMonkey](http://www.seamonkey-project.org/) | `~/.mozilla/` | [[134]](https://bugzil.la/726939) |
| [Solfege](https://www.gnu.org/software/solfege/solfege.html) | 

`~/.solfege
~/.solfegerc
~/lessonfiles`

 | [[135]](https://savannah.gnu.org/bugs/index.php?50251) |
| [SpamAssassin](https://spamassassin.apache.org/) | `~/.spamassassin` |
| [spectrwm](/index.php/Spectrwm "Spectrwm") | `~/.spectrwm` |
| [SQLite](/index.php/SQLite "SQLite") | 

`~/.sqlite_history
~/.sqliterc`

 | [[136]](https://unix.stackexchange.com/questions/306890/change-location-of-sqlite-history-file)[[137]](http://sqlite.1065341.n5.nabble.com/Customizing-the-location-of-the-sqlite-history-td87055.html) | `$ sqlite3 -init "$XDG_CONFIG_HOME"/sqlite3/sqliterc` |
| [Steam](/index.php/Steam "Steam") | 

`~/.steam
~/.steampath
~/.steampid`

 | [[138]](https://github.com/ValveSoftware/steam-for-linux/issues/1890) | Many game engines (Unity 3D, Unreal) follow the specification, but then individual game publishers hardcode the paths in [Steam Auto-Cloud](https://www.ctrl.blog/entry/flatpak-steamcloud-xdg) causing game-saves to sync to the wrong directory. |
| [TeamSpeak](/index.php/TeamSpeak "TeamSpeak") | `~/.ts3client` |
| [TeXmacs](http://www.texmacs.org/) | `~/.TeXmacs` |
| [Thunderbird](/index.php/Thunderbird "Thunderbird") | `~/.thunderbird/` | [[139]](https://bugzil.la/735285) |
| [tllocalmgr](https://git.archlinux.org/users/remy/texlive-localmanager.git/) | `~/.texlive` |
| [vim](/index.php/Vim "Vim") | 

`~/.vim
~/.vimrc
~/.viminfo`

 | Since [7.3.1178](https://github.com/vim/vim/commit/6a459902592e2a4ba68) vim will search for `~/.vim/vimrc` if `~/.vimrc` is not found.

`$ mkdir -p "$XDG_CACHE_HOME"/vim/{undo,swap,backup}`

 `"$XDG_CONFIG_HOME"/vim/vimrc` 
```
set undodir=$XDG_CACHE_HOME/vim/undo
set directory=$XDG_CACHE_HOME/vim/swap
set backupdir=$XDG_CACHE_HOME/vim/backup
set viminfo+='1000,n$XDG_CACHE_HOME/vim/viminfo
set runtimepath=$XDG_CONFIG_HOME/vim,$VIMRUNTIME,$XDG_CONFIG_HOME/vim/after

```
 `~/.profile` 
```
export VIMINIT=":source $XDG_CONFIG_HOME"/vim/vimrc

```

*   [https://tlvince.com/vim-respect-xdg](https://tlvince.com/vim-respect-xdg)

 |
| [vimperator](http://www.vimperator.org/) | `~/.vimperatorrc` | [[140]](http://www.mozdev.org/pipermail/vimperator/2009-October/004848.html) | `$ export VIMPERATOR_INIT=":source $XDG_CONFIG_HOME/vimperator/vimperatorrc"`

`$ export VIMPERATOR_RUNTIME="$XDG_CONFIG_HOME"/vimperator`

 |
| [w3m](https://www.archlinux.org/packages/?name=w3m) | `~/.w3m` | [[141]](https://sourceforge.net/p/w3m/feature-requests/31/) |
| [wpa_cli](https://w1.fi/) | `~/.wpa_cli_history` |
| [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) | `~/.gnome` | [[142]](https://bugs.freedesktop.org/show_bug.cgi?id=90775) | For some reason the script `xdg-desktop-menu` hard-codes `gnome_user_dir="$HOME/.gnome/apps"`. This is used by [chromium](/index.php/Chromium "Chromium") amoung others. |
| [xombrero](https://opensource.conformal.com/wiki/xombrero) | `~/.xombrero` | [[143]](https://github.com/conformal/xombrero/issues/74) |
| [zenmap](https://nmap.org/zenmap/) [nmap](https://www.archlinux.org/packages/?name=nmap) | `~/.zenmap` | [[144]](http://seclists.org/nmap-dev/2012/q2/163) [[145]](https://github.com/nmap/nmap/issues/590) |
| [zsh](/index.php/Zsh "Zsh") | 

`~/.zshrc
~/.zprofile
~/.zshenv
~/.zlogin
~/.zlogout
~/.histfile`

 | [[146]](http://www.zsh.org/mla/workers/2013/msg00692.html) | Consider exporting `ZDOTDIR=$HOME/.config/zsh` in `~/.zshenv` (this is hardcoded due to the bootstrap problem). You could also add this to `/etc/zsh/zshenv` and avoid the need for any dotfiles in your `HOME`. Doing this however requires root privilege which may not be viable and is system-wide.

`$ export HISTFILE="$XDG_DATA_HOME"/zsh/history`

 |

### Won't fix

| Application | Legacy Path | Discussion | Notes |
| [Arduino](/index.php/Arduino "Arduino") | 

`~/.arduino15
~/.jssc`

 | [[147]](https://github.com/arduino/Arduino/issues/3915) |
| [bash](/index.php/Bash "Bash") | 

`~/.bashrc
~/.bash_history
~/.bash_profile
~/.bash_login
~/.bash_logout`

 | [[148]](http://savannah.gnu.org/support/?108134) | `$ export HISTFILE="$XDG_DATA_HOME"/bash/history`

A specified `bashrc` can be sourced from `/etc/bashrc`.

Specify `--init-file <file>` as an alternative to `~/.bashrc` for interactive shells.

 |
| [CUPS](/index.php/CUPS "CUPS") | `~/.cups/` | [[149]](http://www.cups.org/str.php?L4243) |
| [Flatpak](/index.php/Flatpak "Flatpak") | `~/.var/` | [[150]](https://github.com/flatpak/flatpak/issues/46) [[151]](https://github.com/flatpak/flatpak.github.io/issues/191) [[152]](https://github.com/flatpak/flatpak/issues/1651) |
| [Minetest](/index.php/Minetest "Minetest") | `~/.minetest/` | [[153]](https://github.com/minetest/minetest/issues/864) |
| [OpenSSH](https://www.openssh.com/) | `~/.ssh` | [[154]](https://bugzilla.mindrot.org/show_bug.cgi?id=2050) | Assumed to be present by many ssh daemons and clients such as DropBear and OpenSSH. |
| [Nestopia UE](http://0ldsk00l.ca/nestopia/) | `~/.nestopia/` | [[155]](https://github.com/0ldsk00l/nestopia/pull/292) |

## Library and language support

	C

	[C99: Cloudef's simple implementation](https://github.com/Cloudef/chck/tree/master/chck/xdg).

	JVM

	Java, Kotlin, Clojure, Scala, ...

	[directories-jvm](https://github.com/soc/directories-jvm)

	Go

	[go-appdir](https://github.com/ProtonMail/go-appdir)

	Haskell

	Officially in [directory](https://hackage.haskell.org/package/directory) since 1.2.3.0 [ab9d0810ce](https://github.com/haskell/directory/commit/ab9d0810ce).

	[xdg-basedir](https://hackage.haskell.org/package/xdg-basedir)

	Perl

	[File-BaseDir](http://search.cpan.org/dist/File-BaseDir/lib/File/BaseDir.pm)

	[perl-file-xdg](https://github.com/Aerdan/perl-file-xdg)

	Ruby

	[rubyworks/xdg](https://github.com/rubyworks/xdg)

	Rust

	[directories-rs](https://github.com/soc/directories-rs)

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