**Status de tradução:** Esse artigo é uma tradução de [XDG Base Directory](/index.php/XDG_Base_Directory "XDG Base Directory"). Data da última tradução: 2019-10-12\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=XDG_Base_Directory&diff=0&oldid=585140) na versão em inglês.

Artigos relacionados

*   [dotfiles](/index.php/Dotfiles_(Portugu%C3%AAs) "Dotfiles (Português)")
*   [Diretórios de usuário XDG](/index.php/Diret%C3%B3rios_de_usu%C3%A1rio_XDG "Diretórios de usuário XDG")

Esse artigo resumo a [especificação XDG Base Directory](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html) em [#Especificação](#Especificação) e rastreia o suporte por softwares em [#Suporte](#Suporte).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Especificação](#Especificação)
    *   [1.1 Diretórios de usuário](#Diretórios_de_usuário)
    *   [1.2 Diretórios de sistema](#Diretórios_de_sistema)
*   [2 Suporte](#Suporte)
    *   [2.1 Contribuindo](#Contribuindo)
    *   [2.2 Tem suporte](#Tem_suporte)
    *   [2.3 Parcial](#Parcial)
    *   [2.4 Codificado](#Codificado)
*   [3 Bibliotecas](#Bibliotecas)
*   [4 Veja também](#Veja_também)

## Especificação

Leia a [especificação completa](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html). Essa seção vai tentar destrinchar a essência do que a especificação tenta alcançar.

Apenas `XDG_RUNTIME_DIR` está definido por padrão por meio de [pam_systemd](https://www.freedesktop.org/software/systemd/man/pam_systemd.html). É deixado para que o usuário [defina](/index.php/Defina "Defina") explicitamente as demais variáveis de acordo com a especificação.

### Diretórios de usuário

*   `XDG_CONFIG_HOME`
    *   Onde configurações específicas do usuário devem ser escrita (análogo a `/etc`).
    *   O padrão deve ser `$HOME/.config`.

*   `XDG_CACHE_HOME`
    *   Onde dados (em cache) não essenciais e específicos do usuário devem ser escritos (análogo a `/var/cache`).
    *   O padrão deve ser `$HOME/.cache`.

*   `XDG_DATA_HOME`
    *   Onde arquivos de dados específicos do usuário devem ser escritos (análogo a `/usr/share`).
    *   O padrão deve ser `$HOME/.local/share`.

*   `XDG_RUNTIME_DIR`
    *   Usado para arquivos de dados não essenciais e específicos do usuário, como soquetes, pipes nomeados etc.
    *   Não é necessário ter um valor padrão; avisos devem ser emitidos se não definido ou equivalentes não forem fornecidos.
    *   Deve pertencer ao usuário com um modo de acesso de `0700`.
    *   Sistema de arquivos totalmente caracterizado pelos padrões do sistema operacional.
    *   Deve estar no sistema de arquivos local.
    *   Pode estar sujeito a limpeza periódica.
    *   Modificado a cada 6 horas ou defina um bit adesivo se desejar persistência.
    *   Só pode existir durante o início de sessão do usuário.
    *   Não deve armazenar arquivos grandes, pois pode ser montado como um tmpfs.

### Diretórios de sistema

*   `XDG_DATA_DIRS`
    *   Lista de diretórios separadas por `:` (análogo a `PATH`).
    *   O padrão deve ser `/usr/local/share:/usr/share`.

*   `XDG_CONFIG_DIRS`
    *   Lista os diretórios separados por `:` (análogo a `PATH`).
    *   O padrão deve ser `/etc/xdg`.

## Suporte

Esta seção existe para catalogar o crescente conjunto de softwares usando a [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html) introduzida em 2003\. Isso está aqui para demonstrar a viabilidade desta especificação listando os arquivos de ponto comumente encontrados e seu status de suporte. Para aqueles que atualmente não oferecem suporte à Base Directory Specification, as soluções alternativas serão demonstradas como emulação.

As soluções alternativas serão limitadas a qualquer coisa que não envolva o patch da fonte, a execução do código armazenado em [variáveis de ambiente](/index.php/Vari%C3%A1veis_de_ambiente "Variáveis de ambiente") ou as opções de tempo de compilação. A lógica para isso é que as configurações devem ser portáveis entre sistemas e ter opções em tempo de compilação evitam isso.

Espera-se que isso forneça uma fonte de informações sobre exatamente o que são certos tipos de arquivos-ponto (*dotfiles*) e de onde eles vêm.

### Contribuindo

Ao contribuir, certifique-se de usar a seção correta.

Nada deve exigir avaliação de código (como [vim](/index.php/Vim "Vim") e `VIMINIT`), patches ou opções em tempo de compilação para obter suporte e qualquer coisa que deva ser considerada codificada. Além disso, se o processo for muito propenso a erros ou difícil, como [cabal do Haskell](https://www.haskell.org/cabal/) ou Eclipse, eles também deverão ser considerados como codificados.

*   A primeira coluna deve ser um link para um artigo interno, um [Template:Pkg](/index.php/Template:Pkg "Template:Pkg") ou um [Template:AUR](/index.php/Template:AUR "Template:AUR").
*   A segunda coluna é para todos os arquivos e diretórios legados que o projeto tinha (um por linha); isso é feito para que as pessoas possam encontrá-los, mesmo que não sejam mais lidos.
*   Na terceira, tente encontrar o commit ou a versão de um projeto que mudou para o XDG Base Directory ou quaisquer discussões abertas e inclua-as nas próximas duas colunas (duas por linha).
*   A última coluna deve incluir quaisquer soluções alternativas ou soluções apropriadas. Verifique se sua solução está correta e funcional.

### Tem suporte

| Aplicativo | Caminho legado | Suporte desde | Discussão | Observações |
| [aerc-git](https://aur.archlinux.org/packages/aerc-git/) |
| [antimicro](https://aur.archlinux.org/packages/antimicro/) | `~/.antimicro` | [edba864](https://github.com/Antimicro/antimicro/commit/edba864) | [[1]](https://github.com/Antimicro/antimicro/issues/5) |
| [aria2](/index.php/Aria2 "Aria2") | `~/.aria2` | [8bc1d37](https://github.com/tatsuhiro-t/aria2/commit/8bc1d37) | [[2]](https://github.com/tatsuhiro-t/aria2/issues/27) |
| [asunder](https://www.archlinux.org/packages/?name=asunder) | 

`~/.asunder
~/.asunder_album_artist
~/.asunder_album_genre
~/.asunder_album_title`

 | [2.9.0](https://littlesvr.ca/bugs/show_bug.cgi?id=31) | [[3]](https://littlesvr.ca/bugs/show_bug.cgi?id=52) | Usa `XDG_CONFIG_HOME/asunder/asunder` para `~/.asunder` e `XDG_CACHE_HOME/asunder/asunder_album_...` para outros 3 arquivos. Caminhos legados não são removidos após a migração, tendo que ser excluídos manualmente. |
| [binwalk](https://www.archlinux.org/packages/?name=binwalk) | `~/.binwalk` | [2051757](https://github.com/ReFirmLabs/binwalk/commit/2051757) | [[4]](https://github.com/ReFirmLabs/binwalk/issues/216) | `$XDG_CONFIG_HOME/binwalk`

Há suporte apenas no branch master do Git, não havendo lançamentos estáveis atualizados.

 |
| [Blender](/index.php/Blender "Blender") | `~/.blender` | [4293f47](http://git.blender.org/gitweb/gitweb.cgi/blender.git/commit/4293f47) | [[5]](https://developer.blender.org/T28943) |
| [calibre](https://www.archlinux.org/packages/?name=calibre) |
| [Chromium](/index.php/Chromium "Chromium") | `~/.chromium` | [23057](https://src.chromium.org/viewvc/chrome?revision=23057&view=revision) | 

[[6]](https://groups.google.com/forum/#!topic/chromium-dev/QekVQxF3nho) [[7]](https://code.google.com/p/chromium/issues/detail?id=16976)

 |
| [citra-git](https://aur.archlinux.org/packages/citra-git/) | `~/.citra-emu` | [f7c3193](https://github.com/citra-emu/citra/commit/f7c3193) | [[8]](https://github.com/citra-emu/citra/pull/575) |
| [Composer](/index.php/Composer "Composer") | `~/.composer` | [1.0.0-beta1](https://github.com/composer/composer/releases/tag/1.0.0-beta1) | [[9]](https://github.com/composer/composer/pull/1407) |
| [d-feet](https://www.archlinux.org/packages/?name=d-feet) | `~/.d-feet` | [7f6104b](https://gitlab.gnome.org/GNOME/d-feet/commit/7f6104b) |
| [dconf](https://www.archlinux.org/packages/?name=dconf) |
| [Dolphin emulator](/index.php/Dolphin_emulator "Dolphin emulator") | `~/.dolphin-emu` | [a498c68](https://github.com/dolphin-emu/dolphin/commit/a498c68) | [[10]](https://github.com/dolphin-emu/dolphin/pull/2304) |
| [dr14_tmeter](https://aur.archlinux.org/packages/dr14_tmeter/) | [7e777ca](https://github.com/simon-r/dr14_t.meter/commit/7e777ca) | [[11]](https://github.com/simon-r/dr14_t.meter/pull/30) | `XDG_CONFIG_HOME/dr14tmeter/` |
| [dunst](https://www.archlinux.org/packages/?name=dunst) | [78b6e2b](https://github.com/knopwob/dunst/commit/78b6e2b) | [[12]](https://github.com/knopwob/dunst/issues/22) |
| [dwb](/index.php/Dwb "Dwb") |
| [elixir](https://www.archlinux.org/packages/?name=elixir) | `~/.mix` | [afaf889](https://github.com/elixir-lang/elixir/commit/afaf889) | [[13]](https://github.com/elixir-lang/elixir/issues/8818) |
| [fish](/index.php/Fish "Fish") |
| [fontconfig](/index.php/Fontconfig "Fontconfig") | 

`~/.fontconfig
~/.fonts`

 | [8c255fb](https://cgit.freedesktop.org/fontconfig/commit/?id=8c255fb) | Usa `"$XDG_DATA_HOME"/fonts` para armazenar fones. |
| [fontforge](https://www.archlinux.org/packages/?name=fontforge) | 

`~/.FontForge
~/.PfaEdit`

 | [e4c2cc7](https://github.com/fontforge/fontforge/commit/e4c2cc7) | 

[[14]](https://github.com/fontforge/fontforge/issues/847) [[15]](https://github.com/fontforge/fontforge/issues/991)

 |
| [freerdp](https://www.archlinux.org/packages/?name=freerdp) | `~/.freerdp` | [edf6e72](https://github.com/FreeRDP/FreeRDP/commit/edf6e72) |
| [Gajim](/index.php/Gajim "Gajim") | `~/.gajim` | [3e777ea](https://dev.gajim.org/gajim/gajim/commit/3e777ea) | [[16]](https://dev.gajim.org/gajim/gajim/issues/2149) |
| [gconf](https://www.archlinux.org/packages/?name=gconf) | `~/.gconf` | [fc28caa](https://gitlab.gnome.org/Archive/gconf/commit/fc28caa) | [[17]](https://bugzilla.gnome.org/show_bug.cgi?id=674803) |
| [GIMP](/index.php/GIMP "GIMP") | 

`~/.gimp-x.y
~/.thumbnails`

 | 

[60e0cfe](https://gitlab.gnome.org/GNOME/gimp/commit/60e0cfe) [483505f](https://gitlab.gnome.org/GNOME/gimp/commit/483505f)

 | 

[[18]](https://bugzilla.gnome.org/show_bug.cgi?id=166643) [[19]](https://bugzilla.gnome.org/show_bug.cgi?id=646644)

 |
| [Git](/index.php/Git "Git") | `~/.gitconfig` | [0d94427](https://github.com/git/git/commit/0d94427) |
| [GStreamer](/index.php/GStreamer "GStreamer") | `~/.gstreamer-0.10` | [4e36f93](https://cgit.freedesktop.org/gstreamer/gstreamer/commit/?id=4e36f93) | [[20]](https://bugzilla.gnome.org/show_bug.cgi?id=518597) |
| [GTK](/index.php/GTK_(Portugu%C3%AAs) "GTK (Português)") 3 |
| [htop](https://www.archlinux.org/packages/?name=htop) | `~/.htoprc` | [93233a6](https://github.com/hishamhm/htop/commit/93233a6) |
| [i3](/index.php/I3 "I3") | `~/.i3` | [7c130fb](http://code.stapelberg.de/git/i3/commit/?id=7c130fb) |
| [i3status](https://www.archlinux.org/packages/?name=i3status) | `~/.i3status.conf` | [c3f7fc4](http://code.stapelberg.de/git/i3status/commit/?id=c3f7fc4) |
| [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) |
| [Inkscape](/index.php/Inkscape "Inkscape") | `~/.inkscape` | [0.47](http://wiki.inkscape.org/wiki/index.php/Release_notes/0.47#Preferences) | [[21]](https://bugs.launchpad.net/inkscape/+bug/199720) |
| [Kakoune](/index.php/Kakoune "Kakoune") |
| latexmk (em [texlive-core](https://www.archlinux.org/packages/?name=texlive-core)) | `~/.latexmkrc` |
| [lftp](https://www.archlinux.org/packages/?name=lftp) | `~/.lftp` | [21dc400](https://github.com/lavv17/lftp/commit/21dc400) | [[22]](https://www.mail-archive.com/lftp@uniyar.ac.ru/msg04301.html) |
| [lgogdownloader](https://aur.archlinux.org/packages/lgogdownloader/) | `~/.gogdownloader` | [d430af6](https://github.com/Sude-/lgogdownloader/commit/d430af6) | [[23]](https://github.com/Sude-/lgogdownloader/issues/4) |
| [LibreOffice](/index.php/LibreOffice "LibreOffice") | 

[a6f56f7](https://cgit.freedesktop.org/libreoffice/ure/commit/?id=a6f56f7) [25bd2ee](https://cgit.freedesktop.org/libreoffice/bootstrap/commit/?id=25bd2ee)

 | [[24]](https://bugs.documentfoundation.org/show_bug.cgi?id=32263) |
| [Streamlink](/index.php/Streamlink "Streamlink") | `~/.livestreamerrc` | [ea80591](https://github.com/chrippa/livestreamer/commit/ea80591) | [[25]](https://github.com/chrippa/livestreamer/pull/106) |
| [llpp](/index.php/Llpp "Llpp") | [3ab86f0](http://repo.or.cz/w/llpp.git/commit/3ab86f0) | Atualmente, *llpp* coloca a configuração diretamente sob `XDG_CONFIG_HOME`, em vez de criar um diretório. |
| [mc](/index.php/Mc "Mc") | `~/.mc` | 

[1b99570](https://github.com/MidnightCommander/mc/commit/1b99570) [0b71156](https://github.com/MidnightCommander/mc/commit/0b71156) [ce401d7](https://github.com/MidnightCommander/mc/commit/ce401d7)

 | [[26]](https://www.midnight-commander.org/ticket/1851) |
| [Mercurial](/index.php/Mercurial "Mercurial") | `~/.hgrc` | 

[3540200](https://www.mercurial-scm.org/repo/hg/rev/3540200) [4.2](https://www.mercurial-scm.org/wiki/Release4.2)

 | `XDG_CONFIG_HOME/hg/hgrc`. |
| [msmtp](/index.php/Msmtp "Msmtp") | `~/.msmtprc` | 

[af2f409](https://github.com/marlam/msmtp-mirror/commit/af2f409) v1.6.7+

 | `$XDG_CONFIG_HOME"/msmtp/config`. |
| [mesa](https://www.archlinux.org/packages/?name=mesa) | [87ab26b](https://cgit.freedesktop.org/mesa/mesa/commit/?id=87ab26b) | `XDG_CACHE_HOME/mesa` |
| [milkytracker](https://www.archlinux.org/packages/?name=milkytracker) | `~/.milkytracker_config` | [eb487c5](https://github.com/Deltafire/MilkyTracker/commit/eb487c5) | [[27]](https://github.com/Deltafire/MilkyTracker/issues/12) |
| [mpd](/index.php/Mpd "Mpd") | `~/.mpdconf` | [87b7328](https://github.com/MusicPlayerDaemon/MPD/commit/87b7328) |
| [mpv](/index.php/Mpv "Mpv") | `~/.mpv` | [cb250d4](https://github.com/mpv-player/mpv/commit/cb250d4) | [[28]](https://github.com/mpv-player/mpv/pull/864) |
| [mutt](/index.php/Mutt "Mutt") | `~/.mutt` | [b17cd67](https://gitlab.com/muttmua/mutt/commit/b17cd67) | [[29]](https://gitlab.com/muttmua/trac-tickets/raw/master/tickets/closed/3207-Conform_to_XDG_Base_Directory_Specification.txt) |
| [mypaint](https://www.archlinux.org/packages/?name=mypaint) | `~/.mypaint` | [cf723b7](https://github.com/mypaint/mypaint/commit/cf723b7) |
| [nano](/index.php/Nano "Nano") | 

`~/.nano/
~/.nanorc`

 | [c16e79b](http://git.savannah.gnu.org/cgit/nano.git/commit/?id=c16e79b) | [[30]](https://savannah.gnu.org/patch/?8523) |
| [ncmpcpp](/index.php/Ncmpcpp "Ncmpcpp") | `~/.ncmpcpp` | 

[38d9f81](https://github.com/arybczak/ncmpcpp/commit/38d9f81) [27cd86e](https://github.com/arybczak/ncmpcpp/commit/27cd86e)

 | 

[[31]](https://github.com/arybczak/ncmpcpp/issues/79) [[32]](https://github.com/arybczak/ncmpcpp/issues/110)

 | `ncmpcpp_directory` deve ser definido para evitar um arquivo `error.log` em `~/.ncmpcpp`. |
| [Neovim](/index.php/Neovim "Neovim") | 

`~/.nvim
~/.nvimlog
~/.nviminfo`

 | [1ca5646](https://github.com/neovim/neovim/commit/1ca5646) | 

[[33]](https://github.com/neovim/neovim/issues/78) [[34]](https://github.com/neovim/neovim/pull/3198)

 |
| [newsbeuter](/index.php/Newsbeuter "Newsbeuter") | `~/.newsbeuter` | [3c57824](https://github.com/akrennmair/newsbeuter/commit/3c57824) | [[35]](https://github.com/akrennmair/newsbeuter/pull/39) | É necessário criar ambos diretórios [[36]](http://newsbeuter.org/doc/newsbeuter.html#_xdg_base_directory_support):

`$ mkdir -p "$XDG_DATA_HOME"/newsbeuter "$XDG_CONFIG_HOME"/newsbeuter`

 |
| [node-gyp](https://github.com/nodejs/node-gyp) | `~/.node-gyp` | [2b5ce52a](https://github.com/nodejs/node-gyp/commit/2b5ce52a) | [[37]](https://github.com/nodejs/node-gyp/pull/1570) | Disponível apenas no master até 2018-12-04. |
| [np2kai-git](https://aur.archlinux.org/packages/np2kai-git/) | 

`~/.config/np2kai
~/.config/xnp2kai`

 | [56a1cc2](https://github.com/AZO234/NP2kai/commit/56a1cc2) | [[38]](https://github.com/AZO234/NP2kai/pull/50) |
| [nteract-bin](https://aur.archlinux.org/packages/nteract-bin/) | [4593e72](https://github.com/nteract/nteract/commit/4593e72) | [[39]](https://github.com/nteract/nteract/issues/180) [[40]](https://github.com/nteract/nteract/pull/3870) | [não reconhece soluções alternativas para ipython/jupyter](https://github.com/nteract/nteract/issues/4517) |
| [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP") | `~/.offlineimaprc` | [5150de5](https://github.com/OfflineIMAP/offlineimap/commit/5150de5) | [[41]](https://github.com/OfflineIMAP/offlineimap/issues/32) |
| [opentyrian](https://aur.archlinux.org/packages/opentyrian/) | `~/.opentyrian` | [8d45ff2](https://bitbucket.org/opentyrian/opentyrian/commits/8d45ff2) | [[42]](https://web.archive.org/web/20140815181350/http://code.google.com/p/opentyrian/issues/detail?id=125) |
| [pandoc](https://www.archlinux.org/packages/?name=pandoc) | `~/.pandoc/` | [0bed0ab](https://github.com/jgm/pandoc/commit/0bed0ab5a308f5e72a01fa9bee76488556288862) | [[43]](https://github.com/jgm/pandoc/issues/3582) |
| [pcsx2](https://www.archlinux.org/packages/?name=pcsx2) | `~/.pcsx2` | 

[87f1e8f](https://github.com/PCSX2/pcsx2/commit/87f1e8f) [a9020c6](https://github.com/PCSX2/pcsx2/commit/a9020c6) [3b22f0f](https://github.com/PCSX2/pcsx2/commit/3b22f0f) [0a012ae](https://github.com/PCSX2/pcsx2/commit/0a012ae)

 | [[44]](https://github.com/PCSX2/pcsx2/issues/352) [[45]](https://github.com/PCSX2/pcsx2/issues/381) |
| [Pry](http://pryrepl.org/) | `~/.pryrc
~/.pry_history` | 

[a0be0cc7](https://github.com/pry/pry/commit/a0be0cc7b2070edff61c0c7f10fa37fce9b730bd) [15e1fc92](https://github.com/pry/pry/commit/15e1fc929ed84c161abc5afc9be73488a41df397) [e9d1be0e](https://github.com/pry/pry/commit/e9d1be0e17b294318dbb2f70f74a50486cfa044c)

 | [[46]](https://github.com/pry/pry/issues/1316) |
| [python-pip](https://www.archlinux.org/packages/?name=python-pip) | `~/.pip` | [6.0](https://github.com/pypa/pip/blob/548a9136525815dff41acd845c558a0b36eb1c5f/NEWS.rst#60-2014-12-22) | [[47]](https://github.com/pypa/pip/issues/1733) |
| [powershell](https://aur.archlinux.org/packages/powershell/) | [6.0](https://docs.microsoft.com/en-us/powershell/scripting/whats-new/what-s-new-in-powershell-core-60#filesystem) |
| [ppsspp](https://www.archlinux.org/packages/?name=ppsspp) | `~/.ppsspp` | [132fe47](https://github.com/hrydgard/ppsspp/commit/132fe47) | [[48]](https://github.com/hrydgard/ppsspp/issues/4623) |
| [procps-ng](https://www.archlinux.org/packages/?name=procps-ng) | `~/.toprc` | [af53e17](https://gitlab.com/procps-ng/procps/commit/af53e17) | 

[[49]](https://gitlab.com/procps-ng/procps/merge_requests/38) [[50]](https://bugzilla.redhat.com/show_bug.cgi?id=1155265)

 |
| [orbment-git](https://aur.archlinux.org/packages/orbment-git/) |
| [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") | `~/.makepkg.conf` | [80eca94](https://projects.archlinux.org/pacman.git/commit/?id=80eca94) | [[51]](https://mailman.archlinux.org/pipermail/pacman-dev/2014-July/019178.html) |
| [panda3d](https://aur.archlinux.org/packages/panda3d/) | `~/.panda3d` | [2b537d2](https://github.com/panda3d/panda3d/commit/2b537d2) |
| [PulseAudio](/index.php/PulseAudio "PulseAudio") | 

`~/.pulse
~/.pulse-cookie`

 | 

[59a8618](https://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=59a8618) [87ae830](https://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=87ae830) [9ab510a](https://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=9ab510a) [4c195bc](https://cgit.freedesktop.org/pulseaudio/pulseaudio/commit/?id=4c195bc)

 | [[52]](https://bugzilla.redhat.com/show_bug.cgi?id=845607) |
| [pyroom](https://aur.archlinux.org/packages/pyroom/) |
| [quodlibet](https://www.archlinux.org/packages/?name=quodlibet) | `~/.quodlibet` | 3.10.0 | [[53]](https://github.com/quodlibet/quodlibet/issues/138) |
| [qutebrowser](/index.php/Qutebrowser "Qutebrowser") |
| [qtile](/index.php/Qtile "Qtile") | 

[fd8686e](https://github.com/qtile/qtile/commit/fd8686e) [66d704b](https://github.com/qtile/qtile/commit/66d704b) [51cff01](https://github.com/qtile/qtile/commit/51cff01)

 | [[54]](https://github.com/qtile/qtile/pull/835) | Algumas barras opcionais podem criar arquivos e diretórios em caminhos sem conformidade, mas geralmente eles ainda são configuráveis. |
| [rclone](https://www.archlinux.org/packages/?name=rclone) | `~/.rclone.conf` | [9d36258](https://github.com/ncw/rclone/commit/9d36258) | [[55]](https://github.com/ncw/rclone/issues/868) |
| [retroarch](https://www.archlinux.org/packages/?name=retroarch) |
| [rr](https://aur.archlinux.org/packages/rr/) | `~/.rr` | [02e7d41](https://github.com/mozilla/rr/commit/02e7d41) | [[56]](https://github.com/mozilla/rr/issues/1455) |
| [RSpec](https://rspec.info) | `~/.rspec` | [5e395e2](https://github.com/rspec/rspec-core/commit/5e395e2016f1da19475e6db2817eb26dae828c4c) | [[57]](https://github.com/rspec/rspec-core/issues/1773) |
| [rTorrent](/index.php/RTorrent "RTorrent") | `~/.rtorrent.rc` | [6a8d332](https://github.com/rakshasa/rtorrent/commit/6a8d332) |
| [RuboCop](https://www.rubocop.org) | `~/.rubocop.yml` | [6fe5956](https://github.com/rubocop-hq/rubocop/commit/6fe5956c177ca369cfaa70bdf748b70020a56bf4) | [[58]](https://github.com/rubocop-hq/rubocop/issues/6662) |
| [skypeforlinux-stable-bin](https://aur.archlinux.org/packages/skypeforlinux-stable-bin/) | `~/.Skype` | 8.0 |
| [snes9x](https://www.archlinux.org/packages/?name=snes9x) | `~/.snes9x` | [93b5f11](https://github.com/snes9xgit/snes9x/commit/93b5f11) | [[59]](https://github.com/snes9xgit/snes9x/issues/194) | Por padrão, o arquivo de configuração é deixado em branco com a intenção de que o usuário vá preenchendo-o de acordo com sua própria vontade (por interface gráfica ou manualmente). |
| [sublime-text-dev](https://aur.archlinux.org/packages/sublime-text-dev/) | O cache é colocado em `$XDG_CONFIG_HOME/sublime-text-3/Cache` em vez do esperado `$XDG_CACHE_HOME/sublime-text-3`. |
| [surfraw](/index.php/Surfraw "Surfraw") | 

`~/.surfraw.conf
~/.surfraw.bookmarks`

 | 

[3e4591d](https://gitlab.com/surfraw/Surfraw/commit/3e4591d) [bd8c427](https://gitlab.com/surfraw/Surfraw/commit/bd8c427) [f57fc71](https://gitlab.com/surfraw/Surfraw/commit/f57fc71)

 |
| [sway](/index.php/Sway "Sway") | `~/.sway/config` | [614393c](https://github.com/SirCmpwn/sway/commit/614393c) | [[60]](https://github.com/SirCmpwn/sway/issues/5) |
| [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") |
| [termite](/index.php/Termite "Termite") |
| [tig](https://www.archlinux.org/packages/?name=tig) | `~/.tigrc`, `~/.tig_history` | [2.2](https://github.com/jonas/tig/blob/master/NEWS.adoc#tig-22) | [[61]](https://github.com/jonas/tig/issues/513) | O diretório `~/.local/share/tig` deve existir, do contrário escreve para `~/.tig_history`. |
| [tmuxinator](https://aur.archlinux.org/packages/tmuxinator/) | `~/.tmuxinator` | [2636923](https://github.com/tmuxinator/tmuxinator/pull/511/commits/2636923) | [[62]](https://github.com/tmuxinator/tmuxinator/pull/511) |
| [Transmission](/index.php/Transmission "Transmission") | `~/.transmission` | [b71a298](https://github.com/transmission/transmission/commit/b71a298) |
| [util-linux](https://www.archlinux.org/packages/?name=util-linux) | [570b321](https://git.kernel.org/pub/scm/utils/util-linux/util-linux.git/commit/?id=570b321) |
| [Uzbl](/index.php/Uzbl "Uzbl") | [c6fd63a](https://github.com/uzbl/uzbl/commit/c6fd63a) | [[63]](https://github.com/uzbl/uzbl/pull/150) |
| [vimb](https://www.archlinux.org/packages/?name=vimb) |
| [VirtualBox](/index.php/VirtualBox_(Portugu%C3%AAs) "VirtualBox (Português)") | `~/.VirtualBox` | [4.3](https://www.virtualbox.org/ticket/5099?action=diff&version=7) | [[64]](https://www.virtualbox.org/ticket/5099) |
| [vis](https://www.archlinux.org/packages/?name=vis) | `~/.vis` | 

[68a25c7](https://github.com/martanne/vis/commit/68a25c7) [d138908](https://github.com/martanne/vis/commit/d138908)

 | [[65]](https://github.com/martanne/vis/pull/303) |
| [VLC](/index.php/VLC "VLC") | `~/.vlcrc` | [16f32e1](http://git.videolan.org/?p=vlc.git;a=commit;h=16f32e1) | [[66]](https://trac.videolan.org/vlc/ticket/1267) |
| [Visual Studio Code](/index.php/Visual_Studio_Code "Visual Studio Code") | Note que o diretório de extensões não vai ser movido; veja [[67]](https://github.com/Microsoft/vscode/issues/3884). |
| [warsow](https://www.archlinux.org/packages/?name=warsow) | `~/.warsow-2.x` | [98ece3f](https://github.com/Qfusion/qfusion/commit/98ece3f) | [[68]](https://github.com/Qfusion/qfusion/issues/298) |
| [Wireshark](/index.php/Wireshark_(Portugu%C3%AAs) "Wireshark (Português)") | `~/.wireshark` | [b0b53fa](https://code.wireshark.org/review/gitweb?p=wireshark.git;a=commit;h=b0b53fa) |
| [xsettingsd-git](https://aur.archlinux.org/packages/xsettingsd-git/) | `~/.xsettingsd` | [b4999f5](https://github.com/derat/xsettingsd/commit/b4999f5) |
| [xmonad](/index.php/Xmonad "Xmonad") | `~/.xmonad` | [40fc10b](https://github.com/xmonad/xmonad/commit/40fc10b) | 

[[69]](https://github.com/xmonad/xmonad/issues/61) [[70]](https://code.google.com/p/xmonad/issues/detail?id=484)

 | Alternativamente, as variáveis de ambiente `XMONAD_CONFIG_HOME`, `XMONAD_DATA_HOME` e `XMONAD_CACHE_HOME` também são configuráveis. |
| [xsel](https://www.archlinux.org/packages/?name=xsel) | `~/.xsel.log` | [ee7b481](https://github.com/kfish/xsel/commit/ee7b481) | [[71]](https://github.com/kfish/xsel/issues/10) |
| [yarn](https://www.archlinux.org/packages/?name=yarn) | 

`~/.yarnrc
~/.yarn/
~/.yarncache/
~/.yarn-config/`

 | [2d454b5](https://github.com/yarnpkg/yarn/commit/2d454b5) | [[72]](https://github.com/yarnpkg/yarn/pull/5336) |

### Parcial

| Aplicativo | Caminho legado | Suporte desde | Discussão | Observações |
| [abook](https://www.archlinux.org/packages/?name=abook) | `~/.abook` | `$ abook --config "$XDG_CONFIG_HOME"/abook/abookrc --datafile "$XDG_CACHE_HOME"/abook/addressbook` |
| [ack](https://www.archlinux.org/packages/?name=ack) | `~/.ackrc` | [[73]](https://github.com/beyondgrep/ack2/issues/516) | `$ export ACKRC="$XDG_CONFIG_HOME/ack/ackrc"` |
| [Anki](/index.php/Anki "Anki") | 

`~/Anki
~/Documents/Anki`

 | [[74]](https://github.com/dae/anki/pull/49) [[75]](https://github.com/dae/anki/pull/58) | `$ anki -b "$XDG_DATA_HOME"/Anki` |
| [aspell](/index.php/Aspell_(Portugu%C3%AAs) "Aspell (Português)") | `~/.aspell.conf` | `$ export ASPELL_CONF="per-conf $XDG_CONFIG_HOME/aspell/aspell.conf; personal $XDG_CONFIG_HOME/aspell/en.pws; repl $XDG_CONFIG_HOME/aspell/en.prepl"` |
| [Atom](/index.php/Atom "Atom") | `~/.atom` | [[76]](https://github.com/atom/atom/issues/8281) | `$ export ATOM_HOME="$XDG_DATA_HOME"/atom` |
| [aws-cli](https://www.archlinux.org/packages/?name=aws-cli) | `~/.aws` | [1.7.45](https://github.com/aws/aws-cli/commit/fc5961ea2cc0b5976ac9f777e20e4236fd7540f5) | [[77]](https://github.com/aws/aws-cli/issues/2433) | 

`$ export AWS_SHARED_CREDENTIALS_FILE="$XDG_CONFIG_HOME"/aws/credentials
$ export AWS_CONFIG_FILE="$XDG_CONFIG_HOME"/aws/config`

 |
| [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) | `~/.bash_completion` | `$ export BASH_COMPLETION_USER_FILE="$XDG_CONFIG_HOME"/bash-completion/bash_completion` |
| [bazaar](/index.php/Bazaar "Bazaar") | 

`~/.bazaar
~/.bzr.log`

 | [2.3.0](https://bugs.launchpad.net/bzr/+bug/195397/comments/15) | [[78]](https://bugs.launchpad.net/bzr/+bug/195397) | Discussão no relatório de erro do upstream informa que o bazaar vai usar `~/.config/bazaar` se existir. O arquivo de log `~/.bzr.log` ainda pode ser escrito. |
| [buchhaltung-git](https://aur.archlinux.org/packages/buchhaltung-git/) | 

`~/.buchhaltung`

 | [[79]](https://github.com/johannesgerer/buchhaltung/issues/44) | `$ export BUCHHALTUNG="$XDG_CONFIG_HOME"/buchhaltung` |
| [Ruby#Bundler](/index.php/Ruby#Bundler "Ruby") | `~/.bundle` | [[80]](https://github.com/bundler/bundler/pull/6024) [[81]](https://github.com/bundler/bundler/issues/4333) | `$ export BUNDLE_USER_CONFIG="$XDG_CONFIG_HOME"/bundle BUNDLE_USER_CACHE="$XDG_CACHE_HOME"/bundle BUNDLE_USER_PLUGIN="$XDG_DATA_HOME"/bundle` |
| [calcurse](https://www.archlinux.org/packages/?name=calcurse) | `~/.calcurse` | `$ calcurse -C "$XDG_CONFIG_HOME"/calcurse -D "$XDG_DATA_HOME"/calcurse` |
| [Rust#Cargo](/index.php/Rust#Cargo "Rust") | `~/.cargo` | [[82]](https://github.com/rust-lang/cargo/issues/1734) [[83]](https://github.com/rust-lang/rfcs/pull/1615) [[84]](https://github.com/rust-lang/cargo/pull/5183) [[85]](https://github.com/rust-lang/cargo/pull/148) | `$ export CARGO_HOME="$XDG_DATA_HOME"/cargo` |
| [ccache](/index.php/Ccache_(Portugu%C3%AAs) "Ccache (Português)") | `~/.ccache` | `$ export CCACHE_CONFIGPATH="$XDG_CONFIG_HOME"/ccache.config`

`$ export CCACHE_DIR="$XDG_CACHE_HOME"/ccache`

 |
| [chez-scheme](https://aur.archlinux.org/packages/chez-scheme/) | `~/.chezscheme_history` | `$ petite --eehistory "$XDG_DATA_HOME"/chezscheme/history` |
| [conky](/index.php/Conky "Conky") | `~/.conkyrc` | [00481ee](https://github.com/brndnmtthws/conky/commit/00481ee9a97025e8e2acd7303d080af1948f7980) | [[86]](https://github.com/brndnmtthws/conky/issues/144) | `$ conky --config="$XDG_CONFIG_HOME"/conky/conkyrc` |
| [coreutils](/index.php/Coreutils_(Portugu%C3%AAs) "Coreutils (Português)") | `~/.dircolors` | `$ source $(dircolors "$XDG_CONFIG_HOME"/dircolors)` |
| [crawl](http://www.dungeoncrawl.org/) | `~/.crawl` | A barra ao final é necessária:

`$ export CRAWL_DIR="$XDG_DATA_HOME"/crawl/`

 |
| [CUDA](/index.php/CUDA "CUDA") | `~/.nv` | `$ export CUDA_CACHE_PATH="$XDG_CACHE_HOME"/nv` |
| [dict](/index.php/Dict "Dict") | `~/.dictrc` | `$ dict -c "$XDG_CONFIG_HOME"/dict/dictrc` |
| [Docker](/index.php/Docker "Docker") | `~/.docker` | `$ export DOCKER_CONFIG="$XDG_CONFIG_HOME"/docker` |
| [docker-machine](https://www.archlinux.org/packages/?name=docker-machine) | `~/.docker/machine` | `$ export MACHINE_STORAGE_PATH="$XDG_DATA_HOME"/docker-machine` |
| [DOSBox](/index.php/DOSBox "DOSBox") | `~/.dosbox/dosbox-0.74-2.conf` | [[87]](https://www.vogons.org/viewtopic.php?t=29599) | `$ dosbox -conf "$XDG_CONFIG_HOME"/dosbox/dosbox.conf` |
| [ELinks](/index.php/ELinks "ELinks") | `~/.elinks` | `$ export ELINKS_CONFDIR="$XDG_CONFIG_HOME"/elinks` |
| [emscripten](https://www.archlinux.org/packages/?name=emscripten) | 

`~/.emscripten
~/.emscripten_sanity
~/.emscripten_ports
~/.emscripten_cache__last_clear`

 | [[88]](https://github.com/kripken/emscripten/issues/3624) | 

`$ export EM_CONFIG="$XDG_CONFIG_HOME"/emscripten/config
$ export EM_CACHE="$XDG_CACHE_HOME"/emscripten/cache
$ export EM_PORTS="$XDG_DATA_HOME"/emscripten/cache
$ emcc --em-config "$XDG_CONFIG_HOME"/emscripten/config --em-cache "$XDG_CACHE_HOME"/emscripten/cache`

 |
| [freecad](https://aur.archlinux.org/packages/freecad/) | `~/.FreeCAD` | [[89]](https://www.freecadweb.org/tracker/view.php?id=2956) | `$ freecad -u "$XDG_CONFIG_HOME"/FreeCAD/user.cfg -s "$XDG_CONFIG_HOME"/FreeCAD/system.cfg`

Apesar dessas opções, [freecad](https://aur.archlinux.org/packages/freecad/) ainda vai criar o arquivo `.FreeCAD/cookie`, pois o módulo web o tem [codificado](https://github.com/FreeCAD/FreeCAD/blob/master/src/Mod/Web/Gui/CookieJar.cpp#L55)

 |
| [GDB](/index.php/GDB_(Portugu%C3%AAs) "GDB (Português)") | `~/.gdbinit` | `$ gdb -nh -x "$XDG_CONFIG_HOME"/gdb/init` |
| [get_iplayer](https://aur.archlinux.org/packages/get_iplayer/) | `~/.get_iplayer` | `$ export GETIPLAYERUSERPREFS="$XDG_DATA_HOME"/get_iplayer` |
| [getmail](/index.php/Getmail "Getmail") | `~/.getmail/getmailrc` | `$ getmail --rcfile="$XDG_CONFIG_HOME/getmail/getmailrc" --getmaildir="$XDG_DATA_HOME/getmail"` |
| [gliv](https://aur.archlinux.org/packages/gliv/) | `~/.glivrc` | `$ gliv --glivrc="$XDG_CONFIG_HOME"/gliv/glivrc` |
| [GnuPG](/index.php/GnuPG "GnuPG") | `~/.gnupg` | [[90]](https://bugs.gnupg.org/gnupg/issue1456) [[91]](https://bugs.gnupg.org/gnupg/issue1018) | 

`$ export GNUPGHOME="$XDG_DATA_HOME"/gnupg
$ gpg2 --homedir "$XDG_DATA_HOME"/gnupg`

 |
| [Google Earth](/index.php/Google_Earth "Google Earth") | `~/.googleearth` | Alguns caminhos podem ser alterados com as opções `KMLPath` e `CachePath` em `~/.config/Google/GoogleEarthPlus.conf` |
| [gopass](https://www.archlinux.org/packages/?name=gopass) | `~/.password-store` | Se sobrepõe às configurações em `~/.config/gopass/config.yml`: `~/.config/gopass/config.yml` 
```
root:
path: gpgcli-gitcli-fs+file:///home/<id-usuário>/.config/password-store

```
 |
| [GQ LDAP client](https://sourceforge.net/projects/gqclient) | 

`~/.gq
~/.gq-state`

 | [1.51](https://sourceforge.net/p/gqclient/mailman/message/2053978) | 

`$ export GQRC="$XDG_CONFIG_HOME"/gqrc
$ export GQSTATE="$XDG_DATA_HOME"/gq/gq-state
$ mkdir -p "$(dirname "$GQSTATE")"`

 |
| [Gradle](/index.php/Gradle "Gradle") | `~/.gradle` | [[92]](https://discuss.gradle.org/t/be-a-nice-freedesktop-citizen-move-the-gradle-to-the-appropriate-location-in-linux/2199) | `$ export GRADLE_USER_HOME="$XDG_DATA_HOME"/gradle` |
| [GTK](/index.php/GTK_(Portugu%C3%AAs) "GTK (Português)") 1 | `~/.gtkrc` | `$ export GTK_RC_FILES="$XDG_CONFIG_HOME"/gtk-1.0/gtkrc` |
| [GTK](/index.php/GTK_(Portugu%C3%AAs) "GTK (Português)") 2 | `~/.gtkrc-2.0` | `$ export GTK2_RC_FILES="$XDG_CONFIG_HOME"/gtk-2.0/gtkrc` |
| [hledger](https://www.archlinux.org/packages/?name=hledger) | `~/.hledger.journal` | [[93]](https://github.com/simonmichael/hledger/issues/1081) | `$ export LEDGER_FILE="$XDG_DATA_HOME"/hledger.journal` |
| [httpie](https://www.archlinux.org/packages/?name=httpie) | `~/.httpie` | [[94]](https://github.com/jakubroztocil/httpie/issues/145) | `$ export HTTPIE_CONFIG_DIR="$XDG_CONFIG_HOME"/httpie` |
| [intellij-idea-ce](https://aur.archlinux.org/packages/intellij-idea-ce/) | `~/.IntelliJIdea*` | [[95]](https://youtrack.jetbrains.com/issue/IDEA-22407) | 
```
$ mkdir -p "${XDG_CONFIG_HOME}"/intellij-idea
$ cp /opt/intellij-idea-ce/bin/{idea.properties,idea64.vmoptions} "${XDG_CONFIG_HOME}"/intellij-idea/
$ export IDEA_PROPERTIES="${XDG_CONFIG_HOME}"/intellij-idea/idea.properties
$ export IDEA_VM_OPTIONS="${XDG_CONFIG_HOME}"/intellij-idea/idea.vmoptions
```
 `$XDG_CONFIG_HOME/idea.properties` 
```
# esses são codificados, mas você pode obter a ideia
idea.config.path=${user.home}/.config/intellij-idea
idea.system.path=${user.home}/.cache/intellij-idea
idea.log.path=${user.home}/.cache/intellij-idea/log
idea.plugins.path=${user.home}/.local/share/intellij-idea/plugins

```
 |
| [ipython](http://ipython.org)/[jupyter](/index.php/Jupyter "Jupyter") | `~/.ipython` | [não vai corrigir](https://github.com/ipython/ipython/pull/4457) | 

`$ export IPYTHONDIR="$XDG_CONFIG_HOME"/jupyter
$ export JUPYTER_CONFIG_DIR="$XDG_CONFIG_HOME"/jupyter`

 |
| [irb](https://ruby-doc.org/stdlib/libdoc/irb/rdoc/IRB.html) | `~/.irbrc` |  `~/.profile`  `$ export IRBRC="$XDG_CONFIG_HOME"/irb/irbrc`  `"$XDG_CONFIG_HOME"/irb/irbrc` 
```
IRB.conf[:SAVE_HISTORY] ||= 1000
IRB.conf[:HISTORY_FILE] ||= File.join(ENV["XDG_DATA_HOME"], "irb", "history")
```
 |
| [irssi](/index.php/Irssi "Irssi") | `~/.irssi` | [[96]](https://github.com/irssi/irssi/pull/511) | `$ irssi --config="$XDG_CONFIG_HOME"/irssi/config --home="$XDG_DATA_HOME"/irssi` |
| [isync](/index.php/Isync "Isync") | `~/.mbsyncrc` | `$ mbsync -c "$XDG_CONFIG_HOME"/isync/mbsyncrc` |
| [Java (Português)#OpenJDK](/index.php/Java_(Portugu%C3%AAs)#OpenJDK "Java (Português)") | `~/.java/.userPrefs` | [[97]](https://bugzilla.redhat.com/show_bug.cgi?id=1154277) | `$ export _JAVA_OPTIONS=-Djava.util.prefs.userRoot="$XDG_CONFIG_HOME"/java` |
| [ledger](/index.php/Ledger "Ledger") | `~/.ledgerrc`, `~/.pricedb` | [[98]](https://github.com/ledger/ledger/issues/1820) | `$ ledger --init-file "$XDG_CONFIG_HOME"/ledgerrc` |
| [less](/index.php/Utilit%C3%A1rios_principais "Utilitários principais") | `~/.lesshst` | 

`$ mkdir -p "$XDG_CACHE_HOME"/less
$ export LESSKEY="$XDG_CONFIG_HOME"/less/lesskey
$ export LESSHISTFILE="$XDG_CACHE_HOME"/less/history`

`$ export LESSHISTFILE=-` pode ser usado para desabilitar esse recurso.

 |
| [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss) | `~/.dvdcss` | [[99]](https://mailman.videolan.org/pipermail/libdvdcss-devel/2014-August/001022.html) | `$ export DVDCSS_CACHE="$XDG_DATA_HOME"/dvdcss` |
| [libice](https://www.archlinux.org/packages/?name=libice) | `~/.ICEauthority` | [[100]](https://gitlab.freedesktop.org/xorg/lib/libice/issues/2) | `$ export ICEAUTHORITY="$XDG_CACHE_HOME"/ICEauthority`

Certifique-se que `XDG_CACHE_HOME` esteja definido antes para o usuário do diretório que está usando [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") tenha acesso de escrita ao mesmo.

**Não** use `XDG_RUNTIME_DIR`, pois ele está disponível **após** o início da sessão, do contrário os gerenciadores de exibição que iniciam [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") (como o [GDM](/index.php/GDM_(Portugu%C3%AAs) "GDM (Português)")) vão falhar repetidamente.

 |
| [libx11](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") | 

`~/.XCompose
~/.compose-cache`

 | 

`$ export XCOMPOSEFILE="$XDG_CONFIG_HOME"/X11/xcompose
$ export XCOMPOSECACHE="$XDG_CACHE_HOME"/X11/xcompose`

 |
| [ltrace](https://www.archlinux.org/packages/?name=ltrace) | `~/.ltrace.conf` | `$ ltrace -F "$XDG_CONFIG_HOME"/ltrace/ltrace.conf` |
| [maven](https://www.archlinux.org/packages/?name=maven) | `~/.m2` | [[101]](https://issues.apache.org/jira/browse/MNG-6603) | `$ mvn -gs "$XDG_CONFIG_HOME"/maven/settings.xml` `[settings.xml](http://maven.apache.org/settings.html)` 
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
| [mednafen](https://www.archlinux.org/packages/?name=mednafen) | `~/.mednafen` | `$ export MEDNAFEN_HOME="$XDG_CONFIG_HOME"/mednafen` |
| [MOC](/index.php/MOC "MOC") | `~/.moc` | 

`$ mocp -M "$XDG_CONFIG_HOME"/moc
$ mocp -O MOCDir="$XDG_CONFIG_HOME"/moc`

 |
| [monero](https://aur.archlinux.org/packages/monero/) | `~/.bitmonero` | `$ monerod --data-dir "$XDG_DATA_HOME"/bitmonero` |
| [most](https://www.archlinux.org/packages/?name=most) | `~/.mostrc` | `$ export MOST_INITFILE="$XDG_CONFIG_HOME"/mostrc` |
| [MPlayer](/index.php/MPlayer "MPlayer") | `~/.mplayer` | `$ export MPLAYER_HOME="$XDG_CONFIG_HOME"/mplayer` |
| [MySQL](/index.php/MySQL "MySQL") | `~/.mysql_history` | `$ export MYSQL_HISTFILE="$XDG_DATA_HOME"/mysql_history` |
| [ncurses](https://www.archlinux.org/packages/?name=ncurses) | `~/.terminfo` | Preclui a pesquisa de caminho do sistema:

`$ export TERMINFO="$XDG_DATA_HOME"/terminfo
$ export TERMINFO_DIRS="$XDG_DATA_HOME"/terminfo:/usr/share/terminfo`

 |
| [ncmpc](https://www.archlinux.org/packages/?name=ncmpc) | `~/.ncmpc` | `ncmpc -f "$XDG_CONFIG_HOME"/ncmpc/config` |
| [Netbeans](/index.php/Netbeans "Netbeans") | `~/.netbeans` | [[102]](https://netbeans.org/bugzilla/show_bug.cgi?id=215961) | `$ netbeans --userdir "${XDG_CONFIG_HOME}"/netbeans` |
| [Node.js](/index.php/Node.js "Node.js") | `~/.node_repl_history` | `$ export NODE_REPL_HISTORY="$XDG_DATA_HOME"/node_repl_history` [[103]](https://nodejs.org/api/repl.html#repl_environment_variable_options) |
| [notmuch](/index.php/Notmuch "Notmuch") | `~/.notmuch-config` | [[104]](http://notmuchmail.org/pipermail/notmuch/2011/007007.html) | 

`$ export NOTMUCH_CONFIG="$XDG_CONFIG_HOME"/notmuch/notmuchrc
$ export NMBGIT="$XDG_DATA_HOME"/notmuch/nmbug`

 |
| [npm](https://www.archlinux.org/packages/?name=npm) | 

`~/.npm
~/.npmrc`

 | [[105]](https://github.com/npm/npm/issues/6675) | `$ export NPM_CONFIG_USERCONFIG=$XDG_CONFIG_HOME/npm/npmrc` `npmrc` 
```
prefix=$XDG_DATA_HOME/npm
cache=$XDG_CACHE_HOME/npm
tmp=$XDG_RUNTIME_DIR/npm
init-module=$XDG_CONFIG_HOME/npm/config/npm-init.js

```

`prefix` é desnecessário (e não há suporte) se o Node.js for instalado por [nvm](https://aur.archlinux.org/packages/nvm/).

 |
| [nuget](https://www.archlinux.org/packages/?name=nuget) | `~/.nuget/packages` | [[106]](https://docs.microsoft.com/en-us/nuget/consume-packages/managing-the-global-packages-and-cache-folders) | `$ export NUGET_PACKAGES="$XDG_CACHE_HOME"/NuGetPackages` |
| [NVIDIA](/index.php/NVIDIA "NVIDIA") | `~/.nv` | Usa `XDG_CACHE_HOME` se definido, do contrário retrocede inadequadamente para `~/.nv` em vez de `~/.cache`. |
| [nvidia-settings](https://www.archlinux.org/packages/?name=nvidia-settings) | `~/.nvidia-settings-rc` | `$ nvidia-settings --config="$XDG_CONFIG_HOME"/nvidia/settings` |
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

Deve-se fornecer à opção `local_list` um caminho absoluto.

 |
| [openscad](https://www.archlinux.org/packages/?name=openscad) | `~/.OpenSCAD` | [7c3077b0f](https://github.com/openscad/openscad/commit/7c3077b0f) | [[107]](https://github.com/openscad/openscad/issues/125) | Não honra totalmente a XDG Base Directory Specification, veja [[108]](https://github.com/openscad/openscad/issues/373)

Atualmente, ele [codifica](https://github.com/openscad/openscad/blob/master/src/PlatformUtils-posix.cc#L20) `~/.local/share`.

 |
| [OpenSSL](/index.php/OpenSSL "OpenSSL") | `~/.rnd` | O local do arquivo semeador `.rnd` pode ser definido com a varável de ambiente `RANDFILE` conforme [FAQ](https://www.openssl.org/docs/faq.html). |
| [parallel](https://www.archlinux.org/packages/?name=parallel) | `~/.parallel` | [20170422](https://git.savannah.gnu.org/cgit/parallel.git/commit/?id=685018f532f4e2d24b84eb28d5de3d759f0d1af1) | `$ export PARALLEL_HOME="$XDG_CONFIG_HOME"/parallel` |
| [Pass](/index.php/Pass "Pass") | `~/.password-store` | `$ export PASSWORD_STORE_DIR="$XDG_DATA_HOME"/pass` |
| [Pidgin](/index.php/Pidgin "Pidgin") | `~/.purple` | [[109]](https://developer.pidgin.im/ticket/4911) | `$ pidgin --config="$XDG_DATA_HOME"/purple` |
| [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") | 

`~/.psqlrc
~/.psql_history
~/.pgpass
~/.pg_service.conf`

 | 9.2 | [[110]](https://www.postgresql.org/docs/current/static/app-psql.html) [[111]](https://www.postgresql.org/docs/current/static/libpq-envars.html) | 

`$ export PSQLRC="$XDG_CONFIG_HOME/pg/psqlrc"
$ export PSQL_HISTORY="$XDG_CACHE_HOME/pg/psql_history"
$ export PGPASSFILE="$XDG_CONFIG_HOME/pg/pgpass"
$ export PGSERVICEFILE="$XDG_CONFIG_HOME/pg/pg_service.conf"`

É necessário criar ambos diretórios: `$ mkdir "$XDG_CONFIG_HOME/pg" && mkdir "$XDG_CACHE_HOME/pg"`

 |
| [PulseAudio](/index.php/PulseAudio_(Portugu%C3%AAs) "PulseAudio (Português)") | `~/.esd_auth` | Provavelmente gerado pelo módulo `module-esound-protocol-unix.so`. Ele pode ser configurado para usar um local diferente, mas faz muito mais sentido apenas comentar este módulo em `/etc/pulse/default.pa` ou `"$XDG_CONFIG_HOME"/pulse/default.pa`. |
| [python-azure-cli](https://aur.archlinux.org/packages/python-azure-cli/) | `~/.azure` | `$ export AZURE_CONFIG_DIR=$XDG_DATA_HOME/azure` |
| [python-setuptools](https://www.archlinux.org/packages/?name=python-setuptools) | `~/.python-eggs` | `$ export PYTHON_EGG_CACHE="$XDG_CACHE_HOME"/python-eggs` |
| [python-pylint](https://www.archlinux.org/packages/?name=python-pylint) | `~/.pylint.d` | [não vai corrigir](https://github.com/PyCQA/pylint/issues/1364) | `$ export PYLINTHOME="$XDG_CACHE_HOME"/pylint` |
| [racket](https://www.archlinux.org/packages/?name=racket) | `~/.racketrc
`

`~/.racket`

 | [[112]](https://github.com/racket/racket/issues/2740) | `$ export PLTUSERHOME="$XDG_DATA_HOME"/racket` |
| [readline](/index.php/Readline "Readline") | `~/.inputrc` | `$ export INPUTRC="$XDG_CONFIG_HOME"/readline/inputrc` |
| [rlwrap](https://www.archlinux.org/packages/?name=rlwrap) | `~/.*_history` | [[113]](https://github.com/hanslub42/rlwrap/issues/25) | `$ export RLWRAP_HOME="$XDG_DATA_HOME"/rlwrap` |
| [Ruby#RubyGems](/index.php/Ruby#RubyGems "Ruby") | `~/.gem` | 

`$ export GEM_HOME="$XDG_DATA_HOME"/gem
$ export GEM_SPEC_CACHE="$XDG_CACHE_HOME"/gem`

Certifique-se de remover `gem: --user-install` de `/etc/gemrc`

 |
| [Rust#Rustup](/index.php/Rust#Rustup "Rust") | `~/.rustup` | [[114]](https://github.com/rust-lang-nursery/rustup.rs/issues/247) | `$ export RUSTUP_HOME="$XDG_DATA_HOME"/rustup` |
| [sbt](https://www.archlinux.org/packages/?name=sbt) | `~/.sbt`

`~/.ivy2`

 | [[115]](https://github.com/sbt/sbt/issues/3681) | `$ sbt -ivy "$XDG_DATA_HOME"/ivy2 -sbt-dir "$XDG_DATA_HOME"/sbt` (cuidado com [[116]](https://github.com/sbt/sbt/issues/3598)) |
| [GNU Screen](/index.php/GNU_Screen "GNU Screen") | `~/.screenrc` | `$ export SCREENRC="$XDG_CONFIG_HOME"/screen/screenrc` |
| [Haskell#Stack](/index.php/Haskell#Stack "Haskell") | `~/.stack` | [[117]](https://github.com/commercialhaskell/stack/issues/342) | `$ export STACK_ROOT="$XDG_DATA_HOME"/stack` |
| [subversion](/index.php/Subversion "Subversion") | `~/.subversion` | [[118]](https://issues.apache.org/jira/browse/SVN-4599) [[119]](https://mail-archives.apache.org/mod_mbox/subversion-users/201204.mbox/%3c4F8FBCC6.4080205@ritsuka.org%3e)[[120]](http://mail-archives.apache.org/mod_mbox/subversion-dev/201509.mbox/%3c20150917222954.GA20331@teapot%3e) | `$ svn --config-dir "$XDG_CONFIG_HOME"/subversion` |
| [task](https://www.archlinux.org/packages/?name=task) | 

`~/.task
~/.taskrc`

 | 

`$ export TASKDATA="$XDG_DATA_HOME"/task
$ export TASKRC="$XDG_CONFIG_HOME"/task/taskrc`

 |
| [tiptop](https://aur.archlinux.org/packages/tiptop/) | `~/.tiptoprc` | Ele ainda vai espera haver o arquivo `.tiptoprc`.

`$ tiptop -W "$XDG_CONFIG_HOME"/tiptop`

 |
| [tmux](/index.php/Tmux "Tmux") | `~/.tmux.conf` | [[121]](https://github.com/tmux/tmux/issues/142) | `$ tmux -f "$XDG_CONFIG_HOME"/tmux/tmux.conf`

`$ export TMUX_TMPDIR="$XDG_RUNTIME_DIR"`

 |
| [uncrustify](https://www.archlinux.org/packages/?name=uncrustify) | `~/.uncrustify.cfg` | `$ export UNCRUSTIFY_CONFIG="$XDG_CONFIG_HOME"/uncrustify/uncrustify.cfg` |
| [Unison](/index.php/Unison "Unison") | `~/.unison` | `$ export UNISON="$XDG_DATA_HOME"/unison` |
| [urxvtd](/index.php/Rxvt-unicode/Tips_and_tricks#Daemon-client "Rxvt-unicode/Tips and tricks") | `~/.urxvt/urxvtd-hostname` | `$ export RXVT_SOCKET="$XDG_RUNTIME_DIR"/urxvtd` |
| [Vagrant](/index.php/Vagrant "Vagrant") | 

`~/.vagrant.d
~/.vagrant.d/aliases`

 | [[122]](https://www.vagrantup.com/docs/other/environmental-variables.html) | 

`$ export VAGRANT_HOME="$XDG_DATA_HOME"/vagrant
$ export VAGRANT_ALIAS_FILE="$XDG_DATA_HOME"/vagrant/aliases`

 |
| [WeeChat](/index.php/WeeChat "WeeChat") | `~/.weechat` | [[123]](http://savannah.nongnu.org/task/?10934) [[124]](https://github.com/ipython/ipython/pull/4457) | 

`$ export WEECHAT_HOME="$XDG_CONFIG_HOME"/weechat
$ weechat -d "$XDG_CONFIG_HOME"/weechat`

 |
| [wget](/index.php/Wget "Wget") | 

`~/.wgetrc
~/.wget-hsts`

 | 

`$ export WGETRC="$XDG_CONFIG_HOME/wgetrc"
`
e adicionar o seguinte como um alias para wget:
`$ wget --hsts-file="$XDG_CACHE_HOME/wget-hsts"`
ou definir a variável `hsts-file` com um caminho absoluto, pois `wgetrc` não tem suporte a variáveis de ambiente:
`$ echo hsts-file \= "$XDG_CACHE_HOME"/wget-hsts >> "$XDG_CONFIG_HOME/wgetrc"`

 |
| [wine](/index.php/Wine "Wine") | `~/.wine` | [[125]](https://bugs.winehq.org/show_bug.cgi?id=20888) | [Winetricks](/index.php/Wine#Winetricks "Wine") usa local tipo XDG abaixo para gerenciamento de [WINEPREFIX](/index.php/Wine#WINEPREFIX "Wine"):

`$ mkdir -p "$XDG_DATA_HOME"/wineprefixes
$ export WINEPREFIX="$XDG_DATA_HOME"/wineprefixes/default`

 |
| [xbindkeys](/index.php/Xbindkeys "Xbindkeys") | `~/.xbindkeysrc` | `$ xbindkeys -f "$XDG_CONFIG_HOME"/xbindkeys/config` |
| [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth) | `~/.Xauthority` | `$ export XAUTHORITY="$XDG_RUNTIME_DIR"/Xauthority` |
| [xinit](/index.php/Xinit_(Portugu%C3%AAs) "Xinit (Português)") | 

`~/.xinitrc
~/.xserverrc`

 | [[126]](https://gitlab.freedesktop.org/xorg/app/xinit/issues/14) | 

`$ export XINITRC="$XDG_CONFIG_HOME"/X11/xinitrc
$ export XSERVERRC="$XDG_CONFIG_HOME"/X11/xserverrc`

Note que essas variáveis são respeitadas pelo *xinit*, mas não pelo *startx*. Em vez disso, especifique o nome de arquivo como um argumento:

`$ startx "$XDG_CONFIG_HOME/X11/xinitrc" -- "$XDG_CONFIG_HOME/X11/xserverrc" vt1`

 |
| [xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb) | 

`~/.Xresources
~/.Xdefaults`

 | Em última análise, você [deve estar](https://superuser.com/questions/243914/xresources-or-xdefaults) usando `Xresources` e já que esses recursos são carregados por meio de `xrdb`, você pode especificar um caminho como `$ xrdb -load ~/.config/X11/xresources`. |
| [z](https://www.archlinux.org/packages/?name=z) | 

`~/.z`

 | [[127]](https://github.com/rupa/z/issues/267) | `$ export _Z_DATA="$XDG_DATA_HOME/z"` |

### Codificado

| Aplicativo | Caminho legal | Discussão | Observações |
| [adb](/index.php/Adb "Adb") | `~/.android/` | [[128]](https://developer.android.com/studio/command-line/variables.html#android_sdk_root) | `$ export ANDROID_SDK_HOME="$XDG_CONFIG_HOME"/android` |
| [AMule](/index.php/AMule "AMule") | `~/.aMule` |
| [Android Studio](https://developer.android.com/studio/index.html) | 

`~/.AndroidStudio2.3
~/.android/
~/.java/`

 |
| [anthy](https://osdn.net/projects/anthy/) | `~/.anthy` | [[129]](https://osdn.net/ticket/browse.php?group_id=14&tid=28397) |
| [Apache Directory Studio](https://directory.apache.org/studio/) | `~/.ApacheDirectoryStudio` |
| [ARandR](https://christian.amsuess.com/tools/arandr/) | `~/.screenlayout` |
| [Arduino](/index.php/Arduino "Arduino") | 

`~/.arduino15
~/.jssc`

 | [não vai corrigir](https://github.com/arduino/Arduino/issues/3915) |
| [Audacity](https://www.audacityteam.org/) | `~/.audacity-data/` |
| [Avidemux](http://fixounet.free.fr/avidemux/) | `~/.avidemux6` |
| [Bash](/index.php/Bash "Bash") | 

`~/.bashrc
~/.bash_history
~/.bash_profile
~/.bash_login
~/.bash_logout`

 | [não vai corrigir](http://savannah.gnu.org/support/?108134) | `$ export HISTFILE="$XDG_DATA_HOME"/bash/history`

Um `bashrc` especificado pode ser carregado a partir de `/etc/bashrc`.

Especifique `--init-file <arquivo>` como uma alternativa a `~/.bashrc` para shells interativos.

 |
| [cabal](https://www.haskell.org/cabal/) | `~/.cabal/` | [[130]](https://github.com/haskell/cabal/issues/680) | Veja a discussão para soluções alternativas em potencial. Não é muito fácil ou direta, mas pode ser possível emular a conformidade com Base Directory. |
| [chatty](https://aur.archlinux.org/packages/chatty/) | `~/.chatty/` | [[131]](https://github.com/chatty/chatty/issues/273) |
| [cmake](https://www.archlinux.org/packages/?name=cmake) | `~/.cmake/` | Usado para registro de pacote de usuário `~/.cmake/packages/<pacote>`, detalhado em [cmake-packages(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cmake-packages.7#User_Package_Registry) e [na página wiki de Package registry](https://gitlab.kitware.com/cmake/community/wikis/doc/tutorials/Package-Registry). Parece que é codificado, por exemplo em [cmFindPackageCommand.cxx](https://gitlab.kitware.com/cmake/cmake/blob/v3.12.1/Source/cmFindPackageCommand.cxx#L1221). |
| [Cinnamon](/index.php/Cinnamon "Cinnamon") | `~/.cinnamon/` | [[132]](https://github.com/linuxmint/Cinnamon/issues/7807) |
| [cryptomator](https://aur.archlinux.org/packages/cryptomator/) | `~/.Cryptomator` | [[133]](https://github.com/cryptomator/cryptomator/issues/710) |
| [CUPS](/index.php/CUPS "CUPS") | `~/.cups/` | [não vai corrigir](https://github.com/apple/cups/issues/4243) |
| [darcs](/index.php/Darcs "Darcs") | `~/.darcs/` | [[134]](http://bugs.darcs.net/issue2453) |
| [dbus](/index.php/Dbus "Dbus") | `~/.dbus/` | [[135]](https://gitlab.freedesktop.org/dbus/dbus/issues/46) | Isso deve ser evitável com kdbus [citação necessária]. |
| [devede](https://www.archlinux.org/packages/?name=devede) | `~/.devedeng` | Codificado [aqui](https://gitlab.com/rastersoft/devedeng/blob/f0893b3ff7b14723bd148db35bdfe2d284156d19/src/devedeng/configuration_data.py#L111) |
| [Dia](https://wiki.gnome.org/Apps/Dia) | `~/.dia/` |
| [dotnet-sdk](https://www.archlinux.org/packages/?name=dotnet-sdk) | `~/.dotnet/` | [[136]](https://github.com/dotnet/cli/issues/7569) |
| [Eclipse](/index.php/Eclipse "Eclipse") | `~/.eclipse/` | [[137]](https://bugs.eclipse.org/bugs/show_bug.cgi?id=200809) | A opção `-Dosgi.configuration.area=@user.home/.config/..` sobrescreve, mas deve ser adicionado para `"$ECLIPSE_HOME"/eclipse.ini"` em vez de linha de comando que significa que você tem que ter acesso de escrita para `$ECLIPSE_HOME`. (Arch Linux codifica `$ECLIPSE_HOME` em `/usr/bin/eclipse`) |
| [Emacs](/index.php/Emacs "Emacs") | 

`~/.emacs
~/.emacs.d/`

 | [[138]](http://debbugs.gnu.org/cgi/bugreport.cgi?bug=583) | É possível definir `HOME`, mas tem efeitos colaterais inesperados. Até agora, a abordagem mais promissora é modificar outra variável de ambiente do Emacs para alterar o caminho de carregamento e criar o seu próprio arquivo de site, que pode carregar manualmente o arquivo init, mas altera significativamente o processo de carregamento. |
| [Fetchmail](http://www.fetchmail.info/) | `~/.fetchmailrc` |
| [Firefox](/index.php/Firefox "Firefox") | `~/.mozilla/` | [[139]](https://bugzil.la/259356) |
| [Flatpak (Português)](/index.php/Flatpak_(Portugu%C3%AAs) "Flatpak (Português)") | `~/.var/` | [[140]](https://github.com/flatpak/flatpak/issues/46) [[141]](https://github.com/flatpak/flatpak.github.io/issues/191) [não vai corrigir](https://github.com/flatpak/flatpak/issues/1651) |
| [GHC](https://www.haskell.org/ghc/) | `~/.ghc` | [[142]](https://ghc.haskell.org/trac/ghc/ticket/6077) |
| [ghidra](https://aur.archlinux.org/packages/ghidra/) | [[143]](https://github.com/NationalSecurityAgency/ghidra/issues/908) |
| [Goldendict](/index.php/Goldendict "Goldendict") | `~/.goldendict/` | [[144]](https://github.com/goldendict/goldendict/issues/151) |
| [gramps](https://www.archlinux.org/packages/?name=gramps) | `~/.gramps/` | [[145]](https://gramps-project.org/bugs/view.php?id=8025) |
| [grsync](https://www.archlinux.org/packages/?name=grsync) | `~/.grsync/` | [[146]](https://sourceforge.net/p/grsync/feature-requests/15/) |
| [gtk-recordMyDesktop](http://recordmydesktop.sourceforge.net/about.php) | `~/.gtk-recordmydesktop` |
| [hplip](https://www.archlinux.org/packages/?name=hplip) | `~/.hplip/` | [[147]](https://bugs.launchpad.net/hplip/+bug/307152) |
| [idris](http://www.idris-lang.org/) | `~/.idris` | [[148]](https://github.com/idris-lang/Idris-dev/pull/3456) |
| [Java](/index.php/Java_(Portugu%C3%AAs) "Java (Português)") OpenJDK | `~/.java/fonts` | [[149]](https://bugzilla.redhat.com/show_bug.cgi?id=1154277) |
| [Java](/index.php/Java_(Portugu%C3%AAs) "Java (Português)") OpenJFX | `~/.java/webview` |
| [julia](http://julialang.org/) | 

`~/.juliarc.jl
~/.julia_history`

 | [[150]](https://github.com/JuliaLang/julia/issues/4630) [[151]](https://github.com/JuliaLang/julia/issues/10016) |
| [Linux PAM](http://www.linux-pam.org/) | `~/.pam_environment` | [[152]](https://github.com/linux-pam/linux-pam/issues/7) | Codificado em [modules/pam_env/pam_env.c](https://github.com/linux-pam/linux-pam/blob/master/modules/pam_env/pam_env.c) |
| [lldb](http://lldb.llvm.org/) | 

`~/.lldb
~/.lldbinit`

 |
| [mathomatic](http://www.mathomatic.org/) | 

`~/.mathomaticrc
~/.matho_history`

 | O histórico pode ser movido usando `rlwrap mathomatic -r` com o ambiente `RLWRAP_HOME` definido apropriadamente. |
| [Minecraft](/index.php/Minecraft "Minecraft") | `~/.minecraft/` | [[153]](https://bugs.mojang.com/browse/MCL-2563) |
| [Minetest](/index.php/Minetest "Minetest") | `~/.minetest/` | [não vai corrigir](https://github.com/minetest/minetest/issues/864) [[154]](https://github.com/minetest/minetest/issues/8151) |
| [mongodb](https://www.mongodb.org/) | 

`~/.mongorc.js
~/.dbshell`

 | [[155]](https://jira.mongodb.org/browse/DOCS-5652?jql=text%20~%20%22.mongorc.js%22) | [Esse tópico do Stack Overflow](https://stackoverflow.com/questions/22348604/the-mongorc-js-is-not-found-but-there-is-one/22349050#22349050) sugere uma solução alternativa parcial usando a opção de linha de comando `--norc`. |
| [Nestopia UE](http://0ldsk00l.ca/nestopia/) | `~/.nestopia/` | [não vai corrigir](https://github.com/0ldsk00l/nestopia/pull/292) |
 `~/.netrc` | Assim como `~/.ssh`, muitos programas esperam que esse arquivo esteja aqui. Estes incluem projetos como curl (`CURLOPT_NETRC_FILE`), ftp (`NETRC`), s-nail (`NETRC`), etc. Enquanto alguns deles oferecem locais alternativos configuráveis, muitos não o fazem, como w3m, wget e lftp. |
| [Networkmanager-openvpn](/index.php/Networkmanager-openvpn "Networkmanager-openvpn") | `~/.cert/nm-openvpn` | [[156]](https://gitlab.gnome.org/GNOME/NetworkManager-openvpn/issues/35) |
| [NSS](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS) | `~/.pki` | [[157]](https://bugzilla.mozilla.org/show_bug.cgi?id=818686) |
| [OpenSSH](/index.php/OpenSSH "OpenSSH") | `~/.ssh` | [não vai corrigir](https://bugzilla.mindrot.org/show_bug.cgi?id=2050) | Presume-se estar presente por muitos daemons e clientes de ssh, tal como DropBear e OpenSSH. |
| [palemoon](https://www.palemoon.org/) | `~/.moonchild productions` | [[158]](https://forum.palemoon.org/viewtopic.php?f=5&t=9639) |
| [parsec-bin](https://aur.archlinux.org/packages/parsec-bin/) | `~/.parsec` |
| [pcsxr](https://aur.archlinux.org/packages/pcsxr/) | `~/.pcsxr` | Uma opção `-cfg` existe, mas só pode ser definido relativo a `~/.pcsxr`. |
| [perf](https://perf.wiki.kernel.org/index.php/Main_Page) | `~/.debug` | Codificado em [tools/perf/util/config.c:29](https://github.com/torvalds/linux/blob/master/tools/perf/util/config.c#L29). |
| vários [shells](/index.php/Shell_(Portugu%C3%AAs) "Shell (Português)") e [gerenciadores de exibição](/index.php/Gerenciadores_de_exibi%C3%A7%C3%A3o "Gerenciadores de exibição") | `~/.profile` |
| [python](/index.php/Python "Python") | `~/.python_history` | Todo o histórico de sessões interativas salvas em `~/.python_history` por padrão desde a [versão 3.4](https://bugs.python.org/issue5845), um caminho personalizado ainda pode ser definido na mesma forma como em versões antigas (veja [este exemplo](https://docs.python.org/3/library/readline.html?highlight=readline#example)). |
| [Qt Designer](https://doc.qt.io/qt-5/qtdesigner-manual.html) | `~/.designer` |
| [RedNotebook](http://rednotebook.sourceforge.net/) | `~/.rednotebook` |
| [Remarkable](https://remarkableapp.github.io/linux.html) | `~/.remarkable` |
| [Ren'Py](https://www.renpy.org/) | `~/.renpy` | [[159]](https://github.com/renpy/renpy/issues/1377) |
| [SANE](/index.php/SANE "SANE") | `~/.sane/` | `scanimage` cria um arquivo `.cal` lá |
| [scribus](https://www.archlinux.org/packages/?name=scribus) | `~/.scribus` |
| [sdcv](https://www.archlinux.org/packages/?name=sdcv) | `~/.stardict/` | [[160]](https://github.com/Dushistov/sdcv/issues/51) | A única solução alternativa é modificar `HOME` |
| [SeaMonkey](http://www.seamonkey-project.org/) | `~/.mozilla/` | [[161]](https://bugzil.la/726939) |
| [simplescreenrecorder](https://www.archlinux.org/packages/?name=simplescreenrecorder) | `~/.ssr/` | [[162]](https://github.com/MaartenBaert/ssr/issues/407) | O autor parece não concordar com esse recurso. |
| [Solfege](https://www.gnu.org/software/solfege/solfege.html) | 

`~/.solfege
~/.solfegerc
~/lessonfiles`

 | [[163]](https://savannah.gnu.org/bugs/index.php?50251) |
| [spacemacs](https://spacemacs.org/) | 

`~/.spacemacs
~/.spacemacs.d`

 | [[164]](https://github.com/syl20bnr/spacemacs/issues/3589) |
| [SpamAssassin](https://spamassassin.apache.org/) | `~/.spamassassin` |
| [spectrwm](/index.php/Spectrwm "Spectrwm") | `~/.spectrwm` |
| [SQLite](/index.php/SQLite "SQLite") | 

`~/.sqlite_history
~/.sqliterc`

 | [[165]](https://www.sqlite.org/src/info/696e82f7c82d1720) | `$ export SQLITE_HISTORY=$XDG_DATA_HOME/sqlite_history
`

`$ sqlite3 -init "$XDG_CONFIG_HOME"/sqlite3/sqliterc`

 |
| [Steam](/index.php/Steam "Steam") | 

`~/.steam
~/.steampath
~/.steampid`

 | [[166]](https://github.com/ValveSoftware/steam-for-linux/issues/1890) | Muitos motores de jogo (Unity 3D, Unreal) seguem a especificação, mas publicadores de jogo individual codificam os caminhos em [Steam Auto-Cloud](https://www.ctrl.blog/entry/flatpak-steamcloud-xdg) fazendo os salvamento de jogos sincronizar para diretório errado. |
| [TeamSpeak](/index.php/TeamSpeak "TeamSpeak") | `~/.ts3client` |
| [texinfo](https://www.archlinux.org/packages/?name=texinfo) | `~/.infokey` | `$ info --init-file "$XDG_CONFIG_HOME/infokey"` |
| [TeXmacs](http://www.texmacs.org/) | `~/.TeXmacs` |
| [Thunderbird](/index.php/Thunderbird "Thunderbird") | `~/.thunderbird/` | [[167]](https://bugzil.la/735285) |
| [tllocalmgr](https://git.archlinux.org/users/remy/texlive-localmanager.git/) | `~/.texlive` |
| [vim](/index.php/Vim "Vim") | 

`~/.vim
~/.vimrc
~/.viminfo`

 | [[168]](https://github.com/vim/vim/issues/2034) | A partir de [7.3.1178](https://github.com/vim/vim/commit/6a459902592e2a4ba68), vem com suporte a `~/.vim/vimrc` se `~/.vimrc` não for encontrado.

`$ mkdir -p "$XDG_DATA_HOME"/vim/{undo,swap,backup}`

 `"$XDG_CONFIG_HOME"/vim/vimrc` 
```
set undodir=$XDG_DATA_HOME/vim/undo
set directory=$XDG_DATA_HOME/vim/swap
set backupdir=$XDG_DATA_HOME/vim/backup
set viminfo+='1000,n$XDG_DATA_HOME/vim/viminfo
set runtimepath=$XDG_CONFIG_HOME/vim,$VIMRUNTIME,$XDG_CONFIG_HOME/vim/after

```
 `~/.profile` 
```
export VIMINIT=":source $XDG_CONFIG_HOME"/vim/vimrc

```

*   [https://tlvince.com/vim-respect-xdg](https://tlvince.com/vim-respect-xdg)

 |
| [vimperator](http://www.vimperator.org/) | `~/.vimperatorrc` | [[169]](http://www.mozdev.org/pipermail/vimperator/2009-October/004848.html) | `$ export VIMPERATOR_INIT=":source $XDG_CONFIG_HOME/vimperator/vimperatorrc"`

`$ export VIMPERATOR_RUNTIME="$XDG_CONFIG_HOME"/vimperator`

 |
| [w3m](https://www.archlinux.org/packages/?name=w3m) | `~/.w3m` | [[170]](https://sourceforge.net/p/w3m/feature-requests/31/) |
| [wpa_cli](https://w1.fi/) | `~/.wpa_cli_history` |
| [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) | `~/.gnome` | [[171]](https://bugs.freedesktop.org/show_bug.cgi?id=90775) | Por algum motivo o script `xdg-desktop-menu` codifica `gnome_user_dir="$HOME/.gnome/apps"`. Isso é usado por [chromium](/index.php/Chromium "Chromium") entre outros. |
| [xombrero](https://opensource.conformal.com/wiki/xombrero) | `~/.xombrero` | [[172]](https://github.com/conformal/xombrero/issues/74) |
| [YARD](https://yardoc.org) | `~/.yard` | [[173]](https://github.com/lsegal/yard/issues/1230) | Aceitaria uma Pull Request se alguém quisesse implementá-la. |
| [zenmap](https://nmap.org/zenmap/) [nmap](https://www.archlinux.org/packages/?name=nmap) | `~/.zenmap` | [[174]](http://seclists.org/nmap-dev/2012/q2/163) [[175]](https://github.com/nmap/nmap/issues/590) |
| [zsh](/index.php/Zsh "Zsh") | 

`~/.zshrc
~/.zprofile
~/.zshenv
~/.zlogin
~/.zlogout
~/.histfile
~/.zcompdump`

 | [[176]](http://www.zsh.org/mla/workers/2013/msg00692.html) | Considere exportar `ZDOTDIR=$HOME/.config/zsh` em `~/.zshenv` (isso é codificado por causa de problema de inicialização). Você também poderia adicionar isso a `/etc/zsh/zshenv` e evita a necessidade de quaisquer *dotfiles* em seu `HOME`. Porém, fazer isso requer privilégios de root que não ser viável e é para todo sistema.

`$ export HISTFILE="$XDG_DATA_HOME"/zsh/history`

`$ compinit -d $XDG_CACHE_HOME/zsh/zcompdump-$ZSH_VERSION` [[177]](https://unix.stackexchange.com/questions/391641/separate-path-for-zcompdump-files) /!\ A pasta precisa existir

 |

## Bibliotecas

	C

	[C99: implementação simples do Cloudef](https://github.com/Cloudef/chck/tree/master/chck/xdg).

	JVM

	Java, Kotlin, Clojure, Scala, ...

	[directories-jvm](https://github.com/soc/directories-jvm)

	Go

	[go-appdir](https://github.com/ProtonMail/go-appdir)

	Haskell

	Oficialmente no [diretório](https://hackage.haskell.org/package/directory) desde 1.2.3.0 [ab9d0810ce](https://github.com/haskell/directory/commit/ab9d0810ce).

	[xdg-basedir](https://hackage.haskell.org/package/xdg-basedir)

	Perl

	[File-BaseDir](http://search.cpan.org/dist/File-BaseDir/lib/File/BaseDir.pm)

	[perl-file-xdg](https://github.com/Aerdan/perl-file-xdg)

	Ruby

	[rubyworks/xdg](https://github.com/rubyworks/xdg)

	Rust

	[directories-rs](https://github.com/soc/directories-rs)

	[rust-xdg](https://github.com/whitequark/rust-xdg)

	Python

	[pyxdg](https://freedesktop.org/wiki/Software/pyxdg/)

	Vala

	Suporte embarcado via [GLib.Environment](http://valadoc.org/#!api=glib-2.0/GLib.Environment).

	Veja `get_user_cache_dir`, `get_user_data_dir`, `get_user_config_dir`, etc.

## Veja também

*   [GNOME Goal: XDG Base Directory Specification Usage](https://wiki.gnome.org/Initiatives/GnomeGoals/XDGConfigFolders)
*   [Rob Pike: "Dotfiles" sendo oculto é um erro UNIXv2](https://web.archive.org/web/20180827160401/plus.google.com/+RobPikeTheHuman/posts/R58WgWwN9jp).
*   [systemd-path(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-path.1)
*   [file-hierarchy(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file-hierarchy.7)
*   [Notas do Grawity sobre dotfiles](https://github.com/grawity/dotfiles/blob/master/.dotfiles.notes).
*   [Notas do Grawity sobre variáveis de ambiente](https://github.com/grawity/dotfiles/blob/master/.environ.notes).
*   [ploum.net: Modify Your Application to use XDG Folders](https://ploum.net/207-modify-your-application-to-use-xdg-folders/).
*   A tentativa [PCGamingWiki](https://pcgamingwiki.com/wiki/Home) para documentar se jogos de PC no Linux seguem ou não a XDG Base Directory Specification.