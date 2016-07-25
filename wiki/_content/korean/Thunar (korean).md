Xfce 프로젝트 [홈페이지](http://docs.xfce.org/xfce/thunar/start) 출처 :

	*Thunar는 Xfce 데스크탑 환경용 최신 파일 관리자이다. Thunar는 빠른 속도와 편리한 사용을 위해 철저하게 설계되었으며 깔끔한 사용자 인터페이스와 쓸모없는 선택사항은 포함하지 않는다. Thunar는 빠른속도와 초기 실행시간, 디렉토리 로딩에서도 좋은 성능을 보여준다.*

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
    *   [1.1 플러그인과 추가기능](#.ED.94.8C.EB.9F.AC.EA.B7.B8.EC.9D.B8.EA.B3.BC_.EC.B6.94.EA.B0.80.EA.B8.B0.EB.8A.A5)
*   [2 Thunar Volume Manager](#Thunar_Volume_Manager)
    *   [2.1 설치](#.EC.84.A4.EC.B9.98_2)
    *   [2.2 설정](#.EC.84.A4.EC.A0.95)
*   [3 유용한 팁](#.EC.9C.A0.EC.9A.A9.ED.95.9C_.ED.8C.81)
    *   [3.1 대용량의 외장 하드디스크 자동으로 마운트](#.EB.8C.80.EC.9A.A9.EB.9F.89.EC.9D.98_.EC.99.B8.EC.9E.A5_.ED.95.98.EB.93.9C.EB.94.94.EC.8A.A4.ED.81.AC_.EC.9E.90.EB.8F.99.EC.9C.BC.EB.A1.9C_.EB.A7.88.EC.9A.B4.ED.8A.B8)
    *   [3.2 원격 위치 탐색](#.EC.9B.90.EA.B2.A9_.EC.9C.84.EC.B9.98_.ED.83.90.EC.83.89)
    *   [3.3 데몬 모드로 실행하기](#.EB.8D.B0.EB.AA.AC_.EB.AA.A8.EB.93.9C.EB.A1.9C_.EC.8B.A4.ED.96.89.ED.95.98.EA.B8.B0)
    *   [3.4 프로그램 로드 시 성능 저하 문제](#.ED.94.84.EB.A1.9C.EA.B7.B8.EB.9E.A8_.EB.A1.9C.EB.93.9C_.EC.8B.9C_.EC.84.B1.EB.8A.A5_.EC.A0.80.ED.95.98_.EB.AC.B8.EC.A0.9C)
    *   [3.5 좌측의 바로가기 항목 변경](#.EC.A2.8C.EC.B8.A1.EC.9D.98_.EB.B0.94.EB.A1.9C.EA.B0.80.EA.B8.B0_.ED.95.AD.EB.AA.A9_.EB.B3.80.EA.B2.BD)
    *   [3.6 키보드 단축키 설정하기](#.ED.82.A4.EB.B3.B4.EB.93.9C_.EB.8B.A8.EC.B6.95.ED.82.A4_.EC.84.A4.EC.A0.95.ED.95.98.EA.B8.B0)
    *   [3.7 fstab에 정의되어 있는 파티션 보이게 하기](#fstab.EC.97.90_.EC.A0.95.EC.9D.98.EB.90.98.EC.96.B4_.EC.9E.88.EB.8A.94_.ED.8C.8C.ED.8B.B0.EC.85.98_.EB.B3.B4.EC.9D.B4.EA.B2.8C_.ED.95.98.EA.B8.B0)
*   [4 사용자 정의 동작](#.EC.82.AC.EC.9A.A9.EC.9E.90_.EC.A0.95.EC.9D.98_.EB.8F.99.EC.9E.91)
    *   [4.1 파일, 디렉토리 검색](#.ED.8C.8C.EC.9D.BC.2C_.EB.94.94.EB.A0.89.ED.86.A0.EB.A6.AC_.EA.B2.80.EC.83.89)
    *   [4.2 바이러스 검색](#.EB.B0.94.EC.9D.B4.EB.9F.AC.EC.8A.A4_.EA.B2.80.EC.83.89)
    *   [4.3 드롭박스 연결](#.EB.93.9C.EB.A1.AD.EB.B0.95.EC.8A.A4_.EC.97.B0.EA.B2.B0)
*   [5 문제 해결](#.EB.AC.B8.EC.A0.9C_.ED.95.B4.EA.B2.B0)
    *   [5.1 Tumblerd 서비스가 멈추고 CPU 사용량이 많아지는 문제](#Tumblerd_.EC.84.9C.EB.B9.84.EC.8A.A4.EA.B0.80_.EB.A9.88.EC.B6.94.EA.B3.A0_CPU_.EC.82.AC.EC.9A.A9.EB.9F.89.EC.9D.B4_.EB.A7.8E.EC.95.84.EC.A7.80.EB.8A.94_.EB.AC.B8.EC.A0.9C)
    *   [5.2 수시로 Trash/network 아이콘이 사라지는 문제](#.EC.88.98.EC.8B.9C.EB.A1.9C_Trash.2Fnetwork_.EC.95.84.EC.9D.B4.EC.BD.98.EC.9D.B4_.EC.82.AC.EB.9D.BC.EC.A7.80.EB.8A.94_.EB.AC.B8.EC.A0.9C)
    *   [5.3 Not authenticated to mount filesystems](#Not_authenticated_to_mount_filesystems)
*   [6 출처](#.EC.B6.9C.EC.B2.98)

## 설치

[thunar](https://www.archlinux.org/packages/?name=thunar) 패키지를 [설치](/index.php/Install "Install")한다. [thunar](https://www.archlinux.org/packages/?name=thunar)는 [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/) 패키지 그룹의 하나이기 때문에 [Xfce](/index.php/Xfce "Xfce")를 사용 중이라면 이미 시스템에 설치되어 있을 것이다.

### 플러그인과 추가기능

*   **Thunar Archive Plugin** — 컨텍스트 메뉴 아이템을 이용하여 파일압축 및 압축해제를 제공하는 플러그인이다. File Roller([file-roller](https://www.archlinux.org/packages/?name=file-roller))나 Ark([ark](https://www.archlinux.org/packages/?name=ark)), Xarchiver([xarchiver](https://www.archlinux.org/packages/?name=xarchiver)) 등의 타 압축프로그램들의 프론트엔드로서 자체적으로 압축관련기능을 제공하지 않는다. 해당 플러그인은 [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) 패키지 그룹에 속해 있다.

	[http://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin) || [thunar-archive-plugin](https://www.archlinux.org/packages/?name=thunar-archive-plugin)

*   **Thunar Media Tags Plugin** — 미디어 파일에 대한 자세한 정보를 제공한다. Bulk rename 기능(한번에 다수의 파일 이름을 변경하는 기능: [xfce 문서](http://docs.xfce.org/xfce/thunar/bulk-renamer/start) 참조)과 미디어 태그 편집 기능을 제공하며 ID3(MP3 파일 포맷 시스템)와 Ogg/Vorbis 태그를 제공한다. [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) 패키지 그룹에 속해 있다.

	[http://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin) || [thunar-media-tags-plugin](https://www.archlinux.org/packages/?name=thunar-media-tags-plugin)

*   **Thunar Shares Plugin** — 루트의 접근권한 요청 없이 사용자가 Samba를 사용하는 디렉토리를 빠르게 공유할 수 있도록 해준다. Samba 설정 관련은 다음 문서ᅟ를 참고한다: [how to configure directions](/index.php/Samba#Creating_usershare_path "Samba").

	[http://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin) || [thunar-shares-plugin](https://aur.archlinux.org/packages/thunar-shares-plugin/)

*   **[Thunar Volume Manager](#Thunar_Volume_Manager)** — Thunar에서 이동식 장치을 자동으로 관리하며 [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/) 패키지 그룹에 속해 있다.

	[http://goodies.xfce.org/projects/thunar-plugins/thunar-volman](http://goodies.xfce.org/projects/thunar-plugins/thunar-volman) || [thunar-volman](https://www.archlinux.org/packages/?name=thunar-volman)

*   **Tumbler** — 파일 썸네일을 생성하기 위한 외부 프로그램. 비디오 파일의 썸네일은 [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer)를 설치해야 한다.

	[http://git.xfce.org/xfce/tumbler/tree/README](http://git.xfce.org/xfce/tumbler/tree/README) || [tumbler](https://www.archlinux.org/packages/?name=tumbler)

*   **RAW Thumbnailer** — RAW 이미지 파일의 썸네일을 지원하고 저용량이며 빠르다.

	[https://code.google.com/p/raw-thumbnailer/](https://code.google.com/p/raw-thumbnailer/) || [raw-thumbnailer](https://www.archlinux.org/packages/?name=raw-thumbnailer)

*   **libgsf** — odf 포맷과 같이 구조화 파일 포맷을 읽고 쓰기 위해 필요한 유틸리티 라이브러리. odf 썸네일을 원할 때에 본 라이브러리를 설치해야 한다.

	[http://directory.fsf.org/wiki/Libgsf](http://directory.fsf.org/wiki/Libgsf) || [libgsf](https://www.archlinux.org/packages/?name=libgsf)

**Tip:** Thunar에서 `mtp` 또는 `smb` 서비스에 접근하는 추가적인 기능은 [GVFS](/index.php/GVFS "GVFS")를 참고한다. [File manager functionality](/index.php/File_manager_functionality "File manager functionality")에서도 자세한 정보를 확인할 수 있다.

## Thunar Volume Manager

Thunar에서 이동식 장치들에 대한 자동 마운트/마운트해제를 지원할 수 있지만 마운트/마운트해제 시 자동 명령어 실행과 마운트된 장치의 위치에서 새로운 창 열기 등의 확장기능들은 Thunar Volume Manager가 필요하다.

### 설치

Thunar Volume Manager는 공식 저장소에서 [thunar-volman](https://www.archlinux.org/packages/?name=thunar-volman)로 설치할 수 있다.

**Tip:** Thunar에서 자동 마운트 처리를 위해 반드시 인스턴스 하나는 데몬 모드로 실행되어야 한다. [#Starting in daemon mode](#Starting_in_daemon_mode)

### 설정

카메라나 오디오 플레이어가 연결되었을 때 특정 동작이 실행되도록 설정할 수 있다. 플러그인 설치 후에:

1.  Thunar를 실행하여 *Edit > Preferences*로 들어간다.
2.  'Advanced' 탭에서 'Enable Volume Management'를 체크한다.
3.  'Configure'를 클릭한 후에 아래의 항목들을 체크한다.
    *   Mount removable drives when hot-plugged.
    *   Mount removable media when inserted.
4.  원한다면 추가적인 변경을 한다. (아래 참고)

다음은 Amarok 미디어 플레이어가 오디오 CD를 재생하도록 하는 예제이다.

```
 Multimedia - Audio CDs: `amarok --cdplay %d`

```

## 유용한 팁

### 대용량의 외장 하드디스크 자동으로 마운트

만약 tunar-volman과 gvfs가 설치되어 있는 환경에도 불구하고 크기가 1TB가 넘는 대용량의 휴대용 장치의 마운트에 실패했다면 [udevil](https://www.archlinux.org/packages/?name=udevil)나 [udiskie](https://www.archlinux.org/packages/?name=udiskie)와 같은 다른 마운트 프로그램을 시도해본다. *udiskie*는 udisks2를 사용하여 gvfs와 호환되므로 권장된다. udisks2 지원을 활성화하면서 udiskie를 실행하려면 autostart 파일에 아래 라인을 추가한다.

```
udiskie -2 &

```

### 원격 위치 탐색

Xfce 4.8 (Thunar 1.2) 이후 FTP 서버나 Samba 공유서버와 같은 원격 위치에서도 탐색이 가능하다. 원격 위치 탐색 기능을 활성화하기 위해서는 반드시 [gvfs](https://www.archlinux.org/packages/?name=gvfs)와 [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb), [sshfs](https://www.archlinux.org/packages/?name=sshfs)가 설치되어 있어야 한다. 'Network' 항목이 Thunar의 측면 영역에 보이고 Thunar 주소창(단축키 `Ctrl+l`)에 'smb://,ftp://, ssh://, sftp://, davs:// + 호스트이름 또는 IP 주소'와 같은 URI 스키마를 사용하여 원격 위치를 열 수 있다.

[NFS](/index.php/NFS "NFS")(네트워크 파일시스템 공유)를 위한 URI스키마는 없으나 [fstab](/index.php/Fstab "Fstab")을 올바르게 설정했다면 `mount` 명령어를 사용할 수 있다.

 `/etc/fstab` 
```
# nas1 server
nas1:/c/home		/media/nas1/home	nfs	noauto,user,_netdev,bg  0 0
```

여기서 중요한 부분은 옵션 부분이다. `noauto` 옵션은 사용자가 Thunar에서 직접 클릭하기 전까지 마운트되는 것을 방지한다. `user` 옵션은 모든 사용자에게 공유폴더에 대한 마운트, 마운트해제를 허용하고 `_netdev` 옵션은 네트워크 연결이 필수 조건이라는 것을 명시한다. 마지막으로 `bg` 옵션은 마운트 동작을 백그라운드에서 수행하게 한다. 서버의 스핀업 타임으로 타임아웃이 돼서 마운트하기 위해 사용자가 다시 클릭해야하는 경우가 생기는데, 마운트 동작을 백그라운드에서 수행하게 함으로써 이를 방지한다.

**Tip:** 원격 파일시스템 위치에 대한 보안키를 영구적으로 저장하려면 [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")을 설치한다.

### 데몬 모드로 실행하기

Thunar는 데몬 모드로 실행할 수 있다. 데몬 모드로 실행하면 초기 실행이 더 빨라지고 백그라운드에서 동작하는 인스턴스와 필요시에 열리는 윈도우 관련 인스턴스(예. 플래시 드라이브 삽입 시에 열리는 thunar 창) 등 필요한 인스턴스만 사용하게 되며 이동식 디스크에 대한 마운트 동작을 Thunar에서 자동으로 처리하도록 하는 장점이 있다.

로그인 시 `thunar --daemon` 명령어가 자동으로 실행되도록 한다.자세한 것은 [Xfce](/index.php/Xfce "Xfce")와 [Autostarting](/index.php/Autostarting "Autostarting")을 참고한다.

### 프로그램 로드 시 성능 저하 문제

몇몇 유저들은 Thunar 최초 실행 시에 프로그램이 시작되기까지의 시간이 너무 오래 소요되는 문제를 겪는다. 이러한 문제는 네트워크를 확인하는 gvfs가 원인으로서 gvfs가 수행중인 동작을 마칠 때까지 Thunar가 시작되지 못하도록 하기 때문이다. 이러한 문제를 해결하기 위해서는 `/usr/share/gvfs/mounts/network.mount`에서 **AutoMount=true** 부분을 **AutoMount=false**로 변경한다.

### 좌측의 바로가기 항목 변경

좌측의 바로가기 영역에 숨겨진 메뉴가 있다.

DEVICES, PLACES라고 표시된 카테고리 레이블에 대고 오른쪽 마우스를 클릭하면 표시할 아이템을 선택할 수 있는 팝업 메뉴가 나타난다.

### 키보드 단축키 설정하기

[GTK+#Keyboard shortcuts](/index.php/GTK%2B#Keyboard_shortcuts "GTK+") 참고.

### fstab에 정의되어 있는 파티션 보이게 하기

Thunar는 루트 파티션 외에 `/etc/fstab`에 정의된 파티션들은 기본적으로 보여주지 않는다.

이 때, fstab에 **comment=x-gvfs-show** 옵션을 추가하면 사용자가 원하는 파티션을 보이도록 설정할 수 있다.

## 사용자 정의 동작

본 절은 사용자 정의 동작 설정을 설명하고 `Edit -> Configure custom actions`에서 설정이 가능하다. 설정한 내용은 `~/.config/Thunar/uca.xml` 파일에 저장된다. 관련 예제는 [thunar wiki](http://docs.xfce.org/xfce/thunar/custom-actions)에 많이 정리되어 있으니 참고하기 바란다. [this](http://duncanlock.net/blog/2013/06/28/useful-thunar-custom-actions/) 블로그에도 관련된 다양한 콜렉션들을 제공한다.

### 파일, 디렉토리 검색

검색기능을 사용하기 위해서는 [catfish](https://www.archlinux.org/packages/?name=catfish)가 설치되어야 한다. 선택 의존 패키지 [mlocate](https://www.archlinux.org/packages/?name=mlocate)도 반드시 설치한다.

| Name | Command | File patterns | Appears if selection contains |
| Search | `catfish --path=%f` | * | Directories |

### 바이러스 검색

바이러스 검색 기능을 위해서는 [clamav](https://www.archlinux.org/packages/?name=clamav), [clamtk](https://aur.archlinux.org/packages/clamtk/)을 설치한다.

| Name | Command | File patterns | Appears if selection contains |
| Scan for virus | `clamtk %F` | * | Select all |

### 드롭박스 연결

| Name | Command | File patterns | Appears if selection contains |
| Link to Dropbox | `ln -s %f /path/to/DropboxFolder` | * | Directories, other files |

파일과 폴더를 특정 위치로 사용자 정의 동작을 이용하여 심볼릭 링크를 만드려고 하는 경우가 있다. 하지만 해당 동작들이 많아지는 경우, 메뉴 자체에 항목이 엄청나게 늘어날 수 있는데 이러한 경우 `Send To` 폴더를 이용하는 편이 유용하다. `~/.local/share/Thunar/sendto` 폴더 내에 .desktop 파일을 만들고 수행하고자 하는 사용자 정의 동작을 파일에 정의한다. 만약에 Dropbox 폴더에 심볼릭 링크를 만들고자 한다면 다음과 같은 내용으로 dropbox_folder.desktop 파일을 생성하여 SendTo 메뉴에 새로운 항목을 추가할 수 있다. 이 때, 설정 적용을 위해 반드시 Thunar를 재시작해야 한다.

```
[Desktop Entry]
Type=Application
Version=1.0
Encoding=UTF-8
Exec=ln -s %f /path/to/DropboxFolder
Icon=/usr/share/icons/dropbox.png
Name=Dropbox

```

## 문제 해결

### Tumblerd 서비스가 멈추고 CPU 사용량이 많아지는 문제

파일시스템 감시와 시스템 알림 서비스 Tumblerd는 썸네일이 필요할 때 무한루프에 빠져 시스템의 프로세서를 100프로 사용하게 되는 버그가 있다. ([bug report](https://bugzilla.xfce.org/show_bug.cgi?id=7384)). 아래의 코드는 임시 해결방법으로 무한루프를 실행하는 것을 멈추는 스크립트이다. 홈 디렉토리에 *.sh*파일로 저장 후 실행권한을 추가한 뒤 시스템 시작 시에 스크립트가 실행되도록 설정한다.

```
#!/bin/bash
period=20
tumblerpath="/usr/lib/*/tumbler-1/tumblerd" # The * here should find the right one, whether 32 and 64-bit
cpu_threshold=50
mem_threshold=20
max_strikes=2                               # max number of above cpu/mem-threshold's in a row
log="/tmp/tumblerd-watcher.log"

if [[ -n "${log}" ]]; then
    cat /dev/null > "${log}"
    exec >"${log}" 2>&1
fi

strikes=0
while sleep "${period}"; do
    while read pid; do
	cpu_usage=$(ps --no-headers -o pcpu -f "${pid}"|cut -f1 -d.)
	mem_usage=$(ps --no-headers -o pmem -f "${pid}"|cut -f1 -d.)

	if [[ $cpu_usage -gt $cpu_threshold ]] || [[ $mem_usage -gt $mem_threshold ]]; then
	    echo "$(date +"%F %T") PID: $pid CPU: $cpu_usage/$cpu_threshold %cpu MEM: $mem_usage/$mem_threshold STRIKES: ${strikes} NPROCS: $(pgrep -c -f ${tumblerpath})"
	    (( strikes++ ))
	    if [[ ${strikes} -ge ${max_strikes} ]]; then
		kill "${pid}"
		echo "$(date +"%F %T") PID: $pid KILLED; NPROCS: $(pgrep -c -f ${tumblerpath})"
		strikes=0
	    fi
	else
	    strikes=0
	fi
    done < <(pgrep -f ${tumblerpath})
done

```

### 수시로 Trash/network 아이콘이 사라지는 문제

Thunar 인스턴스가 *gvfs*이후에 실행되도록 한다. [[1]](https://bugs.launchpad.net/ubuntu/+source/thunar/+bug/1057610) `thunar --daemon`를 사용하는 경우에는 GVFS가 활성화될 때까지 기다리는 wrapper를 생성할 수 있다. (아래 코드 참고)

**Note:** 반드시 `$PATH`에서 `/usr/local/bin`가 `/usr/bin`이전에 위치해야 한다.
 `/usr/local/bin/Thunar` 
```
#!/bin/bash
if [[ $1 == --daemon ]]; then
  until pgrep gvfs >/dev/null; do
    sleep 1
  done
  exec /usr/bin/Thunar "$@"
else
  exec /usr/bin/Thunar "$@"
fi

```

### Not authenticated to mount filesystems

[File manager functionality#Troubleshooting](/index.php/File_manager_functionality#Troubleshooting "File manager functionality") 참고.

## 출처

*   [Thunar](http://docs.xfce.org/xfce/thunar/start) project page
*   [Thunar Volume Manager](http://goodies.xfce.org/projects/thunar-plugins/thunar-volman) project page
*   This [list](http://goodies.xfce.org/projects/thunar-plugins/start) of plugins