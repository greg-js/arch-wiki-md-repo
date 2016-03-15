**마테 데스크톱 환경**은 그놈 2에서 갈라져 나왔으며 전통적인 사용자 인터페이스를 이용해 직관적이고 매력적인 데스크톱 환경을 제공한다. 마테는 활발하게 개발되고 있다.

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
    *   [1.1 개발 버전](#.EA.B0.9C.EB.B0.9C_.EB.B2.84.EC.A0.84)
*   [2 시작하기](#.EC.8B.9C.EC.9E.91.ED.95.98.EA.B8.B0)
    *   [2.1 수동 시작](#.EC.88.98.EB.8F.99_.EC.8B.9C.EC.9E.91)
    *   [2.2 부팅 시에 자동 시작](#.EB.B6.80.ED.8C.85_.EC.8B.9C.EC.97.90_.EC.9E.90.EB.8F.99_.EC.8B.9C.EC.9E.91)
        *   [2.2.1 GDM (구 버전)](#GDM_.28.EA.B5.AC_.EB.B2.84.EC.A0.84.29)
        *   [2.2.2 LightDM, GDM & LXDM](#LightDM.2C_GDM_.26_LXDM)
        *   [2.2.3 MDM(마테 디스플레이 관리자)](#MDM.28.EB.A7.88.ED.85.8C_.EB.94.94.EC.8A.A4.ED.94.8C.EB.A0.88.EC.9D.B4_.EA.B4.80.EB.A6.AC.EC.9E.90.29)
        *   [2.2.4 KDM](#KDM)
        *   [2.2.5 SLiM](#SLiM)
*   [3 응용프로그램](#.EC.9D.91.EC.9A.A9.ED.94.84.EB.A1.9C.EA.B7.B8.EB.9E.A8)
*   [4 알려진 문제점](#.EC.95.8C.EB.A0.A4.EC.A7.84_.EB.AC.B8.EC.A0.9C.EC.A0.90)
    *   [4.1 Qt 프로그램 스타일 미적용](#Qt_.ED.94.84.EB.A1.9C.EA.B7.B8.EB.9E.A8_.EC.8A.A4.ED.83.80.EC.9D.BC_.EB.AF.B8.EC.A0.81.EC.9A.A9)
    *   [4.2 Evolution 이메일 미작동](#Evolution_.EC.9D.B4.EB.A9.94.EC.9D.BC_.EB.AF.B8.EC.9E.91.EB.8F.99)
    *   [4.3 GTK3 프로그램 스타일 적용](#GTK3_.ED.94.84.EB.A1.9C.EA.B7.B8.EB.9E.A8_.EC.8A.A4.ED.83.80.EC.9D.BC_.EC.A0.81.EC.9A.A9)
*   [5 문제 해결](#.EB.AC.B8.EC.A0.9C_.ED.95.B4.EA.B2.B0)
    *   [5.1 사용자 전환하기](#.EC.82.AC.EC.9A.A9.EC.9E.90_.EC.A0.84.ED.99.98.ED.95.98.EA.B8.B0)
        *   [5.1.1 LightDM](#LightDM)
        *   [5.1.2 GDM](#GDM)
*   [6 같이 보기](#.EA.B0.99.EC.9D.B4_.EB.B3.B4.EA.B8.B0)

## 설치

마테(MATE)는 [공식 저장소](/index.php/Official_repositories "Official repositories")에서 설치할 수 있다.

*   [mate-panel](https://www.archlinux.org/packages/?name=mate-panel) 꾸러미는 최소한의 데스크톱 셀을 제공한다.
*   [mate](https://www.archlinux.org/groups/x86_64/mate/) 그룹은 표준 마테 환경에 필요한 핵심 요소를 포함한다.gexperience.
*   [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) 그룹은 마테 데스크톱과 어울리는 유틸리티와 응용프르그램을 포함한다. [mate-extra](https://www.archlinux.org/groups/x86_64/mate-extra/) 그룹만 설치한다면 의존성에 의해 {Grp|mate}} 그룹의 일부만 설치되기 때문에 모든 마테 꾸러미를 설치하려면 두 그룹을 명시적으로 설치해야 한다.
*   [mate-netbook](https://www.archlinux.org/packages/?name=mate-netbook) 꾸러미는 넷북과 같은 스크린이 작은 장치 소유자에게 유용한 마테 패널 애플릿을 제공한다. 이 애플릿은 모든 창을 자동적으로 최소화하고 프로그램을 전환할 수 있는 애플릿을 제공한다. 이 애플릿은 **mate**나 **mate-extra** 그룹에 포함되어 있지 않지만 원하면 별도로 설치할 수 있다.

### 개발 버전

마테 개발 버전을 설치해 시험해 보려면 다음을 pacman.conf에 추가한 후에 `pacman -Syu`를 실행하라. 2014년 2월 기준, 개발 버전은 1.7.5이다.

```
[mate-unstable]
SigLevel = Optional TrustAll
Server = [http://dev.mate-desktop.org/archlinux/$arch](http://dev.mate-desktop.org/archlinux/$arch)

```

## 시작하기

### 수동 시작

자신의 `[~/.xinitrc](/index.php/Xinitrc "Xinitrc")` 파일에 다음을 추가하라.

```
exec mate-session

```

그리고 다음을 실행하라.

```
$ startx

```

**참고:** logind 세션 보존과 같은 상세한 사항은 [xinitrc](/index.php/Xinitrc "Xinitrc")를 참고하라.

### 부팅 시에 자동 시작

[Display manager](/index.php/Display_manager "Display manager")와 [Start X at Boot](/index.php/Start_X_at_Boot "Start X at Boot")에서 더 자세한 내용을 보라.

#### GDM (구 버전)

AUR에 있는 [gdm-old](https://aur.archlinux.org/packages/gdm-old/)를 사용한다면 세션 목록에서 마테(MATE) 세션을 선택하라. 마테를 최초로 실행할 때 선택 항목이 제시되면 "이번 세션만"을 꼭 선택하라.

#### [LightDM](/index.php/LightDM "LightDM"), [GDM](/index.php/GDM "GDM") & [LXDM](/index.php/LXDM "LXDM")

세션 목록에서 마테(MATE) 세션을 선택하라. 잘 작동한다.

#### MDM(마테 디스플레이 관리자)

MDM은 그놈 디스플레이 관리자에 대응하는 마테 데스크톱 디스플레이 관리자이다. 그 꾸러미인 'mate-display-manager'는 **mate-extra**그룹이나 AUR의 [mate-display-manager](https://aur.archlinux.org/packages/mate-display-manager/)에 있다. GDM처럼 작동한다. 하지만 불행하게도 그 프로젝트가 변화를 겪고 있고 MDM은 2012/07/01 기준으로 이용할 수 없다.

#### [KDM](/index.php/KDM "KDM")

[KDM](/index.php/KDM "KDM")을 사용하려면 그 환경 설정 파일을 수정하라. root 권한으로 `/usr/share/config/kdm/kdmrc` 환경 설정 파일을 편집해 **SessionsDir** 매개 변수를 찾아 `/usr/share/xsessions`을 다음과 같이 추가하라.

```
SessionsDirs=/usr/share/config/kdm/sessions,/usr/share/apps/kdm/sessions,/usr/share/xsessions

```

KDM을 재시작하여 "MATE 세션"을 목록에서 선택하라.

#### [SLiM](/index.php/SLiM "SLiM")

[SLiM](/index.php/SLiM "SLiM")에 따라서 그 사용법을 숙지하고 .xinitrc 파일에 다음을 추가하라.

```
exec mate-session

```

## 응용프로그램

그놈 핵심 프로그램이 라이선스에 따라서 마테용으로 재명명되었음을 명심하라. GNOME -> MATE 프로그램 대응 관계는 다음과 같다.

*   Nautilus는 **caja**로 재명명되었다.
*   Metacity는 **marco**로 재명명되었다.
*   Gconf는 **mate-conf** 로 재명명되었다.
*   Gedit는 **Pluma**로 재명명되었다.
*   Eye of GNOME는 **Eye of MATE**로 재명명되었다.
*   Evince는 **Atril**로 재명명되었다.
*   File Roller는 **Engrampa**로 재명명되었다.
*   GNOME Terminal은 **MATE Terminal**로 재명명되었다.

그놈 패널, 그놈 메뉴와 같이 그놈이 앞에 붙은 기타 프로그램 및 핵심 구성요소는 단순하게 "MATE"를 앞에 붙여서 마테 패널, 마테 메뉴가 되었다.

GTK2용으로 만든 모든 그놈 기타 프로그램이 마테로 갈라진 것은 아니다. 다음 프로그램은 마테에서 그대로 사용한다.

*   Totem (mate-video-player)
*   GNOME Panel applets (mate-applets)

NetworkManager를 사용해 인터넷에 연결한다면 GTK2 nm-applet인 [network-manager-applet-gtk2](https://aur.archlinux.org/packages/network-manager-applet-gtk2/)를 설치할 수 있다. 설치 시에 gnome-bluetooth보다는 mate-bluetooth에 의존하도록 PKGBUILD를 수정할 필요가 있을 것이다.

## 알려진 문제점

### Qt 프로그램 스타일 미적용

Qt4 프로그램은 GTK2 테마가 적용되지 않을 수 있을 것이다. 이 문제는 qtconfig를 실행해 GUI Style을 GTK+로 설정하면 해결될 것이다.

### Evolution 이메일 미작동

[Evolution#Using_Evolution_Outside_Of_Gnome](/index.php/Evolution#Using_Evolution_Outside_Of_Gnome "Evolution")을 보라.

### GTK3 프로그램 스타일 적용

[Rhythmbox](/index.php/Rhythmbox "Rhythmbox")와 같은 프로그램에 스타일 적용이 안 된다면 [Clearlooks Phenix](https://aur.archlinux.org/packages/clearlooks-phenix-gtk-theme-git/) 테마를 사용해 보라.

## 문제 해결

### 사용자 전환하기

MDM (Mate Display Manager)을 사용하지 않으면 사용자 전환을 할 수 없다. 사용하려면 다음과 같이 심볼릭 링크를 만들어라.

#### [LightDM](/index.php/LightDM "LightDM")

```
# ln -s /usr/lib/lightdm/lightdm/gdmflexiserver /usr/bin/mdmflexiserver

```

#### [GDM](/index.php/GDM "GDM")

```
# ln -s /usr/bin/gdmflexiserver /usr/bin/mdmflexiserver

```

## 같이 보기

[마테 공식 홈페이지](http://mate-desktop.org)

**아치 리눅스 포럼**

*   [*마테 데스크톱 환경 일반*](https://bbs.archlinux.org/viewtopic.php?pid=1018647) - 마테에 관한 전반적인 토론
*   [*마테 데스크톱 스크린샷*](https://bbs.archlinux.org/viewtopic.php?id=139877)