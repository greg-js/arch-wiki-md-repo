Related articles

*   [File systems](/index.php/File_systems "File systems")

[F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") (Flash-Friendly File System) 는 낸드 플래시 메모리용으로 설계된 파일 시스템이다. 커널 3.8 이후로 지원되고 있다.

## F2FS 포맷 파티션 생성

F2FS 파티션을 만들기 위해서는 [공식 저장소](/index.php/Official_repositories "Official repositories")에서 [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools)를 [설치](/index.php/Install "Install")한다.

파티션 생성:

```
# mkfs.f2fs -l mylabel */dev/sdxY*

```

`*/dev/sdxY*` 부분에는 F2FS으로 포맷할 볼륨명을 넣는다.

## F2FS 파티션 마운트하기

마운트 전에 사용자가 수동으로 F2FS 커널 모듈을 로드해야 한다. root 권한으로 다음 명령어를 실행한다:

```
# modprobe f2fs

```

커널 모듈 로드 후, 다음과 같이 마운트를 할 수 있다.

```
# mount -t f2fs /dev/sdxY /mnt

```

## F2FS 파티션에 아치리눅스 설치하기

최신 [설치 미디어 파일](https://www.archlinux.org/download/)로써 F2FS 파티션에 루트가 설정된 아치리눅스를 설치할 수 있다.

1.  [#F2FS 포맷 파티션 생성](#F2FS_.ED.8F.AC.EB.A7.B7_.ED.8C.8C.ED.8B.B0.EC.85.98_.EC.83.9D.EC.84.B1)에서 기술된 것을 참고하여 F2FS로 루트 파티션을 제작한다.
2.  ext2 포맷 또는 다른 부트로더가 지원하는 파일시스템으로 `/boot` 파티션을 생성한다.
3.  [chrooted](/index.php/Change_root "Change root") 전까지 [Installation guide#Mount the file systems](/index.php/Installation_guide#Mount_the_file_systems "Installation guide")에서의 설치 과정을 따른다.
4.  [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools)를 설치한다.
5.  chroot 상태에서 [initramfs](/index.php/Initramfs "Initramfs")를 다시 생성한다.

부팅 과정에서 CRC32 모듈 로드에 실패하는 경우는 약간의 작업이 필요하다. 4.6 버전의 커널에 포함된 드라이버는 CRC32를 위해 Crypto API를 사용하므로 `crc32_generic`와 `crc32-pclmul`를 `/etc/mkinitcpio.conf`의 `MODULES`에 추가한 뒤 initramfs를 재생성한다.

부팅 과정에서 파티션을 찾지 못한다면 다른 디스크로 부팅 한 후 `/boot/grub/grub.cfg` 를 열어 `root=/dev/*sdXx*` 등으로 표기된 파티션 명을 `blkid /dev/*sdXx*` 를 입력하여 나온 [UUID](/index.php/UUID "UUID")를 가져와 `root=UUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*` 꼴로 변경하면 된다. [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") 를 참조할 수 있다.