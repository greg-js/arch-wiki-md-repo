[Clam AntiVirus](http://www.clamav.net)는 유닉스용 오픈소스 (GPL) 안티바이러스 툴킷이다. Clam AntiVirus는 유연하고 확장가능한 멀티쓰레드 데몬(daemon)과 커맨드라인 스캐너, 데이터베이스 자동 업데이트를 위한 Advanced 툴 등을 포함한 다수의 유틸리티를 제공한다. ClamAV는 기본적으로 윈도우즈 바이러스와 멀웨어를 감지하는데 그 이유는 ClamAV의 주 사용처가 윈도우즈 데스크탑을 위한 파일 서버 또는 메일 서버이기 때문이다.

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
*   [2 데이터베이스 업데이트](#.EB.8D.B0.EC.9D.B4.ED.84.B0.EB.B2.A0.EC.9D.B4.EC.8A.A4_.EC.97.85.EB.8D.B0.EC.9D.B4.ED.8A.B8)
*   [3 데몬 실행](#.EB.8D.B0.EB.AA.AC_.EC.8B.A4.ED.96.89)
*   [4 소프트웨어 테스트](#.EC.86.8C.ED.94.84.ED.8A.B8.EC.9B.A8.EC.96.B4_.ED.85.8C.EC.8A.A4.ED.8A.B8)
*   [5 데이터베이스/서명 저장소 추가하기](#.EB.8D.B0.EC.9D.B4.ED.84.B0.EB.B2.A0.EC.9D.B4.EC.8A.A4.2F.EC.84.9C.EB.AA.85_.EC.A0.80.EC.9E.A5.EC.86.8C_.EC.B6.94.EA.B0.80.ED.95.98.EA.B8.B0)
*   [6 바이러스 검사](#.EB.B0.94.EC.9D.B4.EB.9F.AC.EC.8A.A4_.EA.B2.80.EC.82.AC)
*   [7 Milter 사용](#Milter_.EC.82.AC.EC.9A.A9)
*   [8 문제 해결](#.EB.AC.B8.EC.A0.9C_.ED.95.B4.EA.B2.B0)
    *   [8.1 Error: Clamd was NOT notified](#Error:_Clamd_was_NOT_notified)
    *   [8.2 Error: No supported database files found](#Error:_No_supported_database_files_found)
    *   [8.3 Error: Can't create temporary directory](#Error:_Can.27t_create_temporary_directory)

## 설치

[clamav](https://www.archlinux.org/packages/?name=clamav) 패키지를 [설치](/index.php/Install "Install")한다.

## 데이터베이스 업데이트

다음 명령어로 바이러스 정의 파일을 업데이트할 수 있다:

```
# freshclam

```

데이터베이스 파일은 아래에 기술된 위치에 저장된다:

```
/var/lib/clamav/daily.cvd
/var/lib/clamav/main.cvd
/var/lib/clamav/bytecode.cvd

```

바이러스 정의 파일 업데이트 서비스는 `freshclamd.service`이다. 시스템 부트 시에 `freshclamd.service` 서비스가 시작되도록 활성화하여 바이러스 정의 파일이 항상 최신 상태로 유지되게 한다.

## 데몬 실행

ClamAV 서비스를 최초로 실행한다면 '반드시' 관련 데이터베이스를 업데이트해야 한다. 업데이트하지 않고 실행하면 에러가 발생한다.

데몬 실행 관련 서비스 이름은 `clamd.service`이다. 서비스 실행 전에는 반드시 `freshclam`를 실행해야 하며, 부트 시 서비스를 시작하기 위해 활성화시키려면 [Daemons](/index.php/Daemons "Daemons") 문서를 참고한다.

## 소프트웨어 테스트

[EICAR 테스트 파일](http://www.eicar.org/86-0-Intended-use.html)(바이러스 코드가 없는 무해한 서명 파일)을 통해 바이러스 정의 파일이 올바르게 되어있는지 테스트할 수 있다. 아래와 같이 clamscan을 사용하여 테스트한다.

```
$ wget -O- [http://www.eicar.org/download/eicar.com.txt](http://www.eicar.org/download/eicar.com.txt) | clamscan -

```

파일이 정상이라면 다음과 같은 메세지가 출력된다.

```
stdin: Eicar-Test-Signature FOUND

```

위와 같은 메세지가 출력되지 않는 경우, 문서 아래의 문제해결을 읽어보거나 [아치리눅스 포럼](https://bbs.archlinux.org/)에 질문할 것을 권한다.

## 데이터베이스/서명 저장소 추가하기

ClamAV는 다른 저장소나 보안 업체들의 데이터베이스나 서명을 사용할 수 있다.

간단한 방법으로써 몇몇 중요 저장소들을 한번에 추가하고 싶다면 [clamav-unofficial-sigs](https://aur.archlinux.org/packages/clamav-unofficial-sigs/)를 설치하고 `/etc/clamav-unofficial-sigs/user.conf` 파일을 설정한다.

이 방법은 MalwarePatrol, SecuriteInfo, Yara, Linux Malware Detect,... 등의 저장소들의 서명, 데이터베이스를 추가한다.

## 바이러스 검사

특정 파일이나 홈 디렉토리, 전체 시스템을 검사하기 위해서는 `clamscan` 명령어를 사용한다:

```
$ clamscan myfile
$ clamscan --recursive=yes --infected /home # or -r -i
$ clamscan --recursive=yes --infected --exclude-dir='^/sys|^/proc|^/dev|^/lib|^/bin|^/sbin' /

```

`clamscan` 명령어 실행으로 감염된 파일을 삭제하게 하려면 `--remove` 옵션을 추가하고, 검역소(특정 디렉토리)로 옮기게 하려면 `--move=/dir` 옵션을 사용한다.

대용량 파일 검사 시에도 `clamscan`를 사용할 수 있다. 이러한 경우에는 `--max-filesize=2000M`, `--max-scansize=2000M`와 같은 옵션들을 사용한다.

추가적으로 `-l /path/to/file` 옵션은 인자로 넘겨준 경로에 있는 파일에 감염파일 위치 정보를 로깅한다.

## Milter 사용

`/etc/clamav/clamav-milter.conf.sample` 파일을 `/etc/clamav/clamav-milter.conf`에 복사한 후 편집한다. 다음 코드는 해당 파일 예제이다:

 `/etc/clamav/clamav-milter.conf` 
```
MilterSocket /run/clamav/clamav-milter.sock
MilterSocketMode 660
FixStaleSocket yes
User clamav
PidFile /run/clamav/clamav-milter.pid
TemporaryDirectory /tmp
ClamdSocket unix:/var/lib/clamav/clamd.sock
LogSyslog yes
LogInfected Basic

```

`/etc/systemd/system/clamav-milter.service` 파일을 생성한다:

 `/etc/systemd/system/clamav-milter.service` 
```
[Unit]
Description='ClamAV Milter'
After=clamd.service

[Service]
Type=forking
ExecStart=/usr/bin/clamav-milter --config-file /etc/clamav/clamav-milter.conf

[Install]
WantedBy=multi-user.target

```

해당 서비스를 활성화한 뒤 실행한다.

## 문제 해결

### Error: Clamd was NOT notified

freshclam 실행 후 다음과 같은 메세지가 출력됐다면,

```
WARNING: Clamd was NOT notified: Cannot connect to clamd through 
/var/lib/clamav/clamd.sock connect(): No such file or directory

```

ClamAV 전용 sock 파일을 추가한다:

```
# touch /var/lib/clamav/clamd.sock
# chown clamav:clamav /var/lib/clamav/clamd.sock

```

그리고나서 `/etc/clamav/clamd.conf` 파일을 열어 아래 주석을 해제한다:

```
LocalSocket /var/lib/clamav/clamd.sock

```

파일 저장 후 [데몬을 재시작한다](/index.php/Daemons "Daemons").

### Error: No supported database files found

데몬 실행 시에 다음과 같은 에러가 출력되는 경우:

```
LibClamAV Error: cli_loaddb(): No supported database files found
in /var/lib/clamav ERROR: Not supported data format

```

이 문제는 `/etc/freshclam.conf` 파일에 정의된 `DatabaseDirectory` 값과 `/etc/clamd.conf` 파일에 정의된 `DatabaseDirectory` 값이 일치하지 않아 생기는 문제이다. `/etc/clamd.conf` 내의 DatabaseDirectory를 `/etc/clamd.conf` 파일 안의 DatabaseDirectory와 같은 값으로 변경한다. 변경하고나면 clamav가 성공적으로 실행된다.

**Tip:** `/etc/freshclam.conf`는 기본으로 `/var/lib/clamav`를 가리킨다. 하지만 사용자 설정으로 다른 디렉토리를 가리키도록 변경할 수 있다.

### Error: Can't create temporary directory

다음과 같은 에러메세지가 출력되는 경우 UID와 GID 숫자를 포함하고 있는 힌트를 따른다:

```
# can't create temporary directory

```

올바른 권한으로 설정:

```
# chown UID:GID /var/lib/clamav & chmod 755 /var/lib/clamav

```