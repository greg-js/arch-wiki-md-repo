로캘은 리눅스에서 사용자가 어떤 언어를 사용하는지 지정하는 데 사용된다. 로캘은 사용될 문자 집합을 같이 지정하기 때문에 로캘을 바르게 설정하는 것이 특히 언어에 비아스키 문자가 있을 경우에 매우 중요하다.

로캘은 다음과 같은 형식으로 지정된다.

```
<언어>_<지역>.<코드집합>[@<변형>]

```

## Contents

*   [1 필요한 로캘 활성화](#.ED.95.84.EC.9A.94.ED.95.9C_.EB.A1.9C.EC.BA.98_.ED.99.9C.EC.84.B1.ED.99.94)
    *   [1.1 한국어 예시](#.ED.95.9C.EA.B5.AD.EC.96.B4_.EC.98.88.EC.8B.9C)
*   [2 시스템 로캘 설정](#.EC.8B.9C.EC.8A.A4.ED.85.9C_.EB.A1.9C.EC.BA.98_.EC.84.A4.EC.A0.95)
*   [3 안전 로캘 설정](#.EC.95.88.EC.A0.84_.EB.A1.9C.EC.BA.98_.EC.84.A4.EC.A0.95)
*   [4 개인 사용자 로캘 설정](#.EA.B0.9C.EC.9D.B8_.EC.82.AC.EC.9A.A9.EC.9E.90_.EB.A1.9C.EC.BA.98_.EC.84.A4.EC.A0.95)
*   [5 정렬 순서 설정](#.EC.A0.95.EB.A0.AC_.EC.88.9C.EC.84.9C_.EC.84.A4.EC.A0.95)
*   [6 주일의 첫 번째 요일 설정](#.EC.A3.BC.EC.9D.BC.EC.9D.98_.EC.B2.AB_.EB.B2.88.EC.A7.B8_.EC.9A.94.EC.9D.BC_.EC.84.A4.EC.A0.95)
*   [7 문제 해결](#.EB.AC.B8.EC.A0.9C_.ED.95.B4.EA.B2.B0)
    *   [7.1 터미널에서 UTF-8을 지원하지 못할 경우](#.ED.84.B0.EB.AF.B8.EB.84.90.EC.97.90.EC.84.9C_UTF-8.EC.9D.84_.EC.A7.80.EC.9B.90.ED.95.98.EC.A7.80_.EB.AA.BB.ED.95.A0_.EA.B2.BD.EC.9A.B0)
        *   [7.1.1 Xterm에서 UTF-8을 지원하지 못할 경우](#Xterm.EC.97.90.EC.84.9C_UTF-8.EC.9D.84_.EC.A7.80.EC.9B.90.ED.95.98.EC.A7.80_.EB.AA.BB.ED.95.A0_.EA.B2.BD.EC.9A.B0)
        *   [7.1.2 Gnome-터미널과 rxvt-unicode 터미널에서 UTF-8을 지원하지 못할 경우](#Gnome-.ED.84.B0.EB.AF.B8.EB.84.90.EA.B3.BC_rxvt-unicode_.ED.84.B0.EB.AF.B8.EB.84.90.EC.97.90.EC.84.9C_UTF-8.EC.9D.84_.EC.A7.80.EC.9B.90.ED.95.98.EC.A7.80_.EB.AA.BB.ED.95.A0_.EA.B2.BD.EC.9A.B0)
*   [8 같이 보기](#.EA.B0.99.EC.9D.B4_.EB.B3.B4.EA.B8.B0)

## 필요한 로캘 활성화

로캘을 시스템에서 사용하려면 먼저 활성화해야 한다. 모든 이용 가능한 로캘을 보려면 다음 명령어를 사용하라.

```
$ locale -a

```

로캘을 활성화하려면 `/etc/locale.gen` 파일에서 그 로캘 앞의 주석 표시를 제거하라. 이 파일은 시스템에서 사용 가능한 로캘 전부를 포함한다. 로캘을 비활성화하려면 그 로캘을 주석 처리하라. 필요한 로캘을 지정한 후에 시스템을 다음 명령어로 갱신해야 한다.

```
# locale-gen

```

지금 사용하고 있는 로캘을 표시하려면 다음을 입력해 보라.

```
$ locale

```

**도움말:** 단지 하나의 언어가 시스템에서 대부분 사용될지라도 다른 로캘을 활성화하는 게 도움이 되거나 심지어 필요할 수 있다. en_US를 사용하지 않는 사용자가 있는 다중 사용자 시스템이라면 그 각자의 로캘이 시스템에서 지원되어야 한다.

### 한국어 예시

`/etc/locale.gen`에서 다음을 지정하라.

```
ko_KR.UTF-8 UTF-8

```

루트 권한으로 다음과 같이 시스템을 갱신하라.

```
# locale-gen

```

## 시스템 로캘 설정

시스템 로캘을 지정하려면 `locale.conf` 파일에 `LANG`을 설정하라.

`locale.conf`는 행 바꿈으로 구분되는 환경 변수 할당값을 포함한다. `LANG` 외에도, `LC_ALL`을 제외하고 모든 `LC_*` 변수를 지원한다.

**참고:** `/etc/locale.conf`는 기본적으로 생성되지 않기 때문에 수동으로 만들어야 한다.

**도움말:** 아치를 설치하는 과정에서 `locale`의 출력이 자신의 기호에 맞다면 가상 루트에 있는 동안 `# locale > /etc/locale.conf`를 실행해 설정 시간을 줄일 수 있다.
 `/etc/locale.conf`  `LANG="ko_KR.UTF-8"` 

고급 설정 예시:

 `/etc/locale.conf` 
```
# 한국어 UTF-8 설정
LANG="ko_KR.UTF-8"

# 기본 정렬 방식 유지하도록 설정('.' 파일이 디렉토리 목록의 처음에 표시됨)
LC_COLLATE="C"

#  YYYY년 MM월 DD일 (토) 오후 HH시 MM분 SS초 ("date +%c" 명령어로 시험) 형식으로 날짜 표시하기
LC_TIME="ko_KR.UTF-8"
```

`localectl`을 사용해 `locale.conf`에 기본 로캘을 설정할 수도 있다.

1.  localectl set-locale LANG="ko_KR.utf8"

더 자세한 사항은 `man 1 localectl`과 `man 5 locale.conf`를 참고하라.

로캘은 시스템을 재부팅해야 적용되며 로그인하면 각 세션별로 설정될 것이다.

## 안전 로캘 설정

gettext를 사용해 번역하는 프로그램은 일반 변수 외에 `LANGUAGE` 변수를 사용한다. 이 변수는 다음 순서로 사용될 로캘 변수 [목록](http://www.gnu.org/software/gettext/manual/gettext.html#The-LANGUAGE-variable)을 지정한다. 선호하는 로캘 번역이 없다면 유사한 로캘 번역이 기본 로캘 대신 사용될 것이다. 예를 들면, 한국어 사용자가 그 대안으로 다음과 같이 미국 영어와 영국 영어를 지정할 수도 있다.

 `/etc/locale.conf` 
```
LANG="ko_KR.UTF-8"
export LANGUAGE="en_US:en_GB:en"
```

## 개인 사용자 로캘 설정

앞에서도 말했지만 개별 사용자는 시스템 로캘과 다른 로캘을 사용하기를 원할 수 있다. 이를 위해 `~/.bashrc` 파일에서 `LANG` 변수를 설정한다. 예를 들어 `ko_KR.UTF-8` 로캘을 사용하려면 다음처음 설정하라.

```
export LANG=en_AU.UTF-8

```

로캘은 `~/.bashrc`가 읽어들여질 때 갱신된다. 갱신하려면 재로그인하거나 그것을 수동으로 다음과 같이 읽어들여라.

```
$ source ~/.bashrc

```

## 정렬 순서 설정

정렬은 조금 다른 문제이다. 로캘마다 서로 다른 정렬 방법을 사용한다. 잠재적 위험을 피하려고 아치는 `/etc/profile`에서 `LC_COLLATE="C"`를 지정해었다. 그러나 이 방법은 더 이상 사용되지 않는다. 이 방식을 활성화하려면 `/etc/locale.conf`에 다음을 추가하라.

```
LC_COLLATE="C"

```

ls 명령은 도트파일, 대문자, 소문자 파일 이름순으로 정렬할 것이다. `LC_COLLATE` 설정이 없으면 로캘 인식 프로그램은 `LC_ALL`이나 `LANG`에 따라 정렬하지만, `LC_COLLATE` 설정은 `LC_ALL`이 설정되면 무시될 것이다. 이것이 문제가 된다면 `/etc/profile`에 다음을 추가해 LC_ALL의 설정을 해제하라.

```
export LC_ALL=

```

LC_ALL은 `/etc/locale.conf`에서 **설정될 수 없는** 유일한 변수임을 명심하라.

## 주일의 첫 번째 요일 설정

많은 나라에서 주일의 첫 번째 요일이 월요일이다. 이를 조정하려면 `/usr/share/i18n/locales/<자신의 로캘>`에서 다음을 `LC_TIME`부분에 추가하거나 변경하라. :

```
week            7;19971130;5
first_weekday   2
first_workday   2

```

그리고 시스템을 갱신하라.

```
# locale-gen

```

**도움말:** 시스템에 문제가 생겨서 포럼, 메일링 리스트 등에 도움을 요청하고 싶다면 그 전에 `export LC_MESSAGES=C`를 설정한 상태에서 문제가 되는 프로그램의 출력을 질문 글에 포함하라. 그러면 오류나 경고 같은 프로그램 출력이 영어로 표시되어 더 많은 사람이 답할 수 있을 것이다. 비영어 포럼이라면 이렇게 할 필요가 없다.

## 문제 해결

### 터미널에서 UTF-8을 지원하지 못할 경우

불행하게도 일부 터미널은 UTF-8을 지원하지 않는다. 이런 경우에는 다른 터미널을 사용해야 한다. UTF-8 지원 터미널로 다음과 같은 것이 있다.

*   vte 기반 터미널
*   gnustep-terminal
*   konsole
*   [mlterm](/index.php/Mlterm "Mlterm")
*   rxvt-unicode
*   xterm

#### Xterm에서 UTF-8을 지원하지 못할 경우

xterm은 `uxterm`이나 `xterm -u8`로 실행해야만 UTF-8을 지원한다.

#### Gnome-터미널과 rxvt-unicode 터미널에서 UTF-8을 지원하지 못할 경우

UTF-8 로캘에서 이 프로그램을 실행해야 한다. 그렇지 않으면 UTF-8 지원을 하지 않는다. `ko_KR.UTF-8` 로캘을 위에서 설명한 대로 기본 로캘(또는 다른 언어 UTF-8) 로 설정하고 재부팅하라.

## 같이 보기

*   [젠투 리눅스 지역화 안내](http://www.gentoo.org/doc/en/guide-localization.xml)
*   [젠투 위키 보관 자료: 로캘](http://www.gentoo-wiki.info/Locales)
*   [ICU 사용자 입력 정렬 시험](http://demo.icu-project.org/icu-bin/locexp?_=en_US&x=col)
*   [Free Standards Group Open 지역화 방안](http://www.openi18n.org/)
*   [*The Single UNIX Specification* 로캘 정의](http://pubs.opengroup.org/onlinepubs/007908799/xbd/locale.html) (Open Group)