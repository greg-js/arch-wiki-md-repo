콤튼[Compton](/index.php/Compton "Compton")은 컴포지팅 기능을 네이티브하게 지원하지 않는 [window managers](/index.php/Window_managers "Window managers")와 함께 사용하기 좋은 스탠드얼론 컴포짓 매니저 입니다. 콤튼은 [xcompmgr](/index.php/Xcompmgr "Xcompmgr")의 포크버전인 [xcompmgr-dana](http://oliwer.net/xcompmgr-dana/)의 포크입니다. 더 자세한 정보가 필요하다면 [compton github page](https://github.com/chjj/compton)을 읽으십시오.

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
*   [2 사용](#.EC.82.AC.EC.9A.A9)
    *   [2.1 자동실행](#.EC.9E.90.EB.8F.99.EC.8B.A4.ED.96.89)
    *   [2.2 커맨드로 실행](#.EC.BB.A4.EB.A7.A8.EB.93.9C.EB.A1.9C_.EC.8B.A4.ED.96.89)
    *   [2.3 설정파일 사용](#.EC.84.A4.EC.A0.95.ED.8C.8C.EC.9D.BC_.EC.82.AC.EC.9A.A9)
        *   [2.3.1 몇몇 창의 그림자 효과](#.EB.AA.87.EB.AA.87_.EC.B0.BD.EC.9D.98_.EA.B7.B8.EB.A6.BC.EC.9E.90_.ED.9A.A8.EA.B3.BC)
*   [3 다중 모니터](#.EB.8B.A4.EC.A4.91_.EB.AA.A8.EB.8B.88.ED.84.B0)
*   [4 오류 해결](#.EC.98.A4.EB.A5.98_.ED.95.B4.EA.B2.B0)
    *   [4.1 탭 창](#.ED.83.AD_.EC.B0.BD)
    *   [4.2 slock](#slock)
    *   [4.3 dwm & dmenu](#dwm_.26_dmenu)
    *   [4.4 Unable to change the background color with xsetroot](#Unable_to_change_the_background_color_with_xsetroot)
    *   [4.5 Corrupted screen contents with Intel graphics](#Corrupted_screen_contents_with_Intel_graphics)
    *   [4.6 Screen artifacts/screenshot issues when using AMD's Catalyst driver](#Screen_artifacts.2Fscreenshot_issues_when_using_AMD.27s_Catalyst_driver)
    *   [4.7 Errors while trying to daemonize with nvidia drivers](#Errors_while_trying_to_daemonize_with_nvidia_drivers)
    *   [4.8 Lag when using xft fonts](#Lag_when_using_xft_fonts)
    *   [4.9 Flicker](#Flicker)
    *   [4.10 Fullscreen tearing](#Fullscreen_tearing)
*   [5 See also](#See_also)

## 설치

[Install](/index.php/Install "Install")하기 위해선 [compton](https://www.archlinux.org/packages/?name=compton)나 [git](/index.php/Git "Git") 버전인 [compton-git](https://aur.archlinux.org/packages/compton-git/) 중 하나를 설치하면 됩니다.

[Qt](/index.php/Qt "Qt")를 기반한 GUI가 필요하다면 [compton-conf](https://aur.archlinux.org/packages/compton-conf/) 나 [compton-conf-git](https://aur.archlinux.org/packages/compton-conf-git/) 패키지 중 하나를 설치하면 됩니다.

## 사용

콤튼은 세션 중 아무 때나 수동으로 실행되거나 종료될 수 있습니다, 또한 백그라운드에서 ([Daemon](/index.php/Daemon "Daemon")) 프로세스로 자동실행되도록 할 수 있습니다. 컴포지팅 효과를 설정하기 위해서 여러가지 인자를 사용할 수도 있습니다. 사용될 수 있는 인자는 다음과 같습니다:

*   `-b`: 세션 중 백그라운드 ([Daemon](/index.php/Daemon "Daemon")) 프로세스로 실행됩니다 (예: [Openbox](/index.php/Openbox "Openbox") 등의 [window manager](/index.php/Window_manager "Window manager") 에서 자동실행 할 때)
*   `-c`: 그림자 효과를 활성화
*   `-C`: 패널이나 독에 그림자 효과를 비활성화
*   `-G`: 어플리케이션 창이나 드래그-온-드롭 오브젝트에 그림자 효과를 비활성화
*   `--config`: 지정된 설정 파일을 사용

디스플레이 설정, 타이밍 설정, 그리고 메뉴, 윈도우 테두리, 비활성화된 어플리케이션 메뉴 투명도 설정 등 더 많은 옵션들이 존재합니다. 더 많은 정보를 위해서는 [Compton Man Page](https://github.com/chjj/compton/blob/master/man/compton.1.asciidoc)을 확인하십시오.

**Note:** 만약 다른 [composite manager](/index.php/Composite_manager "Composite manager") 가 실행 중이라면, *compton*을 실행하기 전 종료되어야 합니다..

### 자동실행

콤튼을 [Daemon](/index.php/Daemon "Daemon") 프로세스로 자동실행하는 법은 사용 중인 [desktop environment](/index.php/Desktop_environment "Desktop environment") 나 [window manager](/index.php/Window_manager "Window manager") 에 달려있습니다. 예를 들어, [i3](/index.php/I3 "I3")에서는 `~/.i3/config` 파일을 수정해야 하지만, [Openbox](/index.php/Openbox "Openbox")에서는 `~/.config/openbox/autostart` 파일을 수정해야 합니다. 필요하다면, 콤튼은 [xprofile](/index.php/Xprofile "Xprofile") 이나 [Xinitrc](/index.php/Xinitrc "Xinitrc")에서 자동실행될 수도 있습니다. 더 많은 정보를 위해서는 [startup files](/index.php/Startup_files "Startup files")를 읽어보십시오.

### 커맨드로 실행

세션 중에 수동으로 기본 컴포지팅 기능을 활성화하기 위해서는, 다음의 커맨드를 사용하십시오:

```
$ compton

```

세션 중에 혹시 모든 그림자 기능을 사용하지 않으려면 `-C` 과 `-G` 인자가 추가되어져야 합니다:

```
$ compton -CG

```

콤튼을 백그라운드 ([Daemon](/index.php/Daemon "Daemon")) 프로세스로 자동실행하려면, `-b` 인자를 추가해야 합니다:

```
compton -b

```

백그라운드 ([Daemon](/index.php/Daemon "Daemon")) 프로세스에서 모든 그림자 효과를 사용하지 않으려면 `-C` 와 `-G` 인자를 추가해야 합니다:

```
compton -CGb

```

마지막으로, 여러가지 인자와 그에 필요한 값들을 넣어서 실행하는 예입니다:

```
compton -cCGfF -o 0.38 -O 200 -I 200 -t 0 -l 0 -r 3 -D2 -m 0.88

```

### 설정파일 사용

기본 설정파일은 `/etc/xdg/compton.conf`에 있습니다. 수정을 하려면 기본 설정파일을 `~/.config/compton.conf` 나 `~/.compton.conf` 로 복사한 뒤 수정하십시오.

세션 중에 커스텀 설정파일을 사용하려면, 다음 커맨드를 입력하십시오:

```
compton --config *path/to/compton.conf*

```

백그라운드 ([Daemon](/index.php/Daemon "Daemon")) 프로세스로 자동실행하려면, `-b` 인자를 추가하십시오:

```
compton --config *path/to/compton.conf* -b

```

#### 몇몇 창의 그림자 효과

콤튼이 그림자를 그리는 방법 때문에 몇몇 어플리케이션은 그림자 효과가 활성화 되있을 시에 시각적 버그가 있습니다. `shadow-exclude` 옵션을 사용하면 버그가 사라질 수도 있습니다.

예를 들어서, 모든 GTK +3 프로그램에서 그림자 효과를 없애려면, `compton.conf` 의 `shadow-exclude` 에 다음 세팅을 추가하십시오:

```
"_GTK_FRAME_EXTENTS@:c"

```

그림자 효과를 [conky](/index.php/Conky "Conky") 창에서 없애려면, 먼저 `~/.conkyrc` 파일에 다음을 추가하십시오:

```
own_window_class conky

```

그리고 콤튼 설정파일에 다음을 추가하십시오:

```
shadow-exclude = "class_g = 'conky'";

```

[here](https://projects.archlinux.org/svntogit/community.git/tree/trunk/compton.conf?h=packages/compton#n80)에 현재 비활성화된 창들의 리스트가 있습니다.

## 다중 모니터

xinerama 를 사용하지 않고 [multihead](/index.php/Multihead "Multihead") 설정이 되있다면 (X 서버가 하나의 스크린 이상에서 실행 중이라면) 기본적으로 콤튼은 하나의 스크린에서만 실행이 될 것입니다. `-d` 인자를 사용하면 모든 스크린에서 실행시킬 수 있습니다. 예로, 콤튼을 4개의 모니터에서 사용하려면 다음 커맨드를 입력하면 됩니다:

```
seq 0 3 | xargs -l1 -I@ compton -b -d :0.@

```

## 오류 해결

컴포지팅 효과를 다른 프로그램이나 어플리케이션과 함께 사용할 때 설정이 제대로 안 되어져 있다면 시각적 버그가 발생할 수 있습니다.

### 탭 창

투명화 효과가 설정된 창이 탭화 된다면, 아래에 숨어있는 다른 탭 창들이 투명화 효과 때문에 여전히 보여질 수 있습니다. 각각의 탭 창은 또한 개별적으로 그림자를 그리는데, 이는 다수의 그림자 효과가 중첩되어 발생하는 문제를 야기할 수 있습니다.

그림자 효과 중첩을 해결하려면 아래 옵션을 다음 [`shadow-exclude` list](https://projects.archlinux.org/svntogit/community.git/tree/trunk/compton.conf?h=packages/compton#n80)에 추가함으로 해결할 수 있습니다:

```
"_NET_WM_STATE@:32a *= '_NET_WM_STATE_HIDDEN'"

```

Not drawing underlying tabbed windows can be enabled by adding the following to your `compton.conf`:

```
opacity-rule = [
  "95:class_g = 'URxvt' && !_NET_WM_STATE@:32a",
  "0:_NET_WM_STATE@:32a *= '_NET_WM_STATE_HIDDEN'"
];

```

Note that `URxvt` is the Xorg class name of your terminal. Change this if you use a different terminal.

See [[1]](https://www.reddit.com/r/unixporn/comments/330zxl/webmi3_no_more_overlaying_shadows_and_windows_in/) for more information.

### slock

Where inactive window transparency has been enabled (the `-i` argument when running as a command), this may provide troublesome results when also using [slock](/index.php/Slock "Slock"). One solution is to amend the transparency to `0.2`. For example, where running compton arguments as a command:

```
$ compton <any other arguments> -i 0.2

```

Otherwise, where using a configuration file:

```
inactive-dim = 0.2;

```

Alternatively, you may try to exclude slock by its window id, or by excluding all windows with no name.

**Note:** Some programs change their id for every new instance, but slock's appears to be static. Someone more knowledgeable will have to confirm that slock's id is in fact static- until then, use at your own risk.

Exclude all windows with no name from compton using the following options:

```
$ compton <other arguments> --focus-exclude "! name~=''"

```

Find your slock's window id by running the command:

```
$ xwininfo & slock

```

Quickly click anywhere on the screen (before slock exits), then type your password to unlock. You should see the window id in the output:

```
xwininfo: Window id: 0x1800001 (has no name)

```

Take the window id and exclude it from compton with:

```
$ compton <any other arguments> --focus-exclude 'id = 0x1800001'

```

Otherwise, where using a configuration file:

```
focus-exclude = "id = 0x1800001";

```

### dwm & dmenu

dwm's statusbar is not detected by any of compton's functions to automatically exclude window manager elements. Neither dwm statusbar nor dmenu have a static window id. If you want to exclude it from inactive window transparency (or other), you'll have to either patch a window class into the source code of each, or exclude by less precise attributes. The following exmaple is with dwm's status on top, which allows a resolution independent of location exclusion:

```
$ compton <any other arguments> --focus-exclude "x = 0 && y = 0 && override_redirect = true"

```

Otherwise, where using a configuration file:

```
focus-exclude = "x = 0 && y = 0 && override_redirect = true";

```

The override redirect property seems to be false for most windows- having this in the exclusion rule prevents other windows drawn in the upper left corner from being excluded (for example, when dwm statusbar is hidden, x0 y0 will match whatever is in dwm's master stack).

### Unable to change the background color with xsetroot

Currently, compton is incompatible with `xsetroot`'s `-solid` option, a workaround is to use [hsetroot](https://aur.archlinux.org/packages/hsetroot/) to set the background color:

```
$ hsetroot -solid '#000000'

```

For a detailed explanation, please see [https://github.com/chjj/compton/issues/162](https://github.com/chjj/compton/issues/162).

### Corrupted screen contents with Intel graphics

On at least some Intel chipsets, DRI3 is known to cause [trouble](https://bugs.freedesktop.org/show_bug.cgi?id=97916) for compton when the display resolution is changed or a new monitor is connected. This can happen with either the `intel` or `modesetting` driver. A workaround is to [disable DRI3](/index.php/Intel_graphics#DRI3_issues "Intel graphics").

### Screen artifacts/screenshot issues when using AMD's Catalyst driver

Try running compton with

```
--backend xrender

```

or adding

```
backend = "xrender";

```

to your compton.conf file.

For more info, please see [https://github.com/chjj/compton/issues/208](https://github.com/chjj/compton/issues/208)

### Errors while trying to daemonize with nvidia drivers

If you get error `main(): Failed to create new session.` while trying to start compton in background you should try [compton-garnetius-git](https://aur.archlinux.org/packages/compton-garnetius-git/). It also provides a few pulls from upstream that aren't merged yet.

### Lag when using xft fonts

If you experience heavy lag when using Xft fonts in applications such as [xterm](/index.php/Xterm "Xterm") or [urxvt](/index.php/Urxvt "Urxvt") try running with

```
--xrender-sync --xrender-sync-fence

```

or try using the xrender backend.

See [[2]](https://github.com/chjj/compton/issues/152) for more information.

### Flicker

Applies to fully maximized windows (in sessions without any panels) with the default compton.conf caused and resolved by the following option:

```
 unredir-if-possible = false;

```

See [[3]](https://github.com/chjj/compton/issues/402) for more information.

### Fullscreen tearing

If you observe screen tearing of video playback only in fullscreen mode see above.

## See also

*   [Howto: Using Compton for tear-free compositing on XFCE or LXDE](http://ubuntuforums.org/showthread.php?t=2144468&p=12644745#post12644745)