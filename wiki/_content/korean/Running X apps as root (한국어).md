기본적으로 보안 관계상 루트는 일반 사용자의 X 서버에 접근할 수 없을 것이다. 필요하면 루트가 접근할 수 있는 방법이 여러 가지 있다.

## 가장 안전한 방법

가장 안전한 방법은 다음과 같이 간단하다.

*   kdesu (KDE에 포함되어 있음)

```
$ kdesu *name-of-app*

```

*   gksu (GNOME에 포함되어 있음)

```
$ gksu *name-of-app*

```

*   bashrun (커뮤니티에 있음)

```
$ bashrun --su *name-of-app*

```

*   [sudo](/index.php/Sudo "Sudo") (설치되어 `visudo`로 올바르게 설정되어야 함)

```
$ sudo *name-of-app*

```

*   [sux](/index.php?title=Sux&action=edit&redlink=1 "Sux (page does not exist)") (X 인증을 전송하는 su 래퍼)

```
$ sux root *name-of-app*

```

이러한 방법이 선호된다. 왜냐하면 프로그램이 종료할 때 자동으로 종료하여 어떠한 보안 위험도 완전하게 방지하기 때문이다.

## 기타 방법

기타 방법도 일반 사용자 X 서버에 접근을 허용하지만 다양한 보안 문제가 있고 특히 ssh를 실행할 때 그렇다. 방화벽을 작동한다면 사용 용도에 비해 충분히 안전하다고 볼 수 있다.

*   **일시적으로 루트의 접근을 허용하는 방법**

*   xhost

```
$ xhost +

```

이는 루트를 포함하여 *누구라도* X 서버에 일시적으로 접근하게 한다.

```
$ xhost -

```

이는 이 허용을 해제한다.

다음과 같은 방법을 사용하는 사용자도 있다.

```
$ xhost + localhost

```

(`xhost + localhost`가 작동하려면 TCP 연결을 허용하도록 X 서버를 설정해야 한다.)

*   **영구적으로 루트의 접근을 허용하는 방법**

*   `/etc/profile`에서 시스템 전체 설정

`/etc/profile`에 다음을 추가하라.

```
export XAUTHORITY=/home/non-root-usersname/.Xauthority

```

이렇게 루트가 일반 사용자의 X 서버에 영구적으로 접근할 수 있다.

또는 특정 애플리케이션을 지정하라. 예를 들면 루트가 kwrite에 접근하도록 하기 위한 경우 다음과 같이 설정하라.

```
export XAUTHORITY=/home/usersname/.Xauthority kwrite

```