Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Xdg-menu](/index.php/Xdg-menu "Xdg-menu")
*   [Xorg](/index.php/Xorg "Xorg")
*   [xinitrc](/index.php/Xinitrc "Xinitrc")
*   [Start X at Login](/index.php/Start_X_at_Login "Start X at Login")

[윈도우 매니저](https://en.wikipedia.org/wiki/Window_manager "wikipedia:Window manager") (Window Manager, WM)은 그래픽 유저 인터페이스(GUI)의 윈도우 시스템 내에서의 창의 위치와 모양을 관리하는 시스템 소프트웨어이다. 데스크탑 환경([desktop environment](/index.php/Desktop_environment "Desktop environment"), DE)의 일부 혹은 독립된 형태로 사용된다.

*이 문서에서는 '창 관리자' 대신 '윈도우 매니저'라는 용어를 사용한다.*

## Contents

*   [1 개요](#.EA.B0.9C.EC.9A.94)
    *   [1.1 종류](#.EC.A2.85.EB.A5.98)
*   [2 윈도우 매니저 목록](#.EC.9C.88.EB.8F.84.EC.9A.B0_.EB.A7.A4.EB.8B.88.EC.A0.80_.EB.AA.A9.EB.A1.9D)
    *   [2.1 Stacking window managers](#Stacking_window_managers)
    *   [2.2 Tiling window managers](#Tiling_window_managers)
    *   [2.3 Dynamic window managers](#Dynamic_window_managers)
*   [3 출처](#.EC.B6.9C.EC.B2.98)

## 개요

창 관리자(Window Manager)는 그래픽 어플리케이션들이 나타나는 프레임(혹은 윈도우)의 모양이나 동작을 관리하는 X 클라이언트로서 프레임의 경계, 타이틀바, 크기 등을 결정한다. 또한 창 크기 조절 기능이나 [Fluxbox](/index.php/Fluxbox "Fluxbox")와 같은 윈도우 탭 기능 혹은 창 달라붙기 기능(Sticking, [Window Maker](/index.php/Window_Maker "Window Maker")의 Sticking 포함된 기능 [dockapps](http://windowmaker.org/dockapps/) 참고) 등을 제공한다. 몇몇 윈도우 매니저는 응용프로그램 실행을 위한 메뉴나 윈도우 매니저 자체 설정을 위한 간단한 유틸리티들을 제공하기도 한다.

윈도우 매니저는 X 서버와 클라이언트와 상호작용을 위해 [Extended Window Manager Hints](http://standards.freedesktop.org/wm-spec/wm-spec-latest.html) 이라는 표준 정의를 사용한다.

몇몇 윈도우 매니저들은 [desktop environment](/index.php/Desktop_environment "Desktop environment")의 일부로서 개발되어 데스크탑 아이콘, 폰트, 도구모음, 배경화면, 데스크탑 위젯 등의 유저에게 일관된 사용환경을 제공한다.

반면, 그 외의 다른 윈도우 매니저들은 데스크탑 환경의 일부분이 아닌 독립된 형태로 사용되도록 개발되어 사용자들이 사용할 수 있는 프로그램을 직접 선택할 수 있도록 한다. 때문에 사용자 기호에 맞도록 더 가볍고 커스터마이징 된 사용환경을 만들 수 있다. 데스크탑 아이콘이나 툴바, 배경화면, 데스크탑 위젯 등과 같은 부가 기능들은 관련된 어플리케이션들을 추가적으로 설치하여 사용할 수도 있다. (*일반적으로 Gnome에서는* Mutter *또는* Metacity*, KDE에서는* Kwin*을 윈도우 매니저로 사용하고 설치 시 다양한 기본 프로그램이 설치된다. 하지만, 데스크탑 환경을 설치하지 않고 윈도우 매니저만을 설치하여 사용하는 경우 그러한 기본 프로그램이 설치되지 않기 때문에 사용할 수 있는 프로그램을 직접 선택할 수 있다고 언급된 것이다.*)

몇몇 독립된 형태의 윈도우 매니저들(standalone WMs)은 데스크탑 환경의 기본 윈도우 매니저를 대체하여 사용될 수 있기도 하다.

윈도우 매니저를 설치하기 전에, X 서버 설치가 반드시 되어야 한다.([Xorg](/index.php/Xorg "Xorg")를 참고)

### 종류

*   [Stacking](#Stacking_window_managers)(혹은 floating) Stacking 윈도우 매니저는 윈도우즈와 맥 OS X와 같은 운영체제에서 사용된다. 마치 책상 위에 놓여진 종이들처럼 창들을 다른 창들 위에 쌓아 놓는 형태를 가진다. (아치 리눅스 위키 페이지 [Category:Stacking WMs](/index.php/Category:Stacking_WMs "Category:Stacking WMs") 참고.)
*   [Tiling](#Tiling_window_managers) 윈도우 매니저는 Stacking과 다르게 창들이 다른 창 위에 놓여 겹치지지 않는다. 대신, 타일처럼 화면이 분할되며 마우스보다 조합키를 통해 프로그램의 창을 조작하고 관리한다. Tiling 윈도우 매니저는 분할되는 창 레이아웃에 대해 직접 수정이 가능하지만 미리 정의된 레이아웃이 제공되기도 한다. (아치 리눅스 위키 페이지 [Category:Tiling WMs](/index.php/Category:Tiling_WMs "Category:Tiling WMs") 참고.)
*   [Dynamic](#Dynamic_window_managers) 윈도우 매니저는 Tiling 방식과 Floating 방식 사이에서 창 관리 기법을 전환할 수 있는 윈도우 매니저이다. 자세한 정보는 [Category:Dynamic WMs](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs")를 참고한다.

윈도우 매니저들의 비교를 확인하고 싶다면 [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers")와 [Wikipedia:Comparison of X window managers](https://en.wikipedia.org/wiki/Comparison_of_X_window_managers "wikipedia:Comparison of X window managers") 페이지를 참고한다.

## 윈도우 매니저 목록

### Stacking window managers

*   **[2bwm](/index.php/2bwm "2bwm")** — floating 방식의 빠른 윈도우 매니저로서 창 프레임에 2개의 경계선을 가지고 있는 특징이 있다. XCB 라이브러리로 개발되었으며 mcwm 윈도우 매니저를 기초로 하여 Michael Cardell에 의해 개발되었다. 모든 것들이 키보드만으로 접근이 가능하며 포인팅 장치로도 창의 이동이나 크기조절, 창의 우선순위 조절이 가능하다. 2bwm 이라는 이름은 mcwm-beast에서 바뀌었다.

	[https://github.com/venam/2bwm](https://github.com/venam/2bwm) || [2bwm](https://aur.archlinux.org/packages/2bwm/)

*   **aewm** — X11 환경을 위한 윈도우 매니저로서 마우스로도 완벽하게 조작 가능하다. 하지만 1997년에 개발된 것으로 적은 메모리 환경에서 직관적 인터페이스보다 기능 위주의 성능을 추구했던 당시의 트렌드의 영향으로 윈도우 프레임을 제외하고 제공되는 UI는 전무하며 조작키 또한 vi 스타일을 따른다.

	[http://www.red-bean.com/decklin/aewm/](http://www.red-bean.com/decklin/aewm/) || [aewm](https://aur.archlinux.org/packages/aewm/)

*   **[AfterStep](https://en.wikipedia.org/wiki/AfterStep "wikipedia:AfterStep")** — UNIX 환경의 X 윈도우 시스템을 위한 윈도우 매니저이다. NeXTStep 인터페이스 환경에 기초하여 사용자에게 깔끔하고 세련된 데스크탑 환경을 제공한다. 유연한 데스크탑 설정과 UI의 미적 요소들을 개선하고 시스템 자원의 효율적 사용을 목표로 개발되었다.

	[http://www.afterstep.org/](http://www.afterstep.org/) || [afterstep](https://aur.archlinux.org/packages/afterstep/)

*   **[Blackbox](/index.php/Blackbox "Blackbox")** — X 윈도우 시스템을 위한 가볍고 빠른 윈도우 매니저로서 C++로 빌드되었으며 라이브러리의 의존성이 전혀 없는 것이 장점이다.

	[http://blackboxwm.sourceforge.net/](http://blackboxwm.sourceforge.net/) || [blackbox](https://www.archlinux.org/packages/?name=blackbox)

*   **[Compiz](/index.php/Compiz "Compiz")** — 최상위의 창들을 텍스쳐 오브젝트에 바인딩 시키기 위해 GLX_EXT_texture_from_pixmap을 사용하는 OpenGL compositing manager이다. 플러그인 시스템을 사용하고 대부분의 그래픽 하드웨어에서 동작하도록 설계되어 유연한 특징을 가지고 있다.

	[https://launchpad.net/compiz](https://launchpad.net/compiz) || [compiz](https://aur.archlinux.org/packages/compiz/)

*   **cwm** — 처음에는 evilwm에서 파생된 윈도우 매니저이지만 후에 처음부터 다시 작성되었다. cwm은 간단하며 창 검색 기능과 같이 유용한 기능들을 제공한다.

	[http://monkey.org/~marius/cwm/cwm.1.a](http://monkey.org/~marius/cwm/cwm.1.a) || [cwm](https://aur.archlinux.org/packages/cwm/)

*   **eggwm** — 가벼은 QT4/QT5 윈도우 매니저이다.

	[eggwm-qt5](https://aur.archlinux.org/packages/eggwm-qt5/) || [eggwm](https://aur.archlinux.org/packages/eggwm/)

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — Enlightenment는 Linux/X11와 다른 것들을 위한 윈도우 매니저일 뿐만 아니라 전체 라이브러리 집합으로서 이전에 전통적인 툴킷과 씨름해야만 했던 작업들을 손쉽게 미려한 유저 인터페이스로 개발할 수 있도록 해준다.

	[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[evilwm](/index.php/Evilwm "Evilwm")** — X Window System 환경을 위한 'minimalist' 윈도우 매니저이다. 여기서 'minimalist'는 사용하기에 적합하지 않을 정도로 아무런 기능이 없다는 의미보다 윈도우 매니저에서 불필요한 요소들을 제거하였다는 의미로 사용되었다.

	[http://www.6809.org.uk/evilwm/](http://www.6809.org.uk/evilwm/) || [evilwm](https://aur.archlinux.org/packages/evilwm/)

*   **[Fluxbox](/index.php/Fluxbox "Fluxbox")** — Blackbox 0.61.1 코드에서 파생되어 개발된 윈도우 매니저로서 굉장히 가볍고 다루기 간편할 뿐만 아니라 빠르고 강력한 데스크탑 환경을 만들기 위한 주요 기능들도 완벽하게 제공된다. Fluxbox는 C++로 개발되었으며 MIT License를 가지고 있다.

	[http://www.fluxbox.org/](http://www.fluxbox.org/) || [fluxbox](https://www.archlinux.org/packages/?name=fluxbox)

*   **[Flwm](https://en.wikipedia.org/wiki/FLWM "wikipedia:FLWM")** — 몇 가지 윈도우 매니저들에서 아이디어를 조합하여 개발된 윈도우 매니저로서 처음 Chris Cannam이 wm2에 영향을 받아 해당 코드를 기초로 개발되었다.

	[http://flwm.sourceforge.net/](http://flwm.sourceforge.net/) || [flwm](https://aur.archlinux.org/packages/flwm/)

*   **[FVWM](/index.php/FVWM "FVWM")** — 강력한 ICCCM 호환 가상 데스크탑 윈도우 매니저로서 개발도 활발하고 지원도 상당하다.

	[http://www.fvwm.org/](http://www.fvwm.org/) || [fvwm](https://www.archlinux.org/packages/?name=fvwm)

*   **[Gala](http://elementaryos.org/journal/meet-gala-window-manager)** — elementary os의 미려한 윈도우 매니저로서 [Pantheon](/index.php/Pantheon "Pantheon") 패키지에 포함되어 있다. 마찬가지로 compositing manager이며 libmutter 라이브러리로 개발되었다.

	[https://launchpad.net/gala](https://launchpad.net/gala) || [gala-bzr](https://aur.archlinux.org/packages/gala-bzr/)

*   **Goomwwm** — cleanroom 소프트웨어 프로젝트로써 C로 개발된 X11 윈도우 매니저이다. 창을 작은 플로팅 레이아웃으로 관리하며 창 전환, 크기조절, 이동, Tagging, 분할 등의 동작들을 키보드로 조작한다. 빠르고 가벼우며 모드가 없이 Xinerama, EWMH 호환성을 지원한다.

	[http://aerosuidae.net/goomwwm/](http://aerosuidae.net/goomwwm/) || [goomwwm](https://aur.archlinux.org/packages/goomwwm/)

*   **[IceWM](/index.php/IceWM "IceWM")** — X 윈도우 시스템을 위한 윈도우 매니저로서 성능과 심플함에 초점을 두고 개발되었다.

	[http://www.icewm.org/](http://www.icewm.org/) || [icewm](https://www.archlinux.org/packages/?name=icewm)

*   **[jbwm](/index.php?title=Jbwm&action=edit&redlink=1 "Jbwm (page does not exist)")** — jbwm은 evilwm 윈도우 매니저에서 파생된 것으로, 최소 설정 파일의 크기가 대략 16kb이다. 작은 바이너리 크기와 유용성에 집중하였으며 타이틀바와 XFT 타이틀바, 폰트 렌더링에 대하여 컴파일 시에 옵션을 통해 설정할 수 있다. jbwm은 evilwm보다 조합키를 사용하기에 편한 특징을 가지고 있다.

	[https://github.com/jefbed/jbwm](https://github.com/jefbed/jbwm) || [jbwm](https://aur.archlinux.org/packages/jbwm/)

*   **[JWM](/index.php/JWM "JWM")** — X11 윈도우 시스템을 위한 윈도우 매니저로서 C로 작성되었고 Xlib 라이브러리만을 사용한다.

	[http://joewing.net/projects/jwm/index.shtml](http://joewing.net/projects/jwm/index.shtml) || [jwm](https://www.archlinux.org/packages/?name=jwm)

*   **Karmen** — Johan Veehuizen이 작성한 윈도우 매니저 프로그램이다. "동작"만을 위해 고안되었으며 설정파일도, Xlib을 제외한 다른 라이브러리에 대한 의존성도 없다. 창의 포커스 방식은 click-to-focus이며 ICCCM과 EWMH 호환성을 목표로 하고 있다.

	[http://karmen.sourceforge.net/](http://karmen.sourceforge.net/) || [karmen](https://aur.archlinux.org/packages/karmen/)

*   **[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")** — KDE 4.0에서의 기본 윈도우 매니저로서 compositing 지원과 이전 KDE에서 제공되던 모든 기능들을 그대로 지원하면서 Compiz와 비슷한 그래픽 효과도 제공한다.

	[https://techbase.kde.org/Projects/KWin](https://techbase.kde.org/Projects/KWin) || [kwin](https://www.archlinux.org/packages/?name=kwin)

*   **lwm** — X 환경을 위한 윈도우 매니저이지만 관심있는 사람은 아마 없을 것이다. 아이콘, 버튼, 독, 메뉴 등의 기본적인 것이 아무 것도 없다. 심지어 설정할 수 있는 방법조차 없다. 만약 언급된 것들을 원한다면 다른 윈도우 매니저를 찾는 것이 낫다. 본인 컴퓨터의 디스크 공간과 추가적인 물리 메모리를 정복하고 싶은 사용자라면 이 윈도우 매니저가 작은 도움이 될 수도 있다.

	[http://www.jfc.org.uk/software/lwm.html](http://www.jfc.org.uk/software/lwm.html) || [lwm](https://www.archlinux.org/packages/?name=lwm)

*   **Marco** — MATE의 윈도우 매니저로서 Metacity 에서 갈라져 나온 것이다.

	[https://github.com/mate-desktop/marco](https://github.com/mate-desktop/marco) || [marco](https://www.archlinux.org/packages/?name=marco)

*   **[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")** — 작고 안정적이며 본 역할에 충실한 윈도우 매니저로서 GNOME3 이전까지 오랫동안 사랑받아왔다.

	[http://blogs.gnome.org/metacity/](http://blogs.gnome.org/metacity/) || [metacity](https://www.archlinux.org/packages/?name=metacity)

*   **[Muffin](https://en.wikipedia.org/wiki/Mutter_(software)#Muffin "wikipedia:Mutter (software)")** — Cinnamon의 윈도우 매니저이자 compositing 매니저로서 Mutter에서 파생되었다. Clutter를 기반으로 하며 OpenGL을 사용한다.

	[https://github.com/linuxmint/muffin/](https://github.com/linuxmint/muffin/) || [muffin](https://www.archlinux.org/packages/?name=muffin)

*   **[Mutter](https://en.wikipedia.org/wiki/Mutter_(window_manager) "wikipedia:Mutter (window manager)")** — GNOME에서 사용되는 윈도우 매니저이자 compositing 매니저로서 OpenGL을 사용하고 Clutter를 기초로 개발되었다.

	[http://git.gnome.org/browse/mutter/](http://git.gnome.org/browse/mutter/) || [mutter](https://www.archlinux.org/packages/?name=mutter)

*   **[MWM](https://en.wikipedia.org/wiki/Motif_Window_Manager "wikipedia:Motif Window Manager")** — Motif toolkit을 기반로 개발된 윈도우 매니저이다.

	[http://sourceforge.net/projects/motif/](http://sourceforge.net/projects/motif/) || [openmotif](https://www.archlinux.org/packages/?name=openmotif)

*   **[Openbox](/index.php/Openbox "Openbox")** — 커스터마이징의 자유도가 높고 extensive 표준들을 지원하는 윈도우 매니저이다.

	[http://openbox.org/wiki/Main_Page](http://openbox.org/wiki/Main_Page) || [openbox](https://www.archlinux.org/packages/?name=openbox)

*   **[pawm](/index.php/Pawm "Pawm")** — Window manager for the X Window system. So it is not a 'desktop' and does not offer you a huge pile of useless options, just the facilities needed to run your X applications and at the same time having a friendly and easy to use interface.

	[http://www.pleyades.net/pawm/](http://www.pleyades.net/pawm/) || [pawm](https://aur.archlinux.org/packages/pawm/)

*   **[PekWM](/index.php/PekWM "PekWM")** — Window manager that once upon a time was based on the aewm++ window manager, but it has evolved enough that it no longer resembles aewm++ at all. It has a much expanded feature-set, including window grouping (similar to Ion, PWM, or Fluxbox), auto-properties, Xinerama, keygrabber that supports keychains, and much more.

	[http://www.pekwm.org/projects/pekwm](http://www.pekwm.org/projects/pekwm) || [pekwm](https://www.archlinux.org/packages/?name=pekwm)

*   **[Sawfish](/index.php/Sawfish "Sawfish")** — Extensible window manager using a Lisp-based scripting language. Its policy is very minimal compared to most window managers. Its aim is simply to manage windows in the most flexible and attractive manner possible. All high-level WM functions are implemented in Lisp for future extensibility or redefinition.

	[http://sawfish.wikia.com/wiki/Main_Page](http://sawfish.wikia.com/wiki/Main_Page) || [sawfish](https://aur.archlinux.org/packages/sawfish/)

*   **TinyWM** — Tiny window manager created as an exercise in minimalism. It may be helpful in learning some of the very basics of creating a window manager. It is comprised of approximately 50 lines of C. There is also a Python version using python-xlib.

	[http://incise.org/tinywm.html](http://incise.org/tinywm.html) || [tinywm](https://aur.archlinux.org/packages/tinywm/) [tinywm-git](https://aur.archlinux.org/packages/tinywm-git/)

*   **[twm](/index.php/Twm "Twm")** — Window manager for the X Window System. It provides titlebars, shaped windows, several forms of icon management, user-defined macro functions, click-to-type and pointer-driven keyboard focus, and user-specified key and pointer button bindings.

	[http://cgit.freedesktop.org/xorg/app/twm/](http://cgit.freedesktop.org/xorg/app/twm/) || [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm)

*   **[UWM](https://en.wikipedia.org/wiki/UDE "wikipedia:UDE")** — The ultimate window manager for UDE.

	[http://udeproject.sourceforge.net/](http://udeproject.sourceforge.net/) || [ude](https://aur.archlinux.org/packages/ude/)

*   **WindowLab** — Small and simple window manager of novel design. It has a click-to-focus but not raise-on-focus policy, a window resizing mechanism that allows one or many edges of a window to be changed in one action, and an innovative menubar that shares the same part of the screen as the taskbar. Window titlebars are prevented from going off the edge of the screen by constraining the mouse pointer, and when appropriate the pointer is also constrained to the taskbar/menubar in order to make target menu items easier to hit.

	[http://nickgravgaard.com/windowlab/](http://nickgravgaard.com/windowlab/) || [windowlab](https://www.archlinux.org/packages/?name=windowlab)

*   **[Window Maker](/index.php/Window_Maker "Window Maker")** — X11 window manager originally designed to provide integration support for the GNUstep Desktop Environment. In every way possible, it reproduces the elegant look and feel of the NEXTSTEP user interface. It is fast, feature rich, easy to configure, and easy to use. It is also free software, with contributions being made by programmers from around the world.

	[http://windowmaker.org/](http://windowmaker.org/) || [windowmaker](https://aur.archlinux.org/packages/windowmaker/)

*   **WM2** — Window manager for X. It provides an unusual style of window decoration and as little functionality as its author feels comfortable with in a window manager. wm2 is not configurable, except by editing the source and recompiling the code, and is really intended for people who do not particularly want their window manager to be too friendly.

	[http://www.all-day-breakfast.com/wm2/](http://www.all-day-breakfast.com/wm2/) || [wm2](https://aur.archlinux.org/packages/wm2/)

*   **[Xfwm](/index.php/Xfwm "Xfwm")** — The [Xfce](/index.php/Xfce "Xfce") window manager manages the placement of application windows on the screen, provides beautiful window decorations, manages workspaces or virtual desktops and natively supports multiscreen mode. It provides its own compositing manager (from the X.Org Composite extension) for true transparency and shadows. The Xfce window manager also includes a keyboard shortcuts editor for user specific commands and basic windows manipulations and provides a preferences dialog for advanced tweaks.

	[http://www.xfce.org/projects/xfwm4/](http://www.xfce.org/projects/xfwm4/) || [xfwm4](https://www.archlinux.org/packages/?name=xfwm4)

### Tiling window managers

*   **[Bspwm](/index.php/Bspwm "Bspwm")** — bspwm is a tiling window manager that represents windows as the leaves of a full binary tree. It has support for EWMH and multiple monitors, and is configured and controlled through messages.

	[https://github.com/baskerville/bspwm](https://github.com/baskerville/bspwm) || [bspwm](https://www.archlinux.org/packages/?name=bspwm)

*   **[Herbstluftwm](/index.php/Herbstluftwm "Herbstluftwm")** — Manual tiling window manager for X11 using Xlib and Glib. The layout is based on splitting frames into subframes which can be split again or can be filled with windows (similar to i3/ musca). Tags (or workspaces or virtual desktops or …) can be added/removed at runtime. Each tag contains its own layout. Exactly one tag is viewed on each monitor. The tags are monitor independent (similar to xmonad). It is configured at runtime via ipc calls from herbstclient. So the configuration file is just a script which is run on startup. (similar to wmii/musca).

	[http://herbstluftwm.org](http://herbstluftwm.org) || [herbstluftwm](https://www.archlinux.org/packages/?name=herbstluftwm)

*   **howm** — A lightweight, tiling X11 window manager that mimics vi by offering operators, motions and modes. Configuration is done through the included `config.h` file.

	[https://github.com/HarveyHunt/howm](https://github.com/HarveyHunt/howm) || [howm-x11](https://aur.archlinux.org/packages/howm-x11/)

*   **[Ion3](/index.php/Ion3 "Ion3")** — Tiling tabbed X11 window manager designed with keyboard users in mind. It was one of the first of the “new wave" of tiling windowing environments (the other being LarsWM, with quite a different approach) and has since spawned an entire category of tiling window managers for X11 – none of which really manage to reproduce the feel and functionality of Ion. It uses Lua as an embedded interpreter which handles all of the configuration.

	[http://tuomov.iki.fi/software](http://tuomov.iki.fi/software) || [ion3](https://aur.archlinux.org/packages/ion3/)

*   **[Notion](/index.php/Notion "Notion")** — Tiling, tabbed window manager for the X window system that utilizes 'tiles' and 'tabbed' windows.
    *   Tiling: you divide the screen into non-overlapping 'tiles'. Every window occupies one tile, and is maximized to it
    *   Tabbing: a tile may contain multiple windows - they will be 'tabbed'.
    *   Static: most tiled window managers are 'dynamic', meaning they automatically resize and move around tiles as windows appear and disappear. Notion, by contrast, does not automatically change the tiling.

	Notion is a fork of Ion3.

	[http://notion.sf.net/](http://notion.sf.net/) || [notion](https://www.archlinux.org/packages/?name=notion)

*   **[Ratpoison](/index.php/Ratpoison "Ratpoison")** — Simple Window Manager with no fat library dependencies, no fancy graphics, no window decorations, and no rodent dependence. It is largely modeled after GNU Screen which has done wonders in the virtual terminal market. Ratpoison is configured with a simple text file. The information bar in Ratpoison is somewhat different, as it shows only when needed. It serves as both an application launcher as well as a notification bar. Ratpoison does not include a system tray.

	[http://www.nongnu.org/ratpoison/](http://www.nongnu.org/ratpoison/) || [ratpoison](https://www.archlinux.org/packages/?name=ratpoison)

*   **[Stumpwm](/index.php/Stumpwm "Stumpwm")** — Tiling, keyboard driven X11 Window Manager written entirely in Common Lisp. Stumpwm attempts to be customizable yet visually minimal. It does have various hooks to attach your personal customizations, and variables to tweak, and can be reconfigured and reloaded while running. There are no window decorations, no icons, no buttons, and no system tray. Its information bar can be set to show constantly or only when needed.

	[http://www.nongnu.org/stumpwm/](http://www.nongnu.org/stumpwm/) || [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/)

*   **[subtle](/index.php/Subtle "Subtle")** — Manual tiling window manager with a rather uncommon approach of tiling: Per default there is no typical layout enforcement, windows are placed on a position (gravity) in a custom grid. The user can change the gravity of each window either directly per grabs or with rules defined by tags in the config. It has workspace tags and automatic client tagging, mouse and keyboard control as well as an extendable statusbar.

	[http://subforge.org/projects/subtle](http://subforge.org/projects/subtle) || [subtle-git](https://aur.archlinux.org/packages/subtle-git/)

*   **[WMFS](/index.php/WMFS "WMFS")** — Window Manager From Scratch is a lightweight and highly configurable tiling window manager for X. It can be configured with a configuration file, supports Xft (FreeType) fonts and is compliant with the Extended Window Manager Hints (EWMH) specifications, Xinerama and Xrandr. WMFS can be driven with Vi based commands (ViWMFS).

	[https://github.com/xorg62/wmfs](https://github.com/xorg62/wmfs) || [wmfs](https://aur.archlinux.org/packages/wmfs/)

*   **[WMFS2](/index.php/WMFS2 "WMFS2")** — Incompatible successor of WMFS. It's even more minimalistic and brings some new stuff.

	[https://github.com/xorg62/wmfs](https://github.com/xorg62/wmfs) || [wmfs2-git](https://aur.archlinux.org/packages/wmfs2-git/)

### Dynamic window managers

*   **[awesome](/index.php/Awesome "Awesome")** — Highly configurable, next generation framework window manager for X. It is very fast, extensible and licensed under the GNU GPLv2 license. Configured in Lua, it has a system tray, information bar, and launcher built in. There are extensions available to it written in Lua. Awesome uses XCB as opposed to Xlib, which may result in a speed increase. Awesome has other features as well, such as an early replacement for notification-daemon, a right-click menu similar to that of the *box window managers, and many other things.

	[http://awesome.naquadah.org/](http://awesome.naquadah.org/) || [awesome](https://www.archlinux.org/packages/?name=awesome)

*   **[catwm](/index.php/Catwm "Catwm")** — Small window manager, even simpler than dwm, written in C. Configuration is done by modifying the config.h file and recompiling.

	[https://github.com/pyknite/catwm](https://github.com/pyknite/catwm) || [catwm-git](https://aur.archlinux.org/packages/catwm-git/)

*   **[dwm](/index.php/Dwm "Dwm")** — Dynamic window manager for X. It manages windows in tiled, monocle and floating layouts. All of the layouts can be applied dynamically, optimising the environment for the application in use and the task performed. does not include a tray app or automatic launcher, although dmenu integrates well with it, as they are from the same author. It has no text configuration file. Configuration is done entirely by modifying the C source code, and it must be recompiled and restarted each time it is changed.

	[http://dwm.suckless.org/](http://dwm.suckless.org/) || [dwm](https://aur.archlinux.org/packages/dwm/)

*   **[echinus](/index.php/Echinus "Echinus")** — Simple and lightweight tiling and floating window manager for X11\. Started as a dwm fork with easier configuration, echinus became full-featured re-parenting window manager with EWMH support. It has an EWMH-compatible panel/taskbar, called [ourico](https://aur.archlinux.org/packages/ourico/).

	[http://plhk.ru](http://plhk.ru) || [echinus](https://aur.archlinux.org/packages/echinus/)

*   **[i3](/index.php/I3 "I3")** — Tiling window manager, completely written from scratch. i3 was created because wmii, our favorite window manager at the time, did not provide some features we wanted (multi-monitor done right, for example), had some bugs, did not progress for quite some time, and was not easy to hack at all (source code comments/documentation completely lacking). Notable differences are in the areas of multi-monitor support and the tree metaphor. For speed the Plan 9 interface of wmii is not implemented.

	[http://i3wm.org/](http://i3wm.org/) || [i3-wm](https://www.archlinux.org/packages/?name=i3-wm)

*   **[FrankenWM](/index.php/FrankenWM "FrankenWM")** — Basically monsterwm with floating done right. Features that are added on top of basic mwm include: more layouts (fibonacci, equal stack, dual stack), gaps (and borders) are adjustable on the fly, minimize/maximize single windows, hide/show all windows, resizing master and stack individually, invert stack.

	[https://github.com/sulami/FrankenWM](https://github.com/sulami/FrankenWM) || [frankenwm-git](https://aur.archlinux.org/packages/frankenwm-git/)

*   **[spectrwm](/index.php/Spectrwm "Spectrwm")** — Small dynamic tiling window manager for X11, largely inspired by xmonad and dwm. It tries to stay out of the way so that valuable screen real estate can be used for much more important stuff. It has sane defaults and is configured with a text file. It was written by hackers for hackers and it strives to be small, compact and fast. It has a built-in status bar fed from a user-defined script.

	[https://github.com/conformal/spectrwm/wiki](https://github.com/conformal/spectrwm/wiki) || [spectrwm](https://www.archlinux.org/packages/?name=spectrwm)

*   **[Qtile](/index.php/Qtile "Qtile")** — Full-featured, hackable tiling window manager written in Python. Qtile is simple, small, and extensible. It's easy to write your own layouts, widgets, and built-in commands.It is written and configured entirely in Python, which means you can leverage the full power and flexibility of the language to make it fit your needs.

	[https://github.com/qtile/qtile](https://github.com/qtile/qtile) || [qtile](https://www.archlinux.org/packages/?name=qtile)

*   **[wmii](/index.php/Wmii "Wmii")** — Small, dynamic window manager for X11\. It is scriptable, has a 9P filesystem interface and supports classic and tiling (Acme-like) window management. It aims to maintain a small and clean (read hackable and beautiful) codebase. The default configuration is in bash and [rc (the Plan 9 shell)](http://rc.cat-v.org), but programs exist written in ruby, and any program that can work with text can configure it. It has a status bar and launcher built in, and also an optional system tray (`witray`).

	[http://wmii.suckless.org/](http://wmii.suckless.org/) || [wmii](https://www.archlinux.org/packages/?name=wmii)

*   **[xmonad](/index.php/Xmonad "Xmonad")** — Dynamically tiling X11 window manager that is written and configured in Haskell. In a normal WM, you spend half your time aligning and searching for windows. Xmonad makes work easier, by automating this. XMonad is configured in Haskell. For all configuration changes, xmonad must be recompiled, so the Haskell compiler (over 100MB) must be installed. A large library called [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) provides many additional features

	[http://xmonad.org/](http://xmonad.org/) || [xmonad](https://www.archlinux.org/packages/?name=xmonad)

## 출처

*   [http://www.gilesorr.com/wm/](http://www.gilesorr.com/wm/)
*   [http://www.slant.co/topics/390/~what-are-the-best-window-managers-for-linux](http://www.slant.co/topics/390/~what-are-the-best-window-managers-for-linux)
*   [https://l3net.wordpress.com/2013/03/17/a-memory-comparison-of-light-linux-desktops/](https://l3net.wordpress.com/2013/03/17/a-memory-comparison-of-light-linux-desktops/)