**pkgfile**은 어떤 꾸러미가 특정한 파일을 포함하는지 또는 특정 꾸러미가 어떤 파일을 포함하는지를 나타내는 도구이다.

[공식 저장소](/index.php/Official_repositories "Official repositories")에서 [pkgfile](https://www.archlinux.org/packages/?name=pkgfile)이나 [AUR](/index.php/AUR "AUR")에서 [pkgfile-git](https://aur.archlinux.org/packages/pkgfile-git/)을 [설치](/index.php/Pacman "Pacman")할 수 있다.

설치 후에 루트 권한으로 다음과 같이 파일 데이터베이스를 갱신하라.

```
# pkgfile --update

```

#### 보기

 `$ pkgfile *makepkg*     #"makepkg"라는 파일을 포함하는 꾸러미를 검색`  `core/pacman           #검색한 파일이 [core] 저장소에 있는 [pacman](https://www.archlinux.org/packages/?name=pacman) 꾸러미에 있다.` 

또 다른 보기:

 `$ pkgfile --list *core/archlinux-keyring*     #[core] 저장소에 있는 [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) 꾸러미가 제공하는 모든 파일을 열거한다.` 
```
core/archlinux-keyring usr/
core/archlinux-keyring usr/share/
core/archlinux-keyring usr/share/pacman/
core/archlinux-keyring usr/share/pacman/keyrings/
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-revoked
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-trusted
core/archlinux-keyring usr/share/pacman/keyrings/archlinux.gpg
```

### "Command not found" 후크

pkgfile은 "command not found" 후크가 내장되어 있어서 인식하지 못하는 명령어를 입력하면 자동적으로 공식 저장소를 검색할 것이다.

자식 쉘에서 이를 활성화하려면 자신의 쉘 초기화 파일에서 이 후크를 불러들여야 한다.

*   [Bash](/index.php/Bash "Bash")의 경우:

 `~/.bashrc`  `source /usr/share/doc/pkgfile/command-not-found.bash` 

*   [Zsh](/index.php/Zsh "Zsh")의 경우:

 `~/.zshrc`  `source /usr/share/doc/pkgfile/command-not-found.zsh` 

## 같이 보기

*   [Bash#The_"command_not_found"_hook](/index.php/Bash#The_.22command_not_found.22_hook "Bash") - [pkgfile](https://www.archlinux.org/packages/?name=pkgfile)과 [command-not-found](https://aur.archlinux.org/packages/command-not-found/) 비교