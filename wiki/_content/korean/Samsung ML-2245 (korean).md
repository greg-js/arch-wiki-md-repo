## Contents

*   [1 소개](#.EC.86.8C.EA.B0.9C)
    *   [1.1 문제](#.EB.AC.B8.EC.A0.9C)
*   [2 설치](#.EC.84.A4.EC.B9.98)
    *   [2.1 그래서, **셋째** - **필터 수동 설치**](#.EA.B7.B8.EB.9E.98.EC.84.9C.2C_.EC.85.8B.EC.A7.B8_-_.ED.95.84.ED.84.B0_.EC.88.98.EB.8F.99_.EC.84.A4.EC.B9.98)

# 소개

## 문제

삼성 ML-2245는 삼성이 만든 프린터입니다. 이는 SPL (Samsung Printer Language)를 사용하지만, [CUPS](/index.php/CUPS "CUPS")와 작동합니다. "삼성"이 만든 공식 드라이버가 있지만, 나의 x86_64 PC에 설치하는데 성공하지 못했습니다. 이 기사는 어떻게 작동하게 하는 방법에 대한 것입니다.

# 설치

**첫째**, CUPS와 SPL 드라이버를 "팩맨"으로 설치합니다.

```
# pacman -Ss cups
extra/cups 1.3.9-4
:The CUPS Printing System
extra/cups-pdf 2.4.8-1
:PDF printer for cups
...
community/splix 2.0.0-1
:CUPS drivers for SPL (Samsung Printer Language) printers
...

# pacman -S extra/cups extra/cups-pdf community/splix
...

```

**둘째** CUPS 설정 ([참조](/index.php?title=CUPS_(%ED%95%9C%EA%B5%AD%EC%96%B4)&action=edit&redlink=1 "CUPS (한국어) (page does not exist)")) 그리고 ML-2245 [추가 (http://localhost:631)](http://localhost:631):

```
(관리) -> (프린터/프린터 추가) 

```

하지만 불행하게도 커뮤니티/splix 패키지에 CUPS용 필터가 없네요!

## 그래서, **셋째** - **필터 수동 설치**

공식 삼성 통합 리눅스 드라이버 (27.2 MB)를 다운로드 [[1]](http://www.samsung.com/download/Model_Select.aspx?type=Printer&typecode=15&subtype=Laser+Printer&subtypecode=1501&model=ML-2245&filetype=DR&language=) 타르볼을 풉니다.

```
$ tar -xzvf UnifiedLinuxDriver.tar.gz
...
$ ls -l
...
-rw-r--r-- 1 a users 30149710 Мар  2 00:45 UnifiedLinuxDriver.tar.gz
drwxr-xr-x 3 a users     4096 Янв  6 04:32 cdroot
$ ls -l cdroot/
итого 8
drwxr-xr-x 5 a users 4096 Янв  6 04:32 Linux
-r-xr-xr-x 1 a users   60 Сен 26 17:47 autorun
$ ls -l cdroot/Linux/
итого 136
-r-xr-xr-x 1 a users  3451 Сен 26 17:47 Installer.htm
-r-xr-xr-x 1 a users   204 Сен 17  2007 OEM.ini
-r-xr-xr-x 1 a users  3825 Сен 26 17:47 check_installation.sh
drwxr-xr-x 8 a users  4096 Янв  6 04:32 i386
-r-xr-xr-x 1 a users 52321 Сен 26 17:47 install.sh
drwxr-xr-x 5 a users  4096 Янв  6 04:32 noarch
-r-xr-xr-x 1 a users 52321 Сен 26 17:47 uninstall.sh
drwxr-xr-x 8 a users  4096 Янв  6 04:32 x86_64

```

**cdroot/Linux/${arch}** - ${arch}는 i386 또는 x86_64 - 당신이 필요한대로. 예를 들면,

```
ls -l cdroot/Linux/x86_64/at_root/usr/lib64/cups/filter/
итого 1560
-rwxr-xr-x 1 a users 608624 Авг 29  2008 libscmssc.so
-rwxr-xr-x 1 a users 632192 Авг 29  2008 libscmssf.so
-rwxr-xr-x 1 a users  13672 Сен 17 17:53 pscms
-rwxr-xr-x 1 a users  65448 Сен 17 17:53 rastertosamsunginkjet
-rwxr-xr-x 1 a users  44328 Сен 17 17:53 rastertosamsungpcl
-rwxr-xr-x 1 a users  69216 Сен 17 17:53 rastertosamsungspl
-rwxr-xr-x 1 a users 132936 Сен 17 17:53 rastertosamsungsplc

```

우리의 필터들이 있네요!

ML-2245 필터를 수동으로 설치합니다.

```
# cp /cdroot/Linux/x86_64/at_root/usr/lib64/cups/filter/rastertosamsungspl \
  /usr/lib/cups/filter/
# chown root:root /usr/lib/cups/filter/rastertosamsungspl
# chmod 644 /usr/lib/cups/filter/rastertosamsungspl

```

이게 답니다. 이론상, 설치는 끝 - 당장 프린터를 쓸 수 있습니다 :) Гуд лак! (*러시아어* [Udachi!](http://translate.google.ru/translate_t?hl=ru#ru%7Cen%7C%D0%A3%D0%B4%D0%B0%D1%87%D0%B8))