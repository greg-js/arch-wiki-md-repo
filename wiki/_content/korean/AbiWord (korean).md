[애비워드](http://www.abisource.com/)는 [LibreOffice](/index.php/LibreOffice "LibreOffice") 라이터와 비슷한 워드프로세서로 다양한 기능을 제공하는 동시에 더 가볍다. 애비워드는 ODF, MS 워드 문서, 워드퍼펙트 문서, RTF, HTML 등 많은 표준 문서 형식을 지원한다.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 설치](#설치)
*   [2 템플릿](#템플릿)
*   [3 단축키 변경](#단축키_변경)
*   [4 LaTeX 폰트](#LaTeX_폰트)
*   [5 GCC 4.6으로 빌드 실패 시](#GCC_4.6으로_빌드_실패_시)
*   [6 바깥 고리](#바깥_고리)

## 설치

[공식 저장소](/index.php/Official_repositories "Official repositories")에서 [abiword](https://www.archlinux.org/packages/?name=abiword) 꾸러미를 설치한다 .

```
# pacman -S abiword

```

맞춤법 검사를 하고자 한다면 사전을 설치할 수 있다. [aspell-en](https://www.archlinux.org/packages/?name=aspell-en) 꾸러미는 영문 맞춤법 검사용 사전이다. 한글용은 아직 없다.

플러그인을 추가하려면 [abiword](https://www.archlinux.org/packages/?name=abiword) 꾸러미를 설치하라.

커서가 작고 글자가 가지런하지 않을 경우 공식 저장소에서 [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)을 설치하거나 [AUR](/index.php/Arch_User_Repository "Arch User Repository")에서 [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)와 공식 저장소에서 [gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts)를 설치하라.

## 템플릿

애비 워드에서 기본 스타일을 변경하려면 새 문서를 열어서 자신의 기호에 맞게 스타일을 수정한 후에 $HOME/.AbiSuite/templates디렉토리에 normal.awt라는 템플릿 이름으로 저장한다.

## 단축키 변경

[이 위키 문서](http://www.abisource.com/wiki/Keyboard_bindings)에서 애비 워드 디폴트 단축키를 변경하는 방법에 대해 보라.

## LaTeX 폰트

[abiword](https://www.archlinux.org/packages/?name=abiword) 꾸러미는 LaTeX 코드를 문서에 삽입할 수 있는 기능을 포함한다. 수식을 제대로 표시하려면 , [latex-xft-fonts](http://movementarian.org/latex-xft-fonts-0.1.tar.gz)를 내려받아서 `/usr/share/fonts` 디렉토리에 저장한다. 그 폰트를 설치하려면 타볼을 풀어서 다음을 실행하라.

```
# fc-cache -fv

```

## GCC 4.6으로 빌드 실패 시

[이 버그](http://bugzilla.abisource.com/show_bug.cgi?id=13066)는 보고되어서 업스트림에서 패치되었지만 아직 (Abiword 2.8.6-4 기준) 아치에서는 이용할 수 없다. 그러므로 이 문제를 겪는다면 직접 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")에 패치를 적용해야 한다.

## 바깥 고리

*   [공식 홈페이지](http://www.abisource.com/)