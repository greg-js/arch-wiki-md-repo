이 문서는 *less, ls, grep* 등 GNU/Linux 시스템 상에서 *Core utilities*라고 불리는 유틸리티들에 대해 설명합니다. 이 문서는 GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) 패키지에 포함되어 있는 유틸리티 등을 포함합니다. 아래에는 해당 유틸리티들에 대한 유용한 도움말과 기타 정보가 제공됩니다.

## Contents

*   [1 기본적 명령어](#.EA.B8.B0.EB.B3.B8.EC.A0.81_.EB.AA.85.EB.A0.B9.EC.96.B4)
*   [2 cat](#cat)
*   [3 dd](#dd)
    *   [3.1 dd 실행 중 진행률 확인하기](#dd_.EC.8B.A4.ED.96.89_.EC.A4.91_.EC.A7.84.ED.96.89.EB.A5.A0_.ED.99.95.EC.9D.B8.ED.95.98.EA.B8.B0)
        *   [3.1.1 파이프 뷰어 사용하기](#.ED.8C.8C.EC.9D.B4.ED.94.84_.EB.B7.B0.EC.96.B4_.EC.82.AC.EC.9A.A9.ED.95.98.EA.B8.B0)
    *   [3.2 dd의 변형판](#dd.EC.9D.98_.EB.B3.80.ED.98.95.ED.8C.90)
*   [4 grep](#grep)
    *   [4.1 컬러 출력](#.EC.BB.AC.EB.9F.AC_.EC.B6.9C.EB.A0.A5)
    *   [4.2 표준 오류](#.ED.91.9C.EC.A4.80_.EC.98.A4.EB.A5.98)
*   [5 iconv](#iconv)
*   [6 ip](#ip)
*   [7 less](#less)
*   [8 ls](#ls)
*   [9 mkdir](#mkdir)
*   [10 mv](#mv)
*   [11 rm](#rm)
*   [12 sed](#sed)
*   [13 seq](#seq)
*   [14 같이 보기](#.EA.B0.99.EC.9D.B4_.EB.B3.B4.EA.B8.B0)

## 기본적 명령어

아래의 표는 리눅스 사용자라면 익숙해져야할 기본적인 명령어들입니다. **볼드**처리된 명령어들은 쉘의 일부이며, 나머지는 독립된 프로그램들입니다. 아래의 섹션들과 관련 문서들을 참고하십시오.

| Command | Description | Example |
| man | 명령어에 대한 설명을 표시합니다. | man ed |
| **cd** | 작업중인 디렉토리를 바꿉니다. | cd /etc/pacman.d |
| mkdir | 디렉토리를 만듭니다. | mkdir ~/newfolder |
| rmdir | 빈 디렉토리를 삭제합니다. | rmdir ~/emptyfolder |
| rm | 파일을 삭제합니다. | rm -r ~/file.txt |
| rm -r | 디렉토리와 그 안의 파일들을 삭제합니다. | rm -r ~/.cache |
| ls | 파일의 목록을 출력합니다. | ls *.avi |
| ls -a | 숨겨진 파일 역시 표시합니다. | ls -a /home/archie |
| ls -al | 숨겨진 파일을 표시하고 파일 속성을 같이 출력합니다. |
| mv | 파일을 옮깁니다. | mv ~/compressed.zip ~/archive/compressed2.zip |
| cp | 파일을 복사합니다. | cp ~/.bashrc ~/.bashrc.bak |
| chmod +x | 파일을 실행가능하게 만듭니다. | chmod +x ~/.local/bin/myscript.sh |
| cat | 파일의 내용을 표시합니다. | cat /etc/hostname |
| strings | 바이너리 파일 안에서 출력 가능한 문자열을 출력합니다. | strings /usr/bin/free |
| find | 파일을 찾습니다. | find ~ -name myfile |
| mount | 파티션을 마운트합니다. | mount /dev/sdc1 /media/usb |
| df -h | 각 파티션에 남은 공간을 표시합니다. |
| ps -A | 실행중인 프로세스를 모두 표시합니다. |
| killall | 특정 프로세스의 인스턴스를 모두 종료합니다. |

## cat

[위키백과에서:](https://ko.wikipedia.org/w/index.php?title=Cat_%28%EC%9C%A0%EB%8B%89%EC%8A%A4%29&) *cat* 명령어는 파일들을 연결하고 표시하기 위해 사용되는 표준 유닉스 프로그램입니다.

*   *cat*은 쉘에 포함된 프로그램이 아닙니다. 스크립트를 작성하고 있거나, 성능을 향상하고 싶은 사용자라면 많은 경우에[리다이렉션](https://ko.wikipedia.org/wiki/%EB%A6%AC%EB%8B%A4%EC%9D%B4%EB%A0%89%EC%85%98)을 사용하는 것이 유용할 수 있습니다. 실제로 `< *file*` 명령은 `cat *file*`과 같은 기능을 합니다.

*   *cat*은 여러 줄을 처리할 수 있습니다. 그러나 경우에 따라 cat을 이렇게 사용하는 것은 권장되지 않습니다.

```
$ cat << EOF >> *path/file*
*first line*
...
*last line*
EOF

```

	이런 경우 *echo* 명령어를 사용하는 것이 낫습니다.

```
$ echo "\
*first line*
...
*last line*" \
>> *path/file*

```

*   파일을 역순으로 나열해야 한다면, [tac](https://en.wikipedia.org/wiki/tac_(Unix) 명령어를 사용하십시오. (tac은 cat을 거꾸로 쓴 것입니다.)

## dd

[dd](https://en.wikipedia.org/wiki/dd_(Unix) "wikipedia:dd (Unix)")는 유닉스 계열의 운영체제의 명령어로서, 파일 변환과 복사를 주 목적으로 합니다.

**참고:** *cp* 명령어는 기타 피연산자 없이도 *dd*와 같은 작업을 실행합니다. 하지만 *cp*는 *dd*와는 다르게 다양한 디스크를 지우는 작업을 지원하지 않습니다.

### dd 실행 중 진행률 확인하기

기본적으로 *dd*는 작업이 완료되기 전까지 아무런 메시지도 출력하지 않습니다. *kill*명령어와 `USR1` 신호를 사용하면 dd를 실제로 종료시키지 않고도 진행률을 확인할 수 있습니다. 두번째 터미널 에뮬레이터에서 루트 권한으로 `killall -USR1 dd` 명령을 실행하십시오.

**참고:** 이 명령은 실행중인 모든 *dd* 프로세스에 작용합니다.

또는,

```
# kill -USR1 *dd_명령어의_pid*

```

를 사용할 수 있습니다.

예를 들어,

```
# kill -USR1 $(dd_프로세스의_pid)

```

를 사용하십시오.

이 명령을 사용할 경우, *dd*는 즉시 진행률을 터미널에 출력합니다. 다음과 유사한 내용이 출력됩니다.

```
605+0 records in
605+0 records out
634388480 bytes (634 MB) copied, 8.17097 s, 77.6 MB/s

```

#### 파이프 뷰어 사용하기

[pv](https://www.archlinux.org/packages/?name=pv)를 사용하여 dd-pipeline의 상태를 보는 것도 가능합니다.

```
# dd if=*/소스/파일스트림* | pv -*모니터링_옵션* -s *파일_크기* | dd of=*/목표지점/파일스트림*

```

파이프 뷰어를 더욱 쉽게 사용하기 위해서 bashrc나 zshrc에 다음을 추가할 수 있습니다.

```
copy() {
    size=$(stat -c%s $1)
    dd if=$1 &> /dev/null | pv -petrb -s $size | dd of=$2
}

```

```
# copy */소스/파일* */목표지점/파일*

```

과 같이 사용할 수 있습니다.

### dd의 변형판

*dd*와 유사하지만 단순한 상태 바 등을 통해 주기적으로 상태를 출력하는 프로그램들도 있습니다.

	dcfldd

	[dcfldd](https://www.archlinux.org/packages/?name=dcfldd)는 dd의 확장판으로서, 보안 및 데이터 복구, 조사 등을 위한 유용한 추가 기능을 포함합니다. dd에서 사용할 수 있는 대부분의 파라미터를 dcfldd에서도 사용할 수 있으며, dcfldd는 자동으로 상태를 출력합니다. 가장 최근의 안정화판은 2006년 12월 19일에 출시되었습니다.

	ddrescue

	GNU [ddrescue](https://www.archlinux.org/packages/?name=ddrescue)는 데이터 복구용 도구입니다. 읽기 오류를 무시하는 기능을 포함합니다. 이 기능은 대개의 경우 사용할 필요가 없을 것입니다. [공식 설명서](http://www.gnu.org/software/ddrescue/manual/ddrescue_manual.html)를 참고하십시오.

## grep

grep은 유닉스용 명령줄 텍스트 검색 프로그램입니다. ([ed 텍스트 편집기](https://en.wikipedia.org/wiki/Ed_(text_editor) "wikipedia:Ed (text editor)")의 g/re/p(모든 범위/정규표현식/출력) 명령어에서 유래되었습니다) *grep* 명령어는 표준 입력 내용 혹은 파일들에서 주어진 정규표현식과 일치하는 줄들을 찾고, 표준 출력에서 검색 결과를 표시합니다.

*   *grep*은 파일을 처리합니다. 그러므로 `cat *파일*`과 같은 명령 대신 `grep *파일* *패턴*`으로 대체해도 무관합니다.
*   버전 컨트롤 시스템 안의 소스 코드를 위하여 최적화된 `grep` 대용판들에는 [the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher)과 [ack](https://www.archlinux.org/packages/?name=ack) 등이 있습니다.

### 컬러 출력

`grep`의 컬러 출력 기능은 [정규표현식](https://ko.wikipedia.org/wiki/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D)과 `grep`의 추가적인 기능을 익히는 데에 도움이 될 수 있습니다.

*grep*의 컬러 출력을 활성화하려면 다음 항목을 쉘의 설정 파일에 추가하십시오. (이 예에서는 [Bash](/index.php/Bash "Bash")를 사용할 경우를 보여줍니다)

 `~/.bashrc`  `alias grep='grep --color=auto'` 

`GREP_COLOR` 환경 변수는 기본 색을 선택하는 데에 사용할 수 있습니다. 기본 설정값은 붉은색입니다. 색깔을 바꾸기 위해서는 원하는 색깔의 [ANSI escape sequence](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html)를 알아낸 후에 그 값을 쉘의 설정파일에 추가하십시오.

```
export GREP_COLOR="1;32"

```

`GREP_COLORS` 변수는 특정 검색에만 적용되도록 설정할 수 있습니다.

### 표준 오류

어떤 명령어들은 출력을 표준 오류로 보내기도 합니다. 이 경우, grep은 아무련 효과도 없는 것처럼 보입니다. 이 때에는 표준 오류의 출력을 표준 출력으로 리다이렉트해주면 됩니다.

```
$ *command* 2>&1 | grep *args*

```

혹은 Bash 단축명령어로

```
$ *command* |& grep *args*

```

[I/O 리다이렉션](http://www.tldp.org/LDP/abs/html/io-redirection.html) 문서를 참고하십시오.

## iconv

## ip

## less

## ls

## mkdir

## mv

## rm

## sed

## seq

## 같이 보기