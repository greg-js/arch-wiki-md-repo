Reflector는 [MirrorStatus](https://www.archlinux.org/mirrors/status/) 페이지에서 최신 미러 사이트 목록을 받아오고 그 중 최신 미러를 골라 빠른 순서대로 정렬해서 `/etc/pacman.d/mirrorlist` 파일을 덮어 씁니다.

## 설치

[reflector](https://www.archlinux.org/packages/?name=reflector) 패키지는 [공식 저장소](/index.php/Official_repositories "Official repositories")에서 받아서 [설치](/index.php/Pacman_(%ED%95%9C%EA%B5%AD%EC%96%B4) "Pacman (한국어)")할 수 있습니다.

```
# pacman -S reflector

```

## 사용 예제

일단 기존 `/etc/pacman.d/mirrorlist` 파일을 백업합니다.

```
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

다음 명령으로 최대 5개의 미러를 가져와서 속도 순으로 정렬하고 그 결과를 `/etc/pacman.d/mirrorlist` 파일에 덮어 씁니다.

```
# reflector -l 5 --sort rate --save /etc/pacman.d/mirrorlist

```

다른 옵션을 찾아보려면 다음 명령을 입력합니다.

```
$ reflector --help

```

**경고:** 팩맨을 실행해서 동기화나 갱신을 하기 전에 미러리스트에 이상한 항목이 없는지 반드시 확인해봐야 합니다.

## 외부 문서

*   공식 프로젝트 홈페이지: [http://xyne.archlinux.ca/projects/reflector/](http://xyne.archlinux.ca/projects/reflector/)