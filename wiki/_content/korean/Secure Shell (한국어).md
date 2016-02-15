## Contents

*   [1 소개](#.EC.86.8C.EA.B0.9C)
*   [2 OpenSSH](#OpenSSH)
    *   [2.1 OpenSSH 설치](#OpenSSH_.EC.84.A4.EC.B9.98)
    *   [2.2 SSH 설정](#SSH_.EC.84.A4.EC.A0.95)
        *   [2.2.1 클라이언트](#.ED.81.B4.EB.9D.BC.EC.9D.B4.EC.96.B8.ED.8A.B8)
        *   [2.2.2 데몬](#.EB.8D.B0.EB.AA.AC)
        *   [2.2.3 접속 허용 방법](#.EC.A0.91.EC.86.8D_.ED.97.88.EC.9A.A9_.EB.B0.A9.EB.B2.95)
    *   [2.3 부팅 시 시작하기](#.EB.B6.80.ED.8C.85_.EC.8B.9C_.EC.8B.9C.EC.9E.91.ED.95.98.EA.B8.B0)
    *   [2.4 서버 접속하기](#.EC.84.9C.EB.B2.84_.EC.A0.91.EC.86.8D.ED.95.98.EA.B8.B0)
*   [3 기타 정보](#.EA.B8.B0.ED.83.80_.EC.A0.95.EB.B3.B4)
    *   [3.1 암호화된 터널](#.EC.95.94.ED.98.B8.ED.99.94.EB.90.9C_.ED.84.B0.EB.84.90)
        *   [3.1.1 1단계: 연결하기](#1.EB.8B.A8.EA.B3.84:_.EC.97.B0.EA.B2.B0.ED.95.98.EA.B8.B0)
        *   [3.1.2 2단계 : 브라우저 설정 (또는 다른 프로그램)](#2.EB.8B.A8.EA.B3.84_:_.EB.B8.8C.EB.9D.BC.EC.9A.B0.EC.A0.80_.EC.84.A4.EC.A0.95_.28.EB.98.90.EB.8A.94_.EB.8B.A4.EB.A5.B8_.ED.94.84.EB.A1.9C.EA.B7.B8.EB.9E.A8.29)
    *   [3.2 X11 포워딩](#X11_.ED.8F.AC.EC.9B.8C.EB.94.A9)
    *   [3.3 SSHFS로 원격 파일 시스템 마운트 하기](#SSHFS.EB.A1.9C_.EC.9B.90.EA.B2.A9_.ED.8C.8C.EC.9D.BC_.EC.8B.9C.EC.8A.A4.ED.85.9C_.EB.A7.88.EC.9A.B4.ED.8A.B8_.ED.95.98.EA.B8.B0)
        *   [3.3.1 Keep Alive](#Keep_Alive)
*   [4 Links & References](#Links_.26_References)

# [소개](http://http://ko.wikipedia.org/wiki/%EC%8B%9C%ED%81%90%EC%96%B4_%EC%85%B8)

SSH 또는 Secure Shell은 네트워크상의 다른 컴퓨터에 로그인하거나 원격 시스템에서 명령을 실행하고 다른 시스템으로 파일을 복사할 수 있도록 해 주는 응용 프로그램 또는 그 통신규약을 가리킵니다. 기존의 rsh, rlogin, 텔넷 등을 대체하기 위해 설계되었으며, 강력한 인증 방법 및 안전하지 못한 네트워크에서 안전하게 통신을 할 수 있는 기능을 제공합니다. 기본적으로는 22번 포트를 사용합니다.

SSH는 암호화 기법을 사용하기 때문에, 통신이 노출된다 하더라도 이해할 수 없는 암호화된 문자로 보입니다.

# OpenSSH

OpenSSH (OpenBSD Secure Shell) is a set of computer programs providing encrypted communication sessions over a computer network using the ssh protocol. It was created as an open source alternative to the proprietary Secure Shell software suite offered by SSH Communications Security. OpenSSH is developed as part of the OpenBSD project, which is led by Theo de Raadt.

OpenSSH is occasionally confused with the similarly-named OpenSSL; however, the projects have different purposes and are developed by different teams, the similar name is drawn only from similar goals.

## OpenSSH 설치

```
# pacman -S openssh

```

## SSH 설정

### 클라이언트

SSH 클라이언트 설정은 `/etc/ssh/ssh_config` 파일에서 설정할 수 있습니다.

아래는 예시입니다.

 `/etc/ssh/ssh_config` 

```
#       $OpenBSD: ssh_config,v 1.25 2009/02/17 01:28:32 djm Exp $

# This is the ssh client system-wide configuration file.  See
# ssh_config(5) for more information.  This file provides defaults for
# users, and the values can be changed in per-user configuration files
# or on the command line.

# Configuration data is parsed as follows:
#  1\. command line options
#  2\. user-specific file
#  3\. system-wide file
# Any configuration value is only changed the first time it is set.
# Thus, host-specific definitions should be at the beginning of the
# configuration file, and defaults at the end.

# Site-wide defaults for some commonly used options.  For a comprehensive
# list of available options, their meanings and defaults, please see the
# ssh_config(5) man page.

Host *
#   ForwardAgent no
#   ForwardX11 no
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
#   Protocol 2,1
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
HashKnownHosts yes
StrictHostKeyChecking ask
```

Protocol 설정을 2로 하는 것을 권장합니다.

```
Protocol 2

```

Protocol 1은 다소 불안정한 것으로 간주합니다.

### 데몬

SSH 데몬은 `/etc/ssh/ssh**d**_config` 파일에서 설정할 수 있습니다.

아래는 예시입니다.

 `/etc/ssh/sshd_config` 

```
#	$OpenBSD: sshd_config,v 1.75 2007/03/19 01:01:29 djm Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options change a
# default value.

#Port 22
#Protocol 2,1
ListenAddress 0.0.0.0
#ListenAddress ::

# HostKey for protocol version 1
#HostKey /etc/ssh/ssh_host_key
# HostKeys for protocol version 2
#HostKey /etc/ssh/ssh_host_rsa_key
#HostKey /etc/ssh/ssh_host_dsa_key

# Lifetime and size of ephemeral version 1 server key
#KeyRegenerationInterval 1h
#ServerKeyBits 768

# Logging
#obsoletes ~QuietMode and ~FascistLogging
#SyslogFacility AUTH
#LogLevel INFO

# Authentication:

#LoginGraceTime 2m
#PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6

#RSAAuthentication yes
#PubkeyAuthentication yes
#AuthorizedKeysFile     .ssh/authorized_keys

# For this to work you will also need host keys in /etc/ssh/ssh_known_hosts
#RhostsRSAAuthentication no
# similar for protocol version 2
#HostbasedAuthentication no
# Change to yes if you don't trust ~/.ssh/known_hosts for
# RhostsRSAAuthentication and HostbasedAuthentication
#IgnoreUserKnownHosts no
# Don't read the user's ~/.rhosts and ~/.shosts files
#IgnoreRhosts yes

# To disable tunneled clear text passwords, change to no here!
#PasswordAuthentication yes
#PermitEmptyPasswords no

# Change to no to disable s/key passwords
#ChallengeResponseAuthentication yes

# Kerberos options
#KerberosAuthentication no
#KerberosOrLocalPasswd yes
#KerberosTicketCleanup yes
#KerberosGetAFSToken no

# GSSAPI options
#GSSAPIAuthentication no
#GSSAPICleanupCredentials yes

# Set this to 'yes' to enable PAM authentication, account processing,
# and session processing. If this is enabled, PAM authentication will
# be allowed through the ~ChallengeResponseAuthentication mechanism.
# Depending on your PAM configuration, this may bypass the setting of
# PasswordAuthentication, ~PermitEmptyPasswords, and
# "PermitRootLogin without-password". If you just want the PAM account and
# session checks to run without PAM authentication, then enable this but set
# ChallengeResponseAuthentication=no
#UsePAM no

#AllowTcpForwarding yes
#GatewayPorts no
#X11Forwarding no
#X11DisplayOffset 10
#X11UseLocalhost yes
#PrintMotd yes
#PrintLastLog yes
#TCPKeepAlive yes
#UseLogin no
#UsePrivilegeSeparation yes
#PermitUserEnvironment no
#Compression yes
#ClientAliveInterval 0
#ClientAliveCountMax 3
#UseDNS yes
#PidFile /var/run/sshd.pid
#MaxStartups 10

# no default banner path
#Banner /some/path

# override default of no subsystems
Subsystem       sftp    /usr/lib/ssh/sftp-server
```

일부 사용자에 대해서만 사용을 허용하려면 줄을 추가하면 됩니다.

```
AllowUsers    사용자1 사용자2

```

이렇게 다음과 같이 보이는 줄들을 변경하면 원하는 설정을 할 수 있습니다.

```
Protocol 2
.
.
.
LoginGraceTime 120
.
.
.
PermitRootLogin no # (put yes here if you want root login)

```

You could also uncomment the BANNER option and edit `/etc/issue` for a nice welcome message.

**Tip:** 기본 22번 포트 말고도 다른 포트로도 변경 가능합니다.([security through obscurity](http://en.wikipedia.org/wiki/Security_through_obscurity)).

Even though the port ssh is running on could be detected by using a port-scanner like nmap, changing it will reduce the number of log entries caused by automated authentication attempts.

### 접속 허용 방법

**Note:** 기본적으로 외부에서 접속 못 하게 설정되어 있습니다.

외부에서 접속하려면 `/etc/hosts.allow` 파일에서 다음을 추가합니다.

```
# 모든 허용
sshd: ALL

# 또는 특정 IP만 허용
sshd: 192.168.0.1

# 또는 특벙 범위만 허용
sshd: 10.0.0.0/255.255.255.0

# 또는 특정 IP 대역만 허용
sshd: 192.168.1.

```

`/etc/hosts.deny` 파일을 확인하여 다음처럼 조정할 수 있습니다.

```
ALL: ALL: DENY

```

외부로 접속할 수 있으며 외부에서 내부로 접속할 수 있습니다.

새로울 설정을 이용하여 시작하려면 데몬을 재시작하면 됩니다.

```
# /etc/rc.d/sshd restart

```

## 부팅 시 시작하기

부팅 시 sshd 데몬을 시작하려면 `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` 파일에서 DAEMONS 항목에 sshd를 추가합니다.

```
DAEMONS=(... ... **sshd** ... ...)

```

데몬을 시작, 정지, 재시작을 하기 위한 명령어는 다음과 같습니다.

```
# /etc/rc.d/sshd {start|stop|restart}

```

## 서버 접속하기

서버에 접속하려면 다음과 같습니다.

```
$ ssh -p port user@server-address

```

# 기타 정보

## 암호화된 터널

이것은 무선 환경에서 연결하는데 유용합니다. 당신이 원하는 건 집이나 회사처럼 안전한 곳에서 돌아가는 SSH 서버일 것입니다. 동적인 DNS나 기억하지 않아도 되는 IP 주소에서 유용할 것입니다.

### 1단계: 연결하기

당신이 사용하는 터미널에서 다음 명령어를 사용합니다.

```
$ ssh -ND 4711 user@host

```

여기서 `"계정"`은 당신의 계정이며 `"host"`는 접속할 서버입니다. 암호를 물어보며 연결될 것입니다. `"N"` 옵션은 대화형 프롬프트 플래그를 해제합니다. 그리고 `"D"` 옵션은 내용을 수신할 로컬 컴퓨터의 포트를 지정합니다. (원한다면 언제든지 포트 번호를 선택할 수 있습니다.)

위 작업을 쉽게 하려면 `~/.bashrc` 파일에 다음과 같이 추가합니다.

```
alias sshtunnel="ssh -ND 4711 -v user@host"

```

자세한 정보를 위해 `"-v"` 옵션을 넣으시면 됩니다. 연결되는 내용을 확인할 수 있게 됩니다. 지금 `"sshtunnel"` 명령어를 실행해보세요.

### 2단계 : 브라우저 설정 (또는 다른 프로그램)

*   파이어 폭스: _도구 → 설정 → 고급 → 네티워크 → 연결 → 설정_:

	_"프록시 수동 설정"_ 체크한 후 _"SOCKS host"_ 칸에 "localhost" 를 입력합니다, 그리고 다음칸에 포트 번호를 입력합니다.

	사용하는 프로토콜로 SOCK4를 선택해야 합니다. SOCKS5는 작동하지 않습니다.

## X11 포워딩

SSH 연결을 통해 그래픽 프로그램을 실행하려면 X11 포워딩을 통하여 할 수 있습니다. 옵션은 서버와 클라이언트 구성 파일에 설정해야 합니다.

서버에 xorg-xauth를 설치 합니다.

```
# pacman -S xorg-xauth

```

*   **서버**에 **AllowTcpForwarding** 옵션을 `sshd_config`에 설정합니다.
*   **서버**에 **X11Forwarding** 옵션을 `sshd_config`에 설정합니다.
*   **서버**에 **X11DisplayOffset** 옵션을 `sshd_config`에 설정합니다.
*   **서버**에 **X11UseLocalhost** 옵션을 `sshd_config`에 설정합니다.

*   **클라이언트**에 **ForwardX11** 옵션을 `sshd_config`에 설정합니다.

SSH로 당신의 서버에 접속합니다.

```
# ssh -X -p port user@server-address

```

만약 그래픽 응용프로그램을 실행하려고 하는데 오류가 난다면 다음과 같이 합니다.:

```
# ssh -Y -p port user@server-address

```

이제 원격 서버에 있는 X 프로그램을 시작할 수 있으며 로컬 세션이 전달되어 출력됩니다.:

```
# xclock

```

## SSHFS로 원격 파일 시스템 마운트 하기

sshfs 설치

```
# pacman -S sshfs

```

Fuse 모듈 올리기

```
# modprobe fuse

```

`/etc/rc.conf`에서 _modules_ 배열란에 fuse를 추가하여 시스템 부팅 때 모듈을 올릴 수 있습니다.

sshfs를 사용하여 원격 디렉토리를 마운트

```
# mkdir ~/remote_folder
# sshfs USER@remote_server:/tmp ~/remote_folder

```

위의 명령은 로컬 컴퓨터의 ~/remote_folder 디렉토리에 원격 서버의 /tmp 디렉토리를 마운트하는 명령어입니다. Copying any file to this folder will result in transparent copying over the network using SFTP. Same concerns direct file editing, creating or removing.

When we’re done working with the remote filesystem, we can unmount the remote folder by issuing:

```
# fusermount -u ~/remote_folder

```

If we work on this folder on a daily basis, it is wise to add it to the `/etc/fstab` table. This way is can be automatically mounted upon system boot or mounted manually (if `noauto` option is chosen) without the need to specify the remote location each time. Here is a sample entry in the table:

```
sshfs#USER@remote_server:/tmp /full/path/to/directory fuse    defaults,auto    0 0

```

### Keep Alive

Your ssh session will automatically log out if it is idle. To keep the connection active (alive) add this to **~/.ssh/config** or to **/etc/ssh/ssh_config** on the client.

```
ServerAliveInterval 5

```

This will send a "keep alive" signal to the server every 5 seconds. You can usually increase this interval, and I use 120.

# Links & References

*   [A Cure for the Common SSH Login Attack](http://www.soloport.com/iptables.html)
*   [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys")
*   [Defending against brute force ssh attacks](http://www.la-samhna.de/library/brutessh.html)