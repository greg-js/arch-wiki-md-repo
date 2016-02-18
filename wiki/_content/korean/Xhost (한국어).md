## Contents

*   [1 요약](#.EC.9A.94.EC.95.BD)
*   [2 설치](#.EC.84.A4.EC.B9.98)
*   [3 사용법](#.EC.82.AC.EC.9A.A9.EB.B2.95)
*   [4 'cannot connect to X server :0.0'라는 메시지에 대해](#.27cannot_connect_to_X_server_:0.0.27.EB.9D.BC.EB.8A.94_.EB.A9.94.EC.8B.9C.EC.A7.80.EC.97.90_.EB.8C.80.ED.95.B4)

## 요약

출처: Xhost man 문서

xhost는 호스트 이름이나 사용자 이름을 X 서버에 접속이 허용된 목록에 추가하거나 삭제하는 프로그램이다. 호스트의 경우, 개인 정보를 통제하고 보호하는 기본 틀을 제공한다. 최악의 남용을 제한할지라도, 워크스테이션 환경(단독 사용자)에서만 충분할 뿐이다. 더욱 정교한 제어가 필요한 환경에서는 사용자 기반 메커니즘을 구현하거나 X 서버에 다른 인증 자료를 전달하는 프로토콜의 hook을 사용해야 한다.

*man xhost*에서 상세한 내용을 보라.

## 설치

[공식 저장소](/index.php/Official_repositories "Official repositories")에서 [xorg-xhost](https://www.archlinux.org/packages/?name=xorg-xhost)를 [설치](/index.php/Pacman "Pacman")하라.

## 사용법

그래픽 서버(X 스크린 또는 컴퓨터 스크린이라고도 함)에 접근하기 위해서 터미널을 열어서 일반 사용자(*su -* 아님)로 다음을 실행하라.

```
xhost +

```

다시 정상 상태로 되돌아 가서 X 스크린 접근을 제어하려면 다음을 실행하라.

```
xhost -

```

## 'cannot connect to X server :0.0'라는 메시지에 대해

**xhost +** 명령어는 저 메시지를 일시적이나마 사라지게 할 것이다. 영구적으로 이 문제를 해결하는 방법은 많지만 한 가지는 다음과 같이 ~/.bashrc 파일에 추가하는 것이다.

```
xhost + >/dev/null

```

이렇게 하면 터미널을 실행할 때마다 이 명령어가 실행된다. .bashrc 파일이 아직 없다면 생성해서 이 명령어를 삽입하라. *>/dev/null*을 추가하지 않으면 터미널을 실행할 때마다 *access control disabled, clients can connect from any host*라는 메시지를 볼 것이다. 이는 *sudo <자신의 소프트웨어>*를 아무 문제없이 실행할 수 있다는 뜻이다.