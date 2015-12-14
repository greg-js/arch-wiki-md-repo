# XDG Base Directory support

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [dotfiles](/index.php/Dotfiles "Dotfiles")
*   [Xdg user directories](/index.php/Xdg_user_directories "Xdg user directories")

This article exists to catalog the growing set of software using the [XDG Base Directory Specification](http://standards.freedesktop.org/basedir-spec/latest/) introduced in 2003\. This is here to demonstrate the viability of this specification by listing commonly found dotfiles and their support status. For those not currently supporting the Base Directory Specification, workarounds will be demonstrated to emulate it instead.

The workarounds will be limited to anything not involving patching the source, executing code stored in [environment variables](/index.php/Environment_variable "Environment variable") or compile-time options. The rationale for this is that configurations should be portable across systems and having compile-time options prevent that.

Hopefully this will provide a source of information about exactly what certain kinds of dotfiles are and where they come from.

## Contents

*   [1 The XDG Base Directory Specification](#The_XDG_Base_Directory_Specification)
    *   [1.1 User Directories](#User_Directories)
    *   [1.2 System Directories](#System_Directories)
*   [2 Exceptions](#Exceptions)
*   [3 Contributing](#Contributing)
*   [4 Supported](#Supported)
*   [5 Partial](#Partial)
*   [6 Hardcoded](#Hardcoded)
*   [7 Library and Language Support](#Library_and_Language_Support)
*   [8 See also](#See_also)

## The XDG Base Directory Specification

Please read the [full specification](http://standards.freedesktop.org/basedir-spec/latest/). This section will attempt to break down the essence of what it tries to achieve.

None of the `XDG_` environments should be set by default except some systems do set `XDG_RUNTIME_DIR` such as systemd (logind).

All paths defined must be absolute and valid.

### User Directories

*   `XDG_CONFIG_HOME`
    *   Defaults to `HOME/.config`
    *   Where user-specific configurations should be written. (Like `/etc`)

*   `XDG_CACHE_HOME`
    *   Defaults to `HOME/.cache`
    *   Where user-specific non-essential (cached) data should be written. (Like `/var/cache`)

*   `XDG_DATA_HOME`
    *   Defaults to `HOME/.local/share`
    *   Where user-specific data files should be written. (Like `/usr/share`)

*   `XDG_RUNTIME_DIR`
    *   Used for non-essential, user-specific data files such as sockets, named pipes, etc.
    *   Defaults to nothing, warnings should be issued if not set or equivalents provided.
    *   Must be owned by the user with an access mode of `0700`.
    *   Filesystem fully featured by standards of OS.
    *   Must be on the local filesystem.
    *   May be subject to periodic cleanup.
    *   Modified every 6 hours or set sticky bit if persistence is desired.
    *   Can only exist for the duration of the user's login.
    *   Should not store large files as it may be mounted as a tmpfs.

### System Directories

*   `XDG_DATA_DIRS`
    *   List of directories seperated by `:` (Like `PATH`)
    *   Defaults to `/usr/local/share:/usr/share`

*   `XDG_CONFIG_DIRS`
    *   List of directories seperated by `:` (Like `PATH`)
    *   Defaults to `/etc/xdg`

## Exceptions

These directories and files are unlikely to ever change, there is far too much historical baggage and most tools written expect these files and directories to exist in these locations.

While some of these tools are still in active development and maintainence, the developers are unwilling to accommodate for the necessary changes due to the aforementioned reasons.

`~/.ssh`

Assumed to be present by many ssh daemons and clients such as DropBear and OpenSSH. [OpenSSH Bug 2050](https://bugzilla.mindrot.org/show_bug.cgi?id=2050)

`~/.pki`

Part of Mozilla's [NSS Project](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS).

`~/.netrc`

Like `~/.ssh`, many programs expect this file to be here. These include projects like curl (`CURLOPT_NETRC_FILE`), ftp (`NETRC`), s-nail (`NETRC`), etc. While some of them offer alternative configurable locations, many do not such as w3m, wget and lftp.

`~/.profile`

Used by the various shells and display managers, this file is expected to be here much like `~/.netrc`.

## Contributing

When contributing make sure to use the correct section.

Nothing should require code evaluation (such as [vim](/index.php/Vim "Vim") and `VIMINIT`), patches or compile-time options to gain support and anything which does must be deemed hardcoded. Additionally if the process is too error prone or difficult, such as [Haskell's cabal](https://www.haskell.org/cabal/) or eclipse, they should also be considered as hardcoded.

*   The first column should be the project name, ideally the command name if it is not ambigious, linked to their website or an appropriate internal wiki article.

*   The second column is for any legacy files and directories the project had, this is done so people can find them even if they are no longer read.

*   Try to find the commit or version a project switched to XDG Base Directory or any open discussions and include them in the next two columns.

*   Finally include any appropriate workarounds or solutions for unsupported projects. Be terse, this article assumes intelligence and good charity from the reader. If something is unclear then feel free to expend some explanation to clarify it.

Lastly, and this goes without saying, please verify that your solution is correct and functional.

## Supported

<table class="wikitable sortable" style="width: 100%">

<tbody>

<tr>

<th>Application</th>

<th>Legacy Path</th>

<th>Supported Since</th>

<th>Discussion</th>

<th>Notes</th>

</tr>

<tr>

<td>[antimicro](https://github.com/Ryochan7/antimicro/)</td>

<td>`~/.antimicro`</td>

<td>[edba864](https://github.com/Ryochan7/antimicro/commit/edba864)</td>

<td>[[1]](https://github.com/Ryochan7/antimicro/issues/5)</td>

</tr>

<tr>

<td>[aria2](https://github.com/tatsuhiro-t/aria2/)</td>

<td>`~/.aria2`</td>

<td>[8bc1d37](https://github.com/tatsuhiro-t/aria2/commit/8bc1d37)</td>

<td>[[2]](https://github.com/tatsuhiro-t/aria2/issues/27)</td>

</tr>

<tr>

<td>[blender](http://www.blender.org/)</td>

<td>`~/.blender`</td>

<td>[4293f473](http://git.blender.org/gitweb/gitweb.cgi/blender.git/commit/4293f473)</td>

<td>[[3]](https://developer.blender.org/T28943)</td>

</tr>

<tr>

<td>[burp](https://github.com/falconindy/burp)</td>

<td>[f2388e9](https://github.com/falconindy/burp/commit/f2388e9)</td>

</tr>

<tr>

<td>[chromium](/index.php/Chromium "Chromium")</td>

<td>`~/.chromium`</td>

<td>[23057](https://src.chromium.org/viewvc/chrome?revision=23057&view=revision)</td>

<td>[[4]](https://groups.google.com/forum/#!topic/chromium-dev/QekVQxF3nho) [[5]](https://code.google.com/p/chromium/issues/detail?id=16976)</td>

</tr>

<tr>

<td>[cower](https://github.com/falconindy/cower)</td>

<td>[8b70805](https://github.com/falconindy/cower/commit/8b70805)</td>

</tr>

<tr>

<td>[dconf](https://wiki.gnome.org/dconf)</td>

</tr>

<tr>

<td>[d-feet](https://wiki.gnome.org/Apps/DFeet)</td>

<td>`~/.d-feet`</td>

<td>[7f6104b](https://git.gnome.org/browse/d-feet/commit/?id==7f6104b)</td>

</tr>

<tr>

<td>[dolphin-emu](/index.php/Dolphin_emulator "Dolphin emulator")</td>

<td>`~/.dolphin-emu`</td>

<td>[a498c68](https://github.com/dolphin-emu/dolphin/commit/a498c68)</td>

<td>[[6]](https://github.com/dolphin-emu/dolphin/pull/2304)</td>

</tr>

<tr>

<td>[dunst](http://www.knopwob.org/dunst/index.html)</td>

<td>[78b6e2b1](https://github.com/knopwob/dunst/commit/78b6e2b1)</td>

<td>[[7]](https://github.com/knopwob/dunst/issues/22)</td>

</tr>

<tr>

<td>[dwb](/index.php/Dwb "Dwb")</td>

</tr>

<tr>

<td>[fontconfig](/index.php/Fontconfig "Fontconfig")</td>

<td>`~/.fontconfig`</td>

<td>[8c255fb1](http://cgit.freedesktop.org/fontconfig/commit/?id=8c255fb1)</td>

</tr>

<tr>

<td>[fontforge](http://fontforge.github.io/)</td>

<td>`~/.FontForge` `~/.PfaEdit`</td>

<td>[e4c2cc7432](https://github.com/fontforge/fontforge/commit/e4c2cc7432)</td>

<td>[[8]](https://github.com/fontforge/fontforge/issues/847) [[9]](https://github.com/fontforge/fontforge/issues/991)</td>

</tr>

<tr>

<td>[fontconfig](/index.php/Fontconfig "Fontconfig")</td>

<td>`~/.fonts`</td>

<td>Use `"$XDG_DATA_HOME"/fonts` instead.</td>

</tr>

<tr>

<td>[gconf](https://projects.gnome.org/gconf)</td>

<td>`~/.gconf`</td>

<td>[fc28caa7](https://git.gnome.org/browse/gconf/commit/?id=fc28caa7)</td>

<td>[[10]](https://bugzilla.gnome.org/show_bug.cgi?id=674803)</td>

</tr>

<tr>

<td>[git](/index.php/Git "Git")</td>

<td>`~/.gitconfig`</td>

<td>[0d94427e](https://github.com/git/git/commit/0d94427e)</td>

</tr>

<tr>

<td>[gstreamer-1.0](http://gstreamer.freedesktop.org/)</td>

<td>[4e36f93924cf](http://cgit.freedesktop.org/gstreamer/gstreamer/commit/?id=4e36f93924cf)</td>

<td>[[11]](https://bugzilla.gnome.org/show_bug.cgi?id=518597)</td>

</tr>

<tr>

<td>[gtk3](/index.php/Gtk "Gtk")</td>

</tr>

<tr>

<td>[htop](http://hisham.hm/htop/)</td>

<td>`~/.htoprc`</td>

<td>[93233a67](https://github.com/hishamhm/htop/commit/93233a67)</td>

</tr>

<tr>

<td>[i3](/index.php/I3 "I3")</td>

<td>`~/.i3`</td>

<td>[7c130fb54](http://code.stapelberg.de/git/i3/commit/?id=7c130fb54)</td>

</tr>

<tr>

<td>[i3status](http://i3wm.org/i3status/)</td>

<td>`~/.i3status.conf`</td>

<td>[c3f7fc4994](http://code.stapelberg.de/git/i3status/commit/?id=c3f7fc4994)</td>

</tr>

<tr>

<td>[imagemagick](http://www.imagemagick.org/script/index.php)</td>

</tr>

<tr>

<td>[inkscape](/index.php/Inkscape "Inkscape")</td>

<td>`~/.inkscape`</td>

<td>[0.47](http://wiki.inkscape.org/wiki/index.php/Release_notes/0.47#Preferences)</td>

<td>[[12]](https://bugs.launchpad.net/inkscape/+bug/199720)</td>

</tr>

<tr>

<td>[lgogdownloader](https://github.com/Sude-/lgogdownloader/)</td>

<td>`~/.gogdownloader`</td>

<td>[d430af63d000](https://github.com/Sude-/lgogdownloader/commit/d430af63d000)</td>

<td>[[13]](https://github.com/Sude-/lgogdownloader/issues/4)</td>

</tr>

<tr>

<td>[livestreamer](/index.php/Livestreamer "Livestreamer")</td>

<td>`~/.livestreamerrc`</td>

<td>[ea805917](https://github.com/chrippa/livestreamer/commit/ea805917)</td>

<td>[[14]](https://github.com/chrippa/livestreamer/pull/106)</td>

</tr>

<tr>

<td>[llpp](/index.php/Llpp "Llpp")</td>

<td>[3ab86f0cb](http://repo.or.cz/w/llpp.git/commit/3ab86f0cb)</td>

<td>Currently llpp places the configuration directly under `XDG_CONFIG_HOME` instead of creating a directory.</td>

</tr>

<tr>

<td>[mc](/index.php/Mc "Mc")</td>

<td>`~/.mc`</td>

<td>[1b9957058](https://www.midnight-commander.org/changeset/1b9957058) [0b7115647](https://www.midnight-commander.org/changeset/0b7115647) [ce401d797](https://www.midnight-commander.org/changeset/ce401d797)</td>

<td>[[15]](https://www.midnight-commander.org/ticket/1851)</td>

</tr>

<tr>

<td>[mpd](/index.php/Mpd "Mpd")</td>

<td>`~/.mpdconf`</td>

<td>[87b73284](http://git.musicpd.org/cgit/master/mpd.git/commit/?id=87b73284)</td>

</tr>

<tr>

<td>[mpv](/index.php/Mpv "Mpv")</td>

<td>`~/.mpv`</td>

<td>[cb250d490](https://github.com/mpv-player/mpv/commit/cb250d490)</td>

<td>[[16]](https://github.com/mpv-player/mpv/pull/864)</td>

</tr>

<tr>

<td>[mypaint](http://mypaint.intilinux.com/)</td>

<td>`~/.mypaint`</td>

<td>[cf723b74cd](https://github.com/mypaint/mypaint/commit/cf723b74cd)</td>

</tr>

<tr>

<td>[newsbeuter](/index.php/Newsbeuter "Newsbeuter")</td>

<td>`~/.newsbeuter`</td>

<td>[3c57824c5](https://github.com/akrennmair/newsbeuter/commit/3c57824c5)</td>

<td>[[17]](https://github.com/akrennmair/newsbeuter/pull/39)</td>

<td>It is required to create both `"$XDG_DATA_HOME"/newsbeuter` and `"$XDG_CONFIG_HOME"/newsbeuter` [[18]](http://newsbeuter.org/doc/newsbeuter.html#_xdg_base_directory_support)</td>

</tr>

<tr>

<td>[OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP")</td>

<td>`~/.offlineimaprc`</td>

<td>[5150de5](https://github.com/OfflineIMAP/offlineimap/commit/5150de5)</td>

<td>[[19]](https://github.com/OfflineIMAP/offlineimap/issues/32)</td>

</tr>

<tr>

<td>[pcsx2](http://pcsx2.net/)</td>

<td>`~/.pcsx2`</td>

<td>[87f1e8f77](https://github.com/PCSX2/pcsx2/commit/87f1e8f77) [a9020c606](https://github.com/PCSX2/pcsx2/commit/a9020c606) [3b22f0fb0](https://github.com/PCSX2/pcsx2/commit/3b22f0fb0) [0a012aec2](https://github.com/PCSX2/pcsx2/commit/0a012aec2)</td>

<td>[[20]](https://github.com/PCSX2/pcsx2/issues/352) [[21]](https://github.com/PCSX2/pcsx2/issues/381)</td>

</tr>

<tr>

<td>[ppsspp](http://www.ppsspp.org/)</td>

<td>`~/.ppsspp`</td>

<td>[132fe47c7d](https://github.com/hrydgard/ppsspp/commit/132fe47c7d)</td>

<td>[[22]](https://github.com/hrydgard/ppsspp/issues/4623)</td>

</tr>

<tr>

<td>[orbment](https://github.com/Cloudef/orbment/)</td>

</tr>

<tr>

<td>[pacman](/index.php/Pacman "Pacman")</td>

<td>`~/.makepkg.conf`</td>

<td>[80eca94c8](https://projects.archlinux.org/pacman.git/commit/?id=80eca94c8)</td>

<td>[[23]](https://mailman.archlinux.org/pipermail/pacman-dev/2014-July/019178.html)</td>

</tr>

<tr>

<td>[PulseAudio](/index.php/PulseAudio "PulseAudio")</td>

<td>`~/.pulse` `~/.pulse-cookie`</td>

<td>[59a8618dcd9](http://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=59a8618dcd9) [87ae8307057](http://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=87ae8307057) [9ab510a6921](http://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=9ab510a6921) [4c195bcc9d5](http://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=4c195bcc9d5)</td>

<td>[[24]](https://bugzilla.redhat.com/show_bug.cgi?id=845607)</td>

</tr>

<tr>

<td>[qutebrowser](/index.php/Qutebrowser "Qutebrowser")</td>

</tr>

<tr>

<td>[systemd](/index.php/Systemd "Systemd")</td>

</tr>

<tr>

<td>[termite](/index.php/Termite "Termite")</td>

</tr>

<tr>

<td>[transmission](/index.php/Transmission "Transmission")</td>

<td>`~/.transmission`</td>

<td>[5517](https://trac.transmissionbt.com/changeset/5517)</td>

<td>[[25]](https://trac.transmissionbt.com/ticket/684)</td>

</tr>

<tr>

<td>[util-linux](https://www.kernel.org/pub/linux/utils/util-linux/)</td>

<td>[570b32100](http://git.kernel.org/cgit/utils/util-linux/util-linux.git/commit/?id=570b32100)</td>

</tr>

<tr>

<td>[freerdp](http://www.freerdp.com/)</td>

<td>`~/.freerdp`</td>

<td>[edf6e7258d](https://github.com/FreeRDP/FreeRDP/commit/edf6e7258d)</td>

</tr>

<tr>

<td>[beets](http://beets.radbox.org/)</td>

</tr>

<tr>

<td>[pyroom](http://pyroom.org/index.html)</td>

</tr>

<tr>

<td>[citra](http://citra-emu.org/)</td>

<td>`~/.citra-emu`</td>

<td>[f7c3193fec](https://github.com/citra-emu/citra/commit/f7c3193fec)</td>

<td>[[26]](https://github.com/citra-emu/citra/pull/575)</td>

</tr>

<tr>

<td>[retroarch](http://www.libretro.com/)</td>

</tr>

<tr>

<td>[lftp](http://lftp.yar.ru/)</td>

<td>`~/.lftp`</td>

<td>[21dc400](https://github.com/lavv17/lftp/commit/21dc400)</td>

<td>[[27]](https://www.mail-archive.com/lftp@uniyar.ac.ru/msg04301.html)</td>

</tr>

<tr>

<td>[xsettingsd](https://github.com/derat/xsettingsd)</td>

<td>`~/.xsettingsd`</td>

<td>[4ecd7be](https://github.com/derat/xsettingsd/commit/b4999f5e9e99224caf97d09f25ee731774ecd7be)</td>

</tr>

<tr>

<td>[surfraw](/index.php/Surfraw "Surfraw")</td>

<td>`~/.surfraw.conf` `~/.surfraw.bookmarks`</td>

<td>[3e4591d8](http://anonscm.debian.org/cgit/surfraw/surfraw.git/commit/?id=3e4591d8) [bd8c427d](http://anonscm.debian.org/cgit/surfraw/surfraw.git/commit/?id=bd8c427d) [f57fc718](http://anonscm.debian.org/cgit/surfraw/surfraw.git/commit/?id=f57fc718)</td>

</tr>

<tr>

<td>[milkytracker](http://milkytracker.org/)</td>

<td>`~/.milkytracker_config`</td>

<td>[eb487c55](https://github.com/Deltafire/MilkyTracker/commit/eb487c55)</td>

<td>[[28]](https://github.com/Deltafire/MilkyTracker/issues/12)</td>

</tr>

<tr>

<td>[sway](https://github.com/SirCmpwn/sway)</td>

<td>`~/.sway/config`</td>

<td>[614393c09](https://github.com/SirCmpwn/sway/commit/614393c09)</td>

<td>[[29]](https://github.com/SirCmpwn/sway/issues/5)</td>

</tr>

<tr>

<td>[fish](/index.php/Fish "Fish")</td>

</tr>

<tr>

<td>[opentyrian](https://bitbucket.org/opentyrian/opentyrian/wiki/Home)</td>

<td>`~/.opentyrian`</td>

<td>[8d45ff2](https://bitbucket.org/opentyrian/opentyrian/commits/8d45ff2)</td>

<td>[[30]](https://web.archive.org/web/20140815181350/http://code.google.com/p/opentyrian/issues/detail?id=125)</td>

</tr>

<tr>

<td>[neovim](http://neovim.io/)</td>

<td>`~/.nvim` `~/.nvimlog` `~/.nviminfo`</td>

<td>[1ca5646bb](https://github.com/neovim/neovim/commit/1ca5646bb)</td>

<td>[[31]](https://github.com/neovim/neovim/issues/78) [[32]](https://github.com/neovim/neovim/pull/3198)</td>

</tr>

<tr>

<td>[rr](http://rr-project.org/)</td>

<td>`~/.rr`</td>

<td>[02e7d41e](https://github.com/mozilla/rr/commit/02e7d41e)</td>

<td>[[33]](https://github.com/mozilla/rr/issues/1455)</td>

</tr>

<tr>

<td>[wireshark](/index.php/Wireshark "Wireshark")</td>

<td>`~/.wireshark`</td>

<td>[b0b53fa5](https://code.wireshark.org/review/gitweb?p=wireshark.git;a=commit;h=b0b53fa5937aa7ba258427ca0f3581dba725230d)</td>

</tr>

<tr>

<td>[vimb](http://fanglingsu.github.io/vimb/)</td>

</tr>

</tbody>

</table>

## Partial

<table class="wikitable sortable" style="width: 100%">

<tbody>

<tr>

<th>Application</th>

<th>Legacy Path</th>

<th>Supported Since</th>

<th>Discussion</th>

<th>Notes</th>

</tr>

<tr>

<td>[abook](http://abook.sourceforge.net/)</td>

<td>`~/.abook`</td>

<td>`$ abook --config "$XDG_CONFIG_HOME"/abook/abookrc \

--datafile "$XDG_CACHE_HOME"/abook/addressbook

`</td>

</tr>

<tr>

<td>[aspell](http://aspell.net/)</td>

<td>`~/.aspell.conf`</td>

</tr>

<tr>

<td>[cargo](http://crates.io/)</td>

<td>`~/.cargo`</td>

<td>[[34]](https://github.com/rust-lang/cargo/pull/148) [[35]](https://github.com/rust-lang/cargo/issues/1734)</td>

<td>`$ export CARGO_HOME="$XDG_DATA_HOME"/cargo`</td>

</tr>

<tr>

<td>[ccache](/index.php/Ccache "Ccache")</td>

<td>`~/.ccache`</td>

<td>`$ export CCACHE_DIR="$XDG_CACHE_HOME"/ccache`</td>

</tr>

<tr>

<td>[conky](/index.php/Conky "Conky")</td>

<td>`~/.conkyrc`</td>

<td>[00481ee](https://github.com/brndnmtthws/conky/commit/00481ee9a97025e8e2acd7303d080af1948f7980)</td>

<td>[[36]](https://github.com/brndnmtthws/conky/issues/144)</td>

<td>`$ conky --config="$XDG_CONFIG_HOME"/conky/conkyrc`</td>

</tr>

<tr>

<td>[crawl](http://www.dungeoncrawl.org/)</td>

<td>`~/.crawl`</td>

<td>`$ export CRAWL_DIR="$XDG_DATA_HOME"/crawl/ # Trailing '/' is required.`</td>

</tr>

<tr>

<td>[coreutils](https://www.gnu.org/software/coreutils/)</td>

<td>`~/.dircolors`</td>

<td>`$ source "$(dircolors "$XDG_CONFIG_HOME"/dircolors)"`</td>

</tr>

<tr>

<td>[ELinks](/index.php/ELinks "ELinks")</td>

<td>`~/.elinks`</td>

<td>`$ export ELINKS_CONFDIR="$XDG_CONFIG_HOME"/elinks`</td>

</tr>

<tr>

<td>[PulseAudio](/index.php/PulseAudio "PulseAudio")</td>

<td>`~/.esd_auth`</td>

<td>Very likely generated by the `module-esound-protocol-unix.so` module. It can be configured to use a different location but it makes much more sense to just comment out this module in `/etc/pulse/default.pa` or `$XDG_CONFIG_HOME/pulse/default.pa`.</td>

</tr>

<tr>

<td>[gdb](http://www.gnu.org/software/gdb/)</td>

<td>`~/.gdbinit`</td>

<td>`$ gdb -nh -x "$XDG_CONFIG_HOME"/gdb/init`</td>

</tr>

<tr>

<td>[gimp](/index.php/Gimp "Gimp")</td>

<td>`~/.gimp-2.8`</td>

<td>[60e0cfe](https://git.gnome.org/browse/gimp/commit/?id=60e0cfe)</td>

<td>[[37]](https://bugzilla.gnome.org/show_bug.cgi?id=166643) [[38]](https://mail.gnome.org/archives/gimp-developer-list/2012-October/msg00028.html)</td>

<td>`$ export GIMP2_DIRECTORY="$XDG_CONFIG_HOME"/gimp`</td>

</tr>

<tr>

<td>[gliv](http://guichaz.free.fr/gliv/)</td>

<td>`~/.glivrc`</td>

<td>`$ gliv --glivrc="$XDG_CONFIG_HOME"/gliv/glivrc`</td>

</tr>

<tr>

<td>[gpg](/index.php/GPG "GPG")</td>

<td>`~/.gnupg`</td>

<td>`$ export GNUPGHOME="$XDG_CONFIG_HOME/gnupg`

`$ gpg2 --homedir "$XDG_CONFIG_HOME/gnupg`

</td>

</tr>

<tr>

<td>[gtk2](/index.php/Gtk "Gtk")</td>

<td>`~/.gtkrc-2.0`</td>

<td>`$ export GTK2_RC_FILES="$XDG_CONFIG_HOME"/gtk-2.0/gtkrc`</td>

</tr>

<tr>

<td>[gtk](/index.php/Gtk "Gtk")</td>

<td>`~/.gtkrc`</td>

<td>`$ export GTK_RC_FILES="$XDG_CONFIG_HOME"/gtk-1.0/gtkrc`</td>

</tr>

<tr>

<td>[httpie](http://httpie.org)</td>

<td>`~/.httpie`</td>

<td>[[39]](https://github.com/jakubroztocil/httpie/issues/145)</td>

<td>`$ export HTTPIE_CONFIG_DIR="$XDG_CONFIG_HOME"/httpie`</td>

</tr>

<tr>

<td>[ipython](http://ipython.org)/[jupyter](http://jupyter.org)</td>

<td>`~/.ipython`</td>

<td>`$ export IPYTHONDIR="$XDG_CONFIG_HOME"/jupyter``$ export JUPYTER_CONFIG_DIR="$XDG_CONFIG_HOME"/jupyter`</td>

</tr>

<tr>

<td>[isync](http://isync.sourceforge.net)</td>

<td>`~/.mbsyncrc`</td>

<td>`$ mbsync -c "$XDG_CONFIG_HOME"/isync/mbsyncrc`</td>

</tr>

<tr>

<td>[libice](ftp://www.x.org/pub/xorg/current/doc/libICE/ice.html)</td>

<td>`~/.ICEauthority`</td>

<td>`$ export ICEAUTHORITY="$XDG_RUNTIME_DIR"/X11/iceauthority`</td>

</tr>

<tr>

<td>[less](http://www.greenwoodsoftware.com/less/)</td>

<td>`~/.lesshst`</td>

<td>`$ export LESSHISTFILE="$XDG_CACHE_HOME"/less/history`

`$ export LESSHISTFILE=-` can be used to disable this feature.

</td>

</tr>

<tr>

<td>[Mathematica](http://www.wolfram.com/mathematica/)</td>

<td>`~/.Mathematica`</td>

<td>`$ export MATHEMATICA_USERBASE="$XDG_CONFIG_HOME"/mathematica`</td>

</tr>

<tr>

<td>[mednafen](http://mednafen.sourceforge.net/)</td>

<td>`~/.mednafen`</td>

<td>`$ export MEDNAFEN_HOME="$XDG_CONFIG_HOME"/mednafen`</td>

</tr>

<tr>

<td>[moc](/index.php/Moc "Moc")</td>

<td>`~/.moc`</td>

<td>`$ mocp -M "$XDG_CONFIG_HOME"/moc`

`$ mocp -O MOCDir="$XDG_CONFIG_HOME"/moc`

</td>

</tr>

<tr>

<td>[MPlayer](/index.php/MPlayer "MPlayer")</td>

<td>`~/.mplayer`</td>

<td>`$ export MPLAYER_HOME="$XDG_CONFIG_HOME"/mplayer`</td>

</tr>

<tr>

<td>[mutt](/index.php/Mutt "Mutt")</td>

<td>`~/.mutt`</td>

<td>[[40]](http://dev.mutt.org/trac/ticket/3207)</td>

<td>`$ mutt -F "$XDG_CONFIG_HOME"/mutt/muttrc` `muttrc` 

```
set header_cache = $XDG_CACHE_HOME/mutt/headers
set message_cachedir = $XDG_DATA_HOME/mutt/messages
set mailcap_path = $XDG_CONFIG_HOME/mutt/mailcap
set record = $XDG_DATA_HOME/mutt/record/sent

```

</td>

</tr>

<tr>

<td>[ncmpcpp](/index.php/Ncmpcpp "Ncmpcpp")</td>

<td>`~/.ncmpcpp`</td>

<td>`$ ncmpcpp -c "$XDG_CONFIG_HOME"/ncmpcpp/config`</td>

</tr>

<tr>

<td>[notmuch](/index.php/Notmuch "Notmuch")</td>

<td>`~/.notmuch-config`</td>

<td>[[41]](http://notmuchmail.org/pipermail/notmuch/2011/007007.html)</td>

<td>`$ export NOTMUCH_CONFIG="$XDG_CONFIG_HOME"/notmuch/notmuchrc`

`$ export NMBGIT="$XDG_DATA_HOME"/notmuch/nmbug`

</td>

</tr>

<tr>

<td>[ncurses](https://www.archlinux.org/packages/?name=ncurses)</td>

<td>`~/.terminfo`</td>

<td>`$ export TERMINFO="$XDG_DATA_HOME"/terminfo # Precludes system path searching.`

`$ export TERMINFO_DIRS="$XDG_DATA_HOME"/terminfo:/usr/share/terminfo`

</td>

</tr>

<tr>

<td>[NVIDIA](/index.php/NVIDIA "NVIDIA"), [CUDA](/index.php/CUDA "CUDA")</td>

<td>`~/.nv`</td>

<td>`$ export __GL_SHADER_DISK_CACHE_PATH="$XDG_CACHE_HOME"/nv`

`$ export CUDA_CACHE_PATH="$XDG_CACHE_HOME"/nv`

</td>

</tr>

<tr>

<td>[readline](http://cnswww.cns.cwru.edu/php/chet/readline/rltop.html)</td>

<td>`~/.inputrc`</td>

<td>`$ export INPUTRC="$XDG_CONFIG_HOME"/readline/inputrc`</td>

</tr>

<tr>

<td>[screen](/index.php/Screen "Screen")</td>

<td>`~/.screenrc`</td>

<td>`$ export SCREENRC="$XDG_CONFIG_HOME"/screen/screenrc`</td>

</tr>

<tr>

<td>[tmux](/index.php/Tmux "Tmux")</td>

<td>`~/.tmux.conf`</td>

<td>[[42]](http://comments.gmane.org/gmane.comp.terminal-emulators.tmux.user/6013) [[43]](http://sourceforge.net/p/tmux/mailman/message/30619546/)</td>

<td>`$ tmux -f "$XDG_CONFIG_HOME"/tmux/tmux.conf`

`$ export TMUX_TMPDIR="$XDG_RUNTIME_DIR"/tmux`

</td>

</tr>

<tr>

<td>[urxvtd](/index.php/Rxvt-unicode#Daemon-client "Rxvt-unicode")</td>

<td>`~/.urxvt/urxvtd-hostname`</td>

<td>`$ export RXVT_SOCKET="$XDG_RUNTIME_DIR"/urxvt/urxvt-"$(hostname)"`</td>

</tr>

<tr>

<td>[WeeChat](/index.php/WeeChat "WeeChat")</td>

<td>`~/.weechat`</td>

<td>[[44]](http://savannah.nongnu.org/task/?10934)</td>

<td>`$ export WEECHAT_HOME="$XDG_CONFIG_HOME"/weechat`

`$ weechat -d "$XDG_CONFIG_HOME"/weechat`

</td>

</tr>

<tr>

<td>[wine](/index.php/Wine "Wine")</td>

<td>`~/.wine`</td>

<td>[[45]](https://bugs.winehq.org/show_bug.cgi?id=20888)</td>

<td>`$ export WINEPREFIX="$XDG_DATA_HOME"/wine`</td>

</tr>

<tr>

<td>[xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth)</td>

<td>`~/.Xauthority`</td>

<td>`$ export XAUTHORITY="$XDG_RUNTIME_DIR"/X11/xauthority`</td>

</tr>

<tr>

<td>[libx11](http://www.x.org/wiki/)</td>

<td>`~/.XCompose`</td>

<td>`$ export XCOMPOSEFILE="$XDG_CONFIG_HOME"/X11/xcompose`</td>

</tr>

<tr>

<td>[xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit)</td>

<td>`~/.xinitrc`</td>

<td>`$ export XINITRC="$XDG_CONFIG_HOME"/X11/xinitrc`</td>

</tr>

<tr>

<td>[xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb)</td>

<td>`~/.Xresources` `~/.Xdefaults`</td>

<td>Ultimately you [should be](http://superuser.com/questions/243914/xresources-or-xdefaults) using `Xresources` and since these resources are loaded via `xrdb` you can specify a path such as `xrdb -load ~/.config/X11/xresources`.</td>

</tr>

<tr>

<td>[openscad](http://www.openscad.org/)</td>

<td>`~/.OpenSCAD`</td>

<td>[7c3077b0f](https://github.com/openscad/openscad/commit/7c3077b0f)</td>

<td>[[46]](https://github.com/openscad/openscad/issues/125)</td>

<td>Does not fully honour XDG Base Directory Specification, see [[47]](https://github.com/openscad/openscad/issues/373)

Currently it [hard-codes](https://github.com/openscad/openscad/blob/master/src/PlatformUtils-posix.cc#L20) `~/.local/share`.

</td>

</tr>

<tr>

<td>[libdvdcss](http://www.videolan.org/developers/libdvdcss.html)</td>

<td>`~/.dvdcss`</td>

<td>[[48]](https://mailman.videolan.org/pipermail/libdvdcss-devel/2014-August/001022.html)</td>

<td>`$ export DVDCSS_CACHE="$XDG_DATA_HOME"/dvdcss`</td>

</tr>

<tr>

<td>[tig](http://jonas.nitro.dk/tig/)</td>

<td>`~/.tigrc`</td>

<td>`$ export TIGRC_USER="$XDG_CONFIG_HOME"/tig/tigrc`</td>

</tr>

<tr>

<td>[rlwrap](http://utopia.knoware.nl/~hlub/uck/rlwrap/)</td>

<td>`~/.*_history`</td>

<td>[[49]](https://github.com/hanslub42/rlwrap/issues/25)</td>

<td>`$ export RLWRAP_HOME="$XDG_DATA_HOME"/rlwrap`</td>

</tr>

<tr>

<td>[uncrustify](https://github.com/bengardner/uncrustify)</td>

<td>`~/.uncrustify.cfg`</td>

<td>`$ export UNCRUSTIFY_CONFIG="$XDG_CONFIG_HOME"/uncrustify/uncrustify.cfg`</td>

</tr>

<tr>

<td>[xsel](http://www.vergenet.net/~conrad/software/xsel/)</td>

<td>`~/.xsel.log`</td>

<td>[[50]](https://github.com/kfish/xsel/issues/10)</td>

<td>`$ xsel --logfile "$XDG_CACHE_HOME"/xsel/xsel.log`</td>

</tr>

<tr>

<td>[emscripten](http://kripken.github.io/emscripten-site/)</td>

<td>`~/.emscripten` `~/.emscripten_sanity` `~/.emscripten_ports` `~/.emscripten_cache__last_clear`</td>

<td>[3624](https://github.com/kripken/emscripten/issues/3624)</td>

<td>`$ export EM_CONFIG="$XDG_CONFIG_HOME"/emscripten/config`

`$ export EM_CACHE="$XDG_CACHE_HOME"/emscripten/cache` `$ export EM_PORTS="$XDG_DATA_HOME"/emscripten/cache` `$ emcc --em-config "$XDG_CONFIG_HOME"/emscripten/config --em-cache "$XDG_CACHE_HOME"/emscripten/cache`

</td>

</tr>

<tr>

<td>[stack](https://www.stackage.org/)</td>

<td>`~/.stack`</td>

<td>[[51]](https://github.com/commercialhaskell/stack/issues/342)</td>

<td>`$ export STACK_ROOT="$XDG_DATA_HOME"/stack`</td>

</tr>

<tr>

<td>[subversion](/index.php/Subversion "Subversion")</td>

<td>`~/.subversion`</td>

<td>[[52]](https://mail-archives.apache.org/mod_mbox/subversion-users/201204.mbox/%3c4F8FBCC6.4080205@ritsuka.org%3e)[[53]](http://mail-archives.apache.org/mod_mbox/subversion-dev/201509.mbox/%3c20150917222954.GA20331@teapot%3e)</td>

<td>`$ svn --config-dir "$XDG_CONFIG_HOME"/subversion`</td>

</tr>

<tr>

<td>[ltrace](http://ltrace.org/)</td>

<td>`~/.ltrace.conf`</td>

<td>`$ ltrace -F "$XDG_CONFIG_HOME"/ltrace/ltrace.conf`</td>

</tr>

</tbody>

</table>

## Hardcoded

<table class="wikitable sortable" style="width: 100%">

<tbody>

<tr>

<th>Application</th>

<th>Legacy Path</th>

<th>Supported Since</th>

<th>Discussion</th>

<th>Notes</th>

</tr>

<tr>

<td>[Apache Directory Studio](https://directory.apache.org/studio/)</td>

<td>`~/.ApacheDirectoryStudio`</td>

</tr>

<tr>

<td>[AMule](/index.php/AMule "AMule")</td>

<td>`~/.aMule`</td>

</tr>

<tr>

<td>[cabal](https://www.haskell.org/cabal/)</td>

<td>`~/.cabal`</td>

<td>[[54]](https://github.com/haskell/cabal/issues/680)</td>

<td>See discussion for potential workarounds. It is not very easy or straightforward but may be possible to emulate Base Directory compliance.</td>

</tr>

<tr>

<td>[julia](http://julialang.org/)</td>

<td>`~/.juliarc.jl` `~/.julia_history`</td>

<td>[[55]](https://github.com/JuliaLang/julia/issues/4630) [[56]](https://github.com/JuliaLang/julia/issues/10016)</td>

</tr>

<tr>

<td>[milkytracker](http://www.milkytracker.org/)</td>

<td>`~/.milkytracker_config`</td>

<td>[[57]](https://github.com/Deltafire/MilkyTracker/issues/12)</td>

</tr>

<tr>

<td>[firefox](/index.php/Firefox "Firefox")</td>

<td>`~/.mozilla`</td>

<td>[[58]](https://bugzil.la/259356)</td>

</tr>

<tr>

<td>[gstreamer-0.10](http://gstreamer.freedesktop.org/documentation/gstreamer010.html)</td>

<td>`~/.gstreamer-0.10`</td>

<td>Use [gstreamer-1.0](http://gstreamer.freedesktop.org/) instead.</td>

</tr>

<tr>

<td>[python](/index.php/Python "Python")</td>

<td>`~/.python_history`</td>

<td>All history from interactive sessions is saved to `~/.python_history` by default since [version 3.4](https://bugs.python.org/issue5845), custom path can still be set the same way as in older versions (see [this example](https://docs.python.org/3/library/readline.html?highlight=readline#example)).</td>

</tr>

<tr>

<td>[procps-ng](https://www.archlinux.org/packages/?name=procps-ng)</td>

<td>`~/.toprc`</td>

<td>[[59]](https://bugzilla.redhat.com/show_bug.cgi?id=1155265)</td>

</tr>

<tr>

<td>[vim](/index.php/Vim "Vim")</td>

<td>`~/.vim` `~/.vimrc` `~/.viminfo`</td>

<td>Since [7.3.1178](https://github.com/vim/vim/commit/6a459902592e2a4ba68) vim will search for `~/.vim/vimrc` if `~/.vimrc` is not found. `~/.vim/vimrc` 

```
set undodir=~/.cache/vim/undo " vim will not create this directory.
set directory=~/.cache/vim/swap " vim will not create this directory.
set backupdir=~/.cache/vim/backup " vim will not create this directory.
set viminfo+=n~/.cache/vim/viminfo

```

*   [https://tlvince.com/vim-respect-xdg](https://tlvince.com/vim-respect-xdg)

</td>

</tr>

<tr>

<td>[xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils)</td>

<td>`~/.gnome`</td>

<td>For some reason the script `xdg-desktop-menu` hard-codes `gnome_user_dir="$HOME/.gnome/apps"`. This is used by [chromium](/index.php/Chromium "Chromium") amoung others.</td>

</tr>

<tr>

<td>[SQLite](/index.php/SQLite "SQLite")</td>

<td>`~/.sqlite_history`</td>

</tr>

<tr>

<td>[wpa_cli](http://w1.fi/)</td>

<td>`~/.wpa_cli_history`</td>

</tr>

<tr>

<td>[xmonad](/index.php/Xmonad "Xmonad")</td>

<td>`~/.xmonad`</td>

<td>[[60]](https://code.google.com/p/xmonad/issues/detail?id=484)</td>

</tr>

<tr>

<td>[eclipse](/index.php/Eclipse "Eclipse")</td>

<td>`~/.eclipse`</td>

<td>[[61]](https://bugs.eclipse.org/bugs/show_bug.cgi?id=200809)</td>

<td>Option `-Dosgi.configuration.area=@user.home/.config/..` overrides but must be added to `"$ECLIPSE_HOME"/eclipse.ini"` rather than command line which means you must have write access to `$ECLIPSE_HOME`. (Arch Linux hard-codes `$ECLIPSE_HOME` in `/usr/bin/eclipse`)</td>

</tr>

<tr>

<td>[perf](https://perf.wiki.kernel.org/index.php/Main_Page)</td>

<td>`~/.debug`</td>

<td>Hardcoded in [tools/perf/util/config.c:18](https://github.com/torvalds/linux/blob/master/tools/perf/util/config.c#L18).</td>

</tr>

<tr>

<td>[zsh](/index.php/Zsh "Zsh")</td>

<td>`~/.zshrc` `~/.zprofile` `~/.zshenv` `~/.zlogin` `~/.zlogout` `~/.zsh_history` `~/.zhistory`</td>

<td>[[62]](http://www.zsh.org/mla/workers/2013/msg00692.html)</td>

<td>Consider exporting `ZDOTDIR=$HOME/.config/zsh` in `~/.zshenv` (this is hardcoded due to the bootstrap problem). You could also add this to `/etc/zsh/zshenv` and avoid the need for any dotfiles in your `HOME`. Doing this however requires root privilege which may not be viable and is system-wide.

`export HISTFILE="$XDG_DATA_HOME"/zsh/history`

</td>

</tr>

<tr>

<td>[bash](/index.php/Bash "Bash")</td>

<td>`~/.bashrc` `~/.bash_history` `~/.bash_profile` `~/.bash_login` `~/.bash_logout`</td>

<td>[[63]](http://savannah.gnu.org/support/?108134)</td>

<td>`export HISTFILE="$XDG_DATA_HOME"/bash/history`</td>

</tr>

<tr>

<td>[lldb](http://lldb.llvm.org/)</td>

<td>`~/.lldb` `~/.lldbinit`</td>

</tr>

<tr>

<td>[emacs](https://www.gnu.org/software/emacs/)</td>

<td>`~/.emacs` `~/.emacs.d`</td>

<td>[[64]](http://debbugs.gnu.org/cgi/bugreport.cgi?bug=583)</td>

<td>It's possible to set `HOME`, but it has unexpected side effects. So far the most promising approach is modifying another Emacs environment variable to alter the load path and author your own site file which can manually load up your init file, but it changes the load process significantly.</td>

</tr>

<tr>

<td>[mathomatic](http://www.mathomatic.org/)</td>

<td>`~/.mathomaticrc` `~/.matho_history`</td>

<td>History can be moved by using `rlwrap mathomatic -r` with the `RLWRAP_HOME` environment set appropriately.</td>

</tr>

<tr>

<td>[mongodb](https://www.mongodb.org/)</td>

<td>`~/.mongorc.js` `~/.dbshell`</td>

<td>[[65]](https://jira.mongodb.org/browse/DOCS-5652?jql=text%20~%20%22.mongorc.js%22)</td>

<td>[This Stack Overflow](http://stackoverflow.com/a/22349050/4200039) thread suggests a partial workaround using command-line switch `--norc`.</td>

</tr>

<tr>

<td>[xombrero](https://opensource.conformal.com/wiki/xombrero)</td>

<td>`~/.xombrero`</td>

<td>[[66]](https://github.com/conformal/xombrero/issues/74)</td>

</tr>

<tr>

<td>[spectrwm](/index.php/Spectrwm "Spectrwm")</td>

<td>`~/.spectrwm`</td>

</tr>

<tr>

<td>[ncmpc](http://www.musicpd.org/clients/ncmpc/)</td>

<td>`~/.ncmpc`</td>

</tr>

<tr>

<td>[palemoon](https://www.palemoon.org/)</td>

<td>`~/.moonchild productions`</td>

<td>[[67]](https://forum.palemoon.org/viewtopic.php?f=5&t=9639)</td>

</tr>

<tr>

<td>[vimperator](http://www.vimperator.org/)</td>

<td>`~/.vimperatorrc`</td>

<td>[[68]](http://www.mozdev.org/pipermail/vimperator/2009-October/004848.html)</td>

<td>`$ export VIMPERATOR_INIT=":source $XDG_CONFIG_HOME/vimperator/vimperatorrc"`

`$ export VIMPERATOR_RUNTIME="$XDG_CONFIG_HOME"/vimperator`

</td>

</tr>

<tr>

<td>[CUPS](/index.php/CUPS "CUPS")</td>

<td>`~/.cups`</td>

<td>[[69]](http://www.cups.org/str.php?L4243)</td>

</tr>

<tr>

<td>[dbus](/index.php/Dbus "Dbus")</td>

<td>`~/.dbus`</td>

<td>[[70]](https://bugs.freedesktop.org/show_bug.cgi?id=35887)</td>

<td>This should be avoidable with kdbus [citation needed].</td>

</tr>

</tbody>

</table>

## Library and Language Support

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

*   [Rob Pike: "Dotfiles" being hidden is a UNIXv2 mistake](https://plus.google.com/+RobPikeTheHuman/posts/R58WgWwN9jp).
*   [systemd-path(1)](http://www.freedesktop.org/software/systemd/man/systemd-path.html)
*   [file-hierarchy(7)](http://www.freedesktop.org/software/systemd/man/file-hierarchy.html)
*   [Grawity's notes on dotfiles](https://github.com/grawity/dotfiles/blob/master/.dotfiles.notes).
*   [Grawity's notes on environment variables](https://github.com/grawity/dotfiles/blob/master/.environ.notes).
*   [ploum.net: Modify Your Application to use XDG Folders](https://ploum.net/207-modify-your-application-to-use-xdg-folders/).

Retrieved from "[https://wiki.archlinux.org/index.php?title=XDG_Base_Directory_support&oldid=412023](https://wiki.archlinux.org/index.php?title=XDG_Base_Directory_support&oldid=412023)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Dotfiles](/index.php/Category:Dotfiles "Category:Dotfiles")