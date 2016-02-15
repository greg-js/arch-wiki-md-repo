[D-Bus](https://en.wikipedia.org/wiki/D-Bus "wikipedia:D-Bus")는 메시지 버스 시스템으로 프로세스 간의 통신을 쉽게하는 수단을 제공한다. 시스템 전반과 각 사용자 세션 모두에 대해 실행될 수 있는 데몬과 응용프로그램이 D-Bus를 사용할 수 있게 하는 일련의 라이브러리로 이루어져 있다.

## 설치

D-Bus는 [systemd](/index.php/Systemd "Systemd")를 사용하면 자동으로 활성화된다. systemd가 [dbus](https://www.archlinux.org/packages/?name=dbus)에 의존하기 때문이다.

## 사용자 세션 시작하기

[gnome-session](/index.php/GNOME "GNOME"), [startkde](/index.php/KDE "KDE"), [startxfce4](/index.php/Xfce "Xfce")는 D-Bus 세션이 이미 실행하고 있지 않으면 자동으로 시작할 것이다. `~/.xinitrc`의 참조 파일인 `/etc/skel/.xinitrc` 역시 똑같은 역할을 할 것이다. `~/.[xinitrc](/index.php/Xinitrc "Xinitrc")` 파일이 참조 파일인 `/etc/skel/.xinitrc`에 기반을 둔 것임을 확인하라.

## 같이 보기

*   [freedesktop.org의 D-Bus 문서](http://www.freedesktop.org/wiki/Software/dbus)
*   [freedesktop.org의 D-Bus 소개](http://www.freedesktop.org/wiki/IntroductionToDBus)