**الصدفة الآمنة** (**SSH**) هي بروتوكول من بروتوكولات الشبكة التي تسمح بتبادل البيانات عبر محطة آمنة بين حاسبين مختلفين, التشفير يضمن سرية المعلومات. إن ssh يستخدم التعمية بالمفتاح العمومي لكي يتم الإستيثاق بالحاسب الذي يقوم بإجراء الإتصال وللسماح بالإستيثاق من المستخدم إذا كان ذلك ضروريًا.

بشكل عام تُستخدم ssh للولوج الى حاسب عن بعد و تنفيذ أوامر, لكنها أيضًا تدعم إنشاء لأنفاق الآمنة بالإضافة الى تمرير المنافذ و إتصالات X11 ونقل الملفات يمكن أن يتم يإستخدام بروتوكول sftp أو بروتوكول scp.

إن خادم ssh بشكل إفتراضي يقوم بإستقبال الإتصالات عبر المنفذ الإفتراضي 22 tcp, عميل ssh هو عبارة عن برنامج يُستخدم لإنشاء إتصال الى خدمة ssh في حال تم إعداده لقبول الإتصالات. كلاهما يتوفر بشكل كبير في الأنظمة الشهيرة كنظام Mac OS X, GNU/Linux, Solaris و OpenVMS. برامج مملوكة و مفتوحة المصدر بمختلف الإصدارات ومختلف مراحل التعقيد و الكمالية متوفرة في الوقت الراهن.

(Source: [Wikipedia:Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell "wikipedia:Secure Shell"))

## Contents

*   [1 OpenSSH](#OpenSSH)
    *   [1.1 Installing OpenSSH](#Installing_OpenSSH)
    *   [1.2 تهيئة إعدادات ssh](#.D8.AA.D9.87.D9.8A.D8.A6.D8.A9_.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA_ssh)
        *   [1.2.1 العميل](#.D8.A7.D9.84.D8.B9.D9.85.D9.8A.D9.84)
        *   [1.2.2 خدمة ssh](#.D8.AE.D8.AF.D9.85.D8.A9_ssh)
    *   [1.3 إدارة خدمة ssh](#.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.AE.D8.AF.D9.85.D8.A9_ssh)
    *   [1.4 الإتصال بالخادم](#.D8.A7.D9.84.D8.A5.D8.AA.D8.B5.D8.A7.D9.84_.D8.A8.D8.A7.D9.84.D8.AE.D8.A7.D8.AF.D9.85)
*   [2 عملاء و خوادم ssh الاخرى](#.D8.B9.D9.85.D9.84.D8.A7.D8.A1_.D9.88_.D8.AE.D9.88.D8.A7.D8.AF.D9.85_ssh_.D8.A7.D9.84.D8.A7.D8.AE.D8.B1.D9.89)
    *   [2.1 Dropbear](#Dropbear)
    *   [2.2 Mosh بديل SSH](#Mosh_.D8.A8.D8.AF.D9.8A.D9.84_SSH)
*   [3 تلمحيات](#.D8.AA.D9.84.D9.85.D8.AD.D9.8A.D8.A7.D8.AA)
    *   [3.1 انبوب SOCKS مُشفر](#.D8.A7.D9.86.D8.A8.D9.88.D8.A8_SOCKS_.D9.85.D9.8F.D8.B4.D9.81.D8.B1)
        *   [3.1.1 الخطوة الولى : قم ببدء الإتصال](#.D8.A7.D9.84.D8.AE.D8.B7.D9.88.D8.A9_.D8.A7.D9.84.D9.88.D9.84.D9.89_:_.D9.82.D9.85_.D8.A8.D8.A8.D8.AF.D8.A1_.D8.A7.D9.84.D8.A5.D8.AA.D8.B5.D8.A7.D9.84)
        *   [3.1.2 الخطوة الثانية : إعداد المتصفح (أو بقية البرامج)](#.D8.A7.D9.84.D8.AE.D8.B7.D9.88.D8.A9_.D8.A7.D9.84.D8.AB.D8.A7.D9.86.D9.8A.D8.A9_:_.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF_.D8.A7.D9.84.D9.85.D8.AA.D8.B5.D9.81.D8.AD_.28.D8.A3.D9.88_.D8.A8.D9.82.D9.8A.D8.A9_.D8.A7.D9.84.D8.A8.D8.B1.D8.A7.D9.85.D8.AC.29)
    *   [3.2 تمرير X11](#.D8.AA.D9.85.D8.B1.D9.8A.D8.B1_X11)
    *   [3.3 تمرير المنافذ الاخرى](#.D8.AA.D9.85.D8.B1.D9.8A.D8.B1_.D8.A7.D9.84.D9.85.D9.86.D8.A7.D9.81.D8.B0_.D8.A7.D9.84.D8.A7.D8.AE.D8.B1.D9.89)
    *   [3.4 تسريع ssh](#.D8.AA.D8.B3.D8.B1.D9.8A.D8.B9_ssh)
    *   [3.5 وصل نظام ملفات خاص بحاسب بعيد عن طريق sshfs](#.D9.88.D8.B5.D9.84_.D9.86.D8.B8.D8.A7.D9.85_.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.AE.D8.A7.D8.B5_.D8.A8.D8.AD.D8.A7.D8.B3.D8.A8_.D8.A8.D8.B9.D9.8A.D8.AF_.D8.B9.D9.86_.D8.B7.D8.B1.D9.8A.D9.82_sshfs)
    *   [3.6 إبقاء الإتصال مفتوحًا](#.D8.A5.D8.A8.D9.82.D8.A7.D8.A1_.D8.A7.D9.84.D8.A5.D8.AA.D8.B5.D8.A7.D9.84_.D9.85.D9.81.D8.AA.D9.88.D8.AD.D9.8B.D8.A7)
    *   [3.7 حفظ بيانات الإتصال في ملف إعدادات ssh](#.D8.AD.D9.81.D8.B8_.D8.A8.D9.8A.D8.A7.D9.86.D8.A7.D8.AA_.D8.A7.D9.84.D8.A5.D8.AA.D8.B5.D8.A7.D9.84_.D9.81.D9.8A_.D9.85.D9.84.D9.81_.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA_ssh)
    *   [3.8 إعادة تشغيل جلسات و انفاق ssh تلقائيًا - Autossh](#.D8.A5.D8.B9.D8.A7.D8.AF.D8.A9_.D8.AA.D8.B4.D8.BA.D9.8A.D9.84_.D8.AC.D9.84.D8.B3.D8.A7.D8.AA_.D9.88_.D8.A7.D9.86.D9.81.D8.A7.D9.82_ssh_.D8.AA.D9.84.D9.82.D8.A7.D8.A6.D9.8A.D9.8B.D8.A7_-_Autossh)
*   [4 إستكشاف الأخطاء وإصلاحها](#.D8.A5.D8.B3.D8.AA.D9.83.D8.B4.D8.A7.D9.81_.D8.A7.D9.84.D8.A3.D8.AE.D8.B7.D8.A7.D8.A1_.D9.88.D8.A5.D8.B5.D9.84.D8.A7.D8.AD.D9.87.D8.A7)
    *   [4.1 الإتصالات تُرفض أو تنتهي مدتها](#.D8.A7.D9.84.D8.A5.D8.AA.D8.B5.D8.A7.D9.84.D8.A7.D8.AA_.D8.AA.D9.8F.D8.B1.D9.81.D8.B6_.D8.A3.D9.88_.D8.AA.D9.86.D8.AA.D9.87.D9.8A_.D9.85.D8.AF.D8.AA.D9.87.D8.A7)
        *   [4.1.1 هل الراوتر لديك يقوم بتمرير المنافذ؟](#.D9.87.D9.84_.D8.A7.D9.84.D8.B1.D8.A7.D9.88.D8.AA.D8.B1_.D9.84.D8.AF.D9.8A.D9.83_.D9.8A.D9.82.D9.88.D9.85_.D8.A8.D8.AA.D9.85.D8.B1.D9.8A.D8.B1_.D8.A7.D9.84.D9.85.D9.86.D8.A7.D9.81.D8.B0.D8.9F)
        *   [4.1.2 هل خدمة ssh تعمل؟](#.D9.87.D9.84_.D8.AE.D8.AF.D9.85.D8.A9_ssh_.D8.AA.D8.B9.D9.85.D9.84.D8.9F)
        *   [4.1.3 هل يقوم الجدار الناري الخاص بك بحجب الإتصالات ؟](#.D9.87.D9.84_.D9.8A.D9.82.D9.88.D9.85_.D8.A7.D9.84.D8.AC.D8.AF.D8.A7.D8.B1_.D8.A7.D9.84.D9.86.D8.A7.D8.B1.D9.8A_.D8.A7.D9.84.D8.AE.D8.A7.D8.B5_.D8.A8.D9.83_.D8.A8.D8.AD.D8.AC.D8.A8_.D8.A7.D9.84.D8.A5.D8.AA.D8.B5.D8.A7.D9.84.D8.A7.D8.AA_.D8.9F)
        *   [4.1.4 هل يصل الإتصال أساسًا الى جهازك؟](#.D9.87.D9.84_.D9.8A.D8.B5.D9.84_.D8.A7.D9.84.D8.A5.D8.AA.D8.B5.D8.A7.D9.84_.D8.A3.D8.B3.D8.A7.D8.B3.D9.8B.D8.A7_.D8.A7.D9.84.D9.89_.D8.AC.D9.87.D8.A7.D8.B2.D9.83.D8.9F)
        *   [4.1.5 هل يقوم مزود الخدمة الخاص بك أو أي جهة اخرى بحجب المنفذ الإفتراضي ؟](#.D9.87.D9.84_.D9.8A.D9.82.D9.88.D9.85_.D9.85.D8.B2.D9.88.D8.AF_.D8.A7.D9.84.D8.AE.D8.AF.D9.85.D8.A9_.D8.A7.D9.84.D8.AE.D8.A7.D8.B5_.D8.A8.D9.83_.D8.A3.D9.88_.D8.A3.D9.8A_.D8.AC.D9.87.D8.A9_.D8.A7.D8.AE.D8.B1.D9.89_.D8.A8.D8.AD.D8.AC.D8.A8_.D8.A7.D9.84.D9.85.D9.86.D9.81.D8.B0_.D8.A7.D9.84.D8.A5.D9.81.D8.AA.D8.B1.D8.A7.D8.B6.D9.8A_.D8.9F)
            *   [4.1.5.1 التحقق بإستخدام Wireshark](#.D8.A7.D9.84.D8.AA.D8.AD.D9.82.D9.82_.D8.A8.D8.A5.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_Wireshark)
            *   [4.1.5.2 حل هذه المشكلة](#.D8.AD.D9.84_.D9.87.D8.B0.D9.87_.D8.A7.D9.84.D9.85.D8.B4.D9.83.D9.84.D8.A9)
        *   [4.1.6 مشكلة Read from socket failed: connection reset by peer](#.D9.85.D8.B4.D9.83.D9.84.D8.A9_Read_from_socket_failed:_connection_reset_by_peer)
    *   [4.2 "[الصدفة التي تستخدمها]: No such file or directory"](#.22.5B.D8.A7.D9.84.D8.B5.D8.AF.D9.81.D8.A9_.D8.A7.D9.84.D8.AA.D9.8A_.D8.AA.D8.B3.D8.AA.D8.AE.D8.AF.D9.85.D9.87.D8.A7.5D:_No_such_file_or_directory.22)
    *   [4.3 ظهور رسالة الخطأ "Terminal unknown" أو "Error opening terminal"](#.D8.B8.D9.87.D9.88.D8.B1_.D8.B1.D8.B3.D8.A7.D9.84.D8.A9_.D8.A7.D9.84.D8.AE.D8.B7.D8.A3_.22Terminal_unknown.22_.D8.A3.D9.88_.22Error_opening_terminal.22)
        *   [4.3.1 الحل بواسطة المتغير $TERM](#.D8.A7.D9.84.D8.AD.D9.84_.D8.A8.D9.88.D8.A7.D8.B3.D8.B7.D8.A9_.D8.A7.D9.84.D9.85.D8.AA.D8.BA.D9.8A.D8.B1_.24TERM)
        *   [4.3.2 الحل بإستخدام ملف terminfo](#.D8.A7.D9.84.D8.AD.D9.84_.D8.A8.D8.A5.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D9.85.D9.84.D9.81_terminfo)
*   [5 شاهد أيضًا](#.D8.B4.D8.A7.D9.87.D8.AF_.D8.A3.D9.8A.D8.B6.D9.8B.D8.A7)
*   [6 Links & references](#Links_.26_references)

## OpenSSH

إن openssh (OpenBSD Secure Shell) هو مجموعة من برامج الحاسب التي توفر وسيلة تواصل مشفرة بين شبكة من الحواسيب بإستخدام بروتوكول ssh, تم تطويرها لتُشكل بديلاً عن برمجيات الصدفة الآمنة المملوكة التي تم تطويرها بواسطة SSH Communications Security. إن openSSH تم تطويرها كجزء من مشروع OpenBSD الذي كان بقيادة Theo de Raadt.

عادةً ما يتم الخلط بين openSSH و بين OpenSSL, كلا المشروعين لديه هدفه الخاص ولا علاقة له بالمشروع الآخر, لكن تشابه الأسماء يشير فقط الى التشابه في الهدف الذي هو توفير بدلا مفتوح المصدر عن البرمجيات المملوكة.

### Installing OpenSSH

قم بتنصيب حزمة OpenSSH من المستودعات الرسمية

### تهيئة إعدادات ssh

#### العميل

إن ملفي الإعدادات الخاصين بعميل ssh هما `/etc/ssh/ssh_config` أو `~/.ssh/config`.

مثال عن ملف الإعدادت :

 `/etc/ssh/ssh_config` 
```
#	$OpenBSD: ssh_config,v 1.26 2010/01/11 01:39:46 dtucker Exp $

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

# Host *
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
#   ProxyCommand ssh -q -W %h:%p gateway.example.com

```

من المُفضل تغيير السطر الخاص بنوع البروتوكول الى السطر التالي :

```
Protocol 2

```

هذا يعني أن البروتوكول 2 سيتم إستخدامه فقط، لأن البروتوكول 1 يتم إعتباره غير آمنة بالمقارنة من البروتوكول 2.

#### خدمة ssh

يمكن الحصول وتعديل على إعدادات خدمة ssh في الملف `/etc/ssh/ssh**d**_config`.

مثال عن ملف الإعدادات :

 `/etc/ssh/sshd_config` 
```
#	$OpenBSD: sshd_config,v 1.82 2010/09/06 17:10:19 naddy Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options change a
# default value.

#Port 22
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::

# The default requires explicit activation of protocol 1
#Protocol 2

# HostKey for protocol version 1
#HostKey /etc/ssh/ssh_host_key
# HostKeys for protocol version 2
#HostKey /etc/ssh/ssh_host_rsa_key
#HostKey /etc/ssh/ssh_host_dsa_key
#HostKey /etc/ssh/ssh_host_ecdsa_key

# Lifetime and size of ephemeral version 1 server key
#KeyRegenerationInterval 1h
#ServerKeyBits 1024

# Logging
# obsoletes QuietMode and FascistLogging
#SyslogFacility AUTH
#LogLevel INFO

# Authentication:

#LoginGraceTime 2m
#PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10

#RSAAuthentication yes
#PubkeyAuthentication yes
#AuthorizedKeysFile	.ssh/authorized_keys

# For this to work you will also need host keys in /etc/ssh/ssh_known_hosts
#RhostsRSAAuthentication no
# similar for protocol version 2
#HostbasedAuthentication no
# Change to yes if you do not trust ~/.ssh/known_hosts for
# RhostsRSAAuthentication and HostbasedAuthentication
#IgnoreUserKnownHosts no
# Don't read the user's ~/.rhosts and ~/.shosts files
#IgnoreRhosts yes

# To disable tunneled clear text passwords, change to no here!
#PasswordAuthentication yes
#PermitEmptyPasswords no

# Change to no to disable s/key passwords
ChallengeResponseAuthentication no

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
# be allowed through the ChallengeResponseAuthentication and
# PasswordAuthentication.  Depending on your PAM configuration,
# PAM authentication via ChallengeResponseAuthentication may bypass
# the setting of "PermitRootLogin without-password".
# If you just want the PAM account and session checks to run without
# PAM authentication, then enable this but set PasswordAuthentication
# and ChallengeResponseAuthentication to 'no'.
UsePAM yes

#AllowAgentForwarding yes
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
#Compression delayed
#ClientAliveInterval 0
#ClientAliveCountMax 3
#UseDNS yes
#PidFile /var/run/sshd.pid
#MaxStartups 10
#PermitTunnel no
#ChrootDirectory none

# no default banner path
#Banner none

# override default of no subsystems
Subsystem	sftp	/usr/lib/ssh/sftp-server

# Example of overriding settings on a per-user basis
#Match User anoncvs
#	X11Forwarding no
#	AllowTcpForwarding no
#	ForceCommand cvs server
```

لكي يتم السماح بالولوج فقط لمُستخدمين مُحددين، قم بإضافة السطر التالي الى ملف الإعدادت :

```
AllowUsers    user1 user2

```

ولإلغاء تفعيل دخول المستخدم الجذر root مباشرةً عبر خدمة ssh، قم بتعديل قمية الخاصية PermitRootLogin الى التالي :

```
PermitRootLogin no

```

ولكي تُضيف رسالة ترحيب، قم بتعديل ملف `/etc/issue` ومن ثم قم بتعديل السطر الخاص بالقيمة Banner الى التالي :

```
Banner /etc/issue

```

{{تلميح : لربما تريد تغيير المنفذ الإفتراضي من 22 الى رقم منفذ أعلى منه (يُمكنك الرجوع الى المقال security through obscurity) (راجع [security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity")).}}

وعلى الرغم من أن منفذ ssh يُمكن الكشف عنه بسهولةبإحدى أدوات المسح الخاصة بالشبكات nmap، لكن تغييره سيُفيد بتقليل عدد محاولات الدخول المؤتمتة، للمساعدة في إختيار رقم منفذ مناسب قم بمراجعة المقال التالي [list of TCP and UDP port numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers "wikipedia:List of TCP and UDP port numbers").

**Tip:** إلغاء تفعيل الدخول عن طريق كلمات المرور ستُزيد بشكل كبير من الأمان راجع مقال [SSH keys](/index.php/SSH_keys "SSH keys") لمزيد من المعلومات.

### إدارة خدمة ssh

يمكن بدء خدمة ssh بإستخدام التعلمية التالية :

```
# systemctl start sshd

```

ويمكن تفعيل تشغيل خدمة ssh عند بدء تشغيل النظام بواسطة التعليمة التالية : # systemctl enable sshd.service

**تحذير:** إن Systemd هو غير متزامن في بدء العمليات، لذا فإذا قُمت بتحديد خدمة ssh الى عنوان ip مُحدد ListenAddress 192.168.1.100، فيمكن أن تفشل في البدء أثناء الإقلاع، يُمكن حل هذه المشكلة بإضافة After=network.target الى ملف الواحدة المُخصص، قم بمراجعة [Systemd#Replacing provided unit files](/index.php/Systemd#Replacing_provided_unit_files "Systemd").

أو أن تقوم ببدء تشغيل خدمة ssh عند أول إتصال تتلقاه :

```
# systemctl enable sshd.socket

```

إذا كنت تستخدم منفذ غير منفذ 22 الإفتراضي، عليك وضع القيمة "ListenStream" في ملف الوحدة

```
  في ملف /etc/systemd/system/sshd.socket قم بتغيير القيمة "ListenStream" الى المنفذ المناسب.

```

### الإتصال بالخادم

لكي تقوم بالإتصال بالخادم قم بتنفيذ التعليمة التالية :

```
$ ssh -p port user@server-address

```

## عملاء و خوادم ssh الاخرى

بعيدًا عن OpenSSH؛ يوجد هناك العديد من عملاء و خوادم ssh متاحة للإستخدام [clients](https://en.wikipedia.org/wiki/Comparison_of_SSH_clients "wikipedia:Comparison of SSH clients") و [servers](https://en.wikipedia.org/wiki/Comparison_of_SSH_servers "wikipedia:Comparison of SSH servers").

### Dropbear

[Dropbear](https://en.wikipedia.org/wiki/Dropbear_(software) هو خادم وعميل ssh-2\. حزمة [dropbear](https://www.archlinux.org/packages/?name=dropbear) متوفرة في [AUR](/index.php/AUR "AUR").

إن عميل ssh الخاص بموجه الأوامر يُسمى dbclient.

### Mosh بديل SSH

الجملة التالية مقتبسة من موقع [mosh](http://mosh.mit.edu/): تطبيق يسمح بالإتصال عبر طرفية بعيدة, يدعم الإتصالات المتقطعة, ويقدم طريقة ذكية للتعديل السطري لكتابات المستخدم. Mosh هو بديل لخدمة ssh. هو أكثر قوة وإستجابة وخصوصًا عبر شبكات Wi-Fi, cellular و الشبكات بعيدة المدى.

يمكنك تنصيب [mosh](https://www.archlinux.org/packages/?name=mosh) من المستودعات الرسمية، أو آخر نسخة [mosh-git](https://aur.archlinux.org/packages/mosh-git/) من [AUR](/index.php/AUR "AUR").

## تلمحيات

### انبوب SOCKS مُشفر

هذه التلميحة مُفيدة جدًا لمستخدمي الحواسيب المُحمولة الذين يتصلون بشبكات WiFi غير آمنة. الشيء الوحيد الذي ستحتاج إليه هو خادم ssh يعمل في مكان آمن (العمل أو المنزل). من المفيد إستخدام خدمة DNS ديناميكية :[DynDNS](http://www.dyndns.org/) كمثال، لذا فلن تحتاج الى تذكر عنوان IP الخاص بك.

#### الخطوة الولى : قم ببدء الإتصال

عليك فقط تنفيذ التعليمة التالية لكي تقوم ببدء الإتصال بخادم ssh : $ ssh -TND 4711 user@host حيث `"user"` هو اسم المستخدم الخاص بك على الخادم `"host"`، سوف يتم سؤالك عن كلمة المرور الخاصة بك. بعد ذلك تكون قد قمت بالإتصال بنجاح. الراية `"N"` fتقوم بإلغاء تفعيل موجه الأوامر التفاعلي بينما الراية D تقوم بتحديد منفذ محلي يمكنك الإتصال منه (تستطيع إختيار أي رقم تريده). الراية `"T"` تقوم بإلغاء تفعيل حصة pseudo-tty.

من المفيد استخدام الراية `"-v"` لأنها تسمح لك من التأكد من أن عملية الإتصال تمت بنجاح من المخرجات.

#### الخطوة الثانية : إعداد المتصفح (أو بقية البرامج)

الخطوة السابقة عديمة الجدوى تمامًا إن لم تقترن بالإعداد الصحيح لمتصفح الويب -أو أي برنامج آخر- لإستخدام انبوب socks الذي قمنا بإنشاءه. وبما أن النسخة الحالية من ssh تدعم SOCKS4 و SOCKS5 فيمكنك إستخدام أي منهما.

لإعداد متصفح firefox : في البداية قم بالدخول الى Edit → Preferences → Advanced → Network → Connection → Setting : قم بتحديد الخيار "Manual proxy configuration" وقم بإدخال القيمة "localhost" في مربع النص المُعنون "SOCKS host" ومن ثم قم بإدخال رقم المنفذ الذي قمت بتحديده في الخطوة السابقة (تم إستخدام 4711)

متصفح firefox لا يقوم بشكل تلقائي بعمل طلبات DNS عبر انبوب socks، هذا الأمر قد يُعرض خصوصيتك للخر لذا قم بعمل الخطوات التالية :

- قم بطلب الصفحة about:config في شريط العنوان الخاص بمتصفح firefox - ابحث عن الراية network.proxy.socks_remote_dns - قم بتحديد true كقيمة لهذه الراية - قم بإعادة تشغيل المتصفح

وأما مُتصفح Chromium فيمكنك تحديد إعدادات socks كمتغيرات خاصة بالبيئة أو بإستخدامها كوسيط في سطر الأوامر، أنا أفضل إضافة إحدى الدالتين الى ملف `.bashrc` الخاص بك :

```
function secure_chromium {
    port=4711
    export SOCKS_SERVER=localhost:$port
    export SOCKS_VERSION=5
    chromium &
    exit
}

```

أو

```
function secure_chromium {
    port=4711
    chromium --proxy-server="socks://localhost:$port" &
    exit
}

```

الآن قم بفتح نافذة الطرفية و نفذ الأمر التالي :

```
$ secure_chromium

```

### تمرير X11

إذا أردت تشغيل برمجيات رسومية عبرإتصال ssh، يتوجب عليك تفعيل خيار تمرير X11 في ملفات الإعدادات في الخادم و العميل (هنا "العميل" هو الجهاز الذي يعمل عليه خادم X11 و يقوم بالإتصال بخدمات X11 من جهاز "الخادم").

قم بتنصيب الحزمة [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth) من المستودعات الرسمية الى الخادم

قم بتفعيل الخيار AllowTcpForwarding في ملف `ssh**d**_config` على الخادم قم بتفعيل الخيار X11Forwarding في ملف `ssh**d**_config` على الخادم قم بتحديد قيمة الخيار X11DisplayOffset في ملف `ssh**d**_config` على الخادم الى الرقم 10 قم بتفعيل الخيار X11UseLocalhost في ملف `ssh**d**_config` على الخادم يتوجب عليك أيضًا : تفعيل الخيار X11UseLocalhost في ملف `ssh_config` على العميل قم بتفعيل الخيار ForwardX11Trusted إذا وجدت مشاكل في الواجهة الرسومية

بالطبع يتوجب عليك إعادة تشغيل خدمة ssh في الخادم لكي يتم تطبيق الإعدادت السابقة .

عندما تقوم بإتسخدام تمرير X11 قم بتنفيذ الأمر التالي في الطرفية

```
$ ssh -X -p port user@server-address

```

إذا واجهت مشكل في تشغيل البرمجيات الرسومية قم بعمل تمرير موثوق مستخدمًا الأمر التالي :

```
$ ssh -Y -p port user@server-address

```

الآن عندما تقوم بتشغيل البرمجيات الرسومية على الخادم، فسيتم تمرير المخرجات الى جهازك المحلي.

```
$ xclock

```

إذا واجهت أخطاء من قبيل "Cannot open display"، قم بتطبيق التعليمة التالية كمستخدم غير مدير للنظام :

```
$ xhost +

```

التعليمة السابقة تقوم بالسماح بتمرير تطبيقات X11 للجميع، إذا أردت حصر ذلك بجهاز معين قم بإستخدام التعليمة التالية :

```
$ xhost +hostname

```

حيث hostname هو اسم الجهاز الذي تريد تمرير إتصالات X11 له. يمكنك الرجوع الى "man xhost" لمزيد من المعلومات عن إستخدام هذا التعليمة.

كن حذرًا مع بعض البرامج التي تتحقق من بيئة العمل المُستخدمة على الجهاز المحلي، مثال عليها برنامج firefox. فيمكنك إغلاق برنامج firefox أو عن طريق تشغيل firefox مفعلًا الخيار -no-remote :

```
$ firefox -no-remote

```

إذا ظهرت لك رسالة الخطأ التالية "X11 forwarding request failed on channel 0" فقم بإحدى الخطوتين التاليتين :

*   قم بتفعيل خيار**AddressFamily any** في ملف `ssh**d**_config` على الخادم.
*   قم بتحديد قيمة الخيار **AddressFamily** في ملف `ssh**d**_config` على الخادم الى inet.

تحديد القيمة inet للخيار AddressFamily يحّل المشاكل مع عملاء ubuntu الذين يستخدمون IPv4.

### تمرير المنافذ الاخرى

بالإضافة الى خاصية تمرير X11 المدمجة مع ssh، يمكنك إنشاء نفق آمن لأي من إتصالات TCP، وذلك بإستخدام تمرير محلي أو عن بُعد. التمرير المحلي يقوم بفتح منفذ في الجهاز المحلي، الإتصالات سيتم تمريرها الى الخادم البعيد ومن ثم من هناك ستصل الى وجهتها. Very often, the forwarding destination will be the same as the remote host, thus providing a secure shell and, e.g. a secure VNC connection, to the same machine. Local forwarding is accomplished by means of the `-L` switch and it's accompanying forwarding specification in the form of `<tunnel port>:<destination address>:<destination port>`.

Thus:

```
$ ssh -L 1000:mail.google.com:25 192.168.0.100

```

will use SSH to login to and open a shell on 192.168.0.100, and will also create a tunnel from the local machine's TCP port 1000 to mail.google.com on port 25\. Once established, connections to localhost:1000 will connect to the Gmail SMTP port. To Google, it will appear that any such connection (though not necessarily the data conveyed over the connection) originated from 192.168.0.100, and such data will be secure as between the local machine and 192.168.0.100, but not between 192.168.0.100, unless other measures are taken.

Similarly:

```
$ ssh -L 2000:192.168.0.100:6001 192.168.0.100

```

will allow connections to localhost:2000 which will be transparently sent to the remote host on port 6001\. The preceding example is useful for VNC connections using the vncserver utility--part of the tightvnc package--which, though very useful, is explicit about its lack of security.

Remote forwarding allows the remote host to connect to an arbitrary host via the SSH tunnel and the local machine, providing a functional reversal of local forwarding, and is useful for situations where, e.g., the remote host has limited connectivity due to firewalling. It is enabled with the `-R` switch and a forwarding specification in the form of `<tunnel port>:<destination address>:<destination port>`.

Thus:

```
$ ssh -R 3000:irc.freenode.net:6667 192.168.0.200

```

will bring up a shell on 192.168.0.200, and connections from 192.168.0.200 to itself on port 3000 (remotely speaking, localhost:3000) will be sent over the tunnel to the local machine and then on to irc.freenode.net on port 6667, thus, in this example, allowing the use of IRC programs on the remote host to be used, even if port 6667 would normally be blocked to it.

Both local and remote forwarding can be used to provide a secure "gateway," allowing other computers to take advantage of an SSH tunnel, without actually running SSH or the SSH daemon by providing a bind-address for the start of the tunnel as part of the forwarding specification, e.g. `<tunnel address>:<tunnel port>:<destination address>:<destination port>`. The `<tunnel address>` can be any address on the machine at the start of the tunnel, `localhost`, `*` (or blank), which, respectively, allow connections via the given address, via the loopback interface, or via any interface. By default, forwarding is limited to connections from the machine at the "beginning" of the tunnel, i.e. the `<tunnel address>` is set to `localhost`. Local forwarding requires no additional configuration, however remote forwarding is limited by the remote server's SSH daemon configuration. See the `GatewayPorts` option in `sshd_config(5)` for more information.

### تسريع ssh

يُمكنك جعل جميع الجلسات الى الخادم نفسه تستخدم إتصالًا واحدًا، هذا يؤدي الى تسريع عملية الولوج، وذلك بإضافة السطور التالية تحت اسم المُضيف المُناسب في ملف `/etc/ssh/ssh_config` :

```
ControlMaster auto
ControlPath ~/.ssh/socket-%r@%h:%p

```

تغيير خوارزمية التشفير المُستخدمة من قبل ssh تُساعد بشكل كبير على تحسين السرعة. في هذا المجال أفصل الخيارات هي arcfour و blowfish-cbc، رجاءً لا تقم بتغييرها إلا إذا كنت تعلم ما تفعله، لخوارزمية arcfour عدد من الجوانب الضعيفة. لإستخدمهم قم بتنفيذ التعليمة التالية :

```
$ ssh -c arcfour,blowfish-cbc user@server-address

```

لإستخدامها بشكل دائم، ضع هذا السطر تحت اسم المضيف المناسب في ملف `/etc/ssh/ssh_config`:

```
Ciphers arcfour,blowfish-cbc

```

خيار آخر لكي تُحسن من سرعة SSH هو تفعيل خيار الضغط بإستخدام راية `"C"`. ولتفعيل هذه الميزة دومًا قم بإضافة السطر التالي تحت اسم المُضيف المُناسب في ملف `/etc/ssh/ssh_config`:

```
Compression yes

```

الوقت الآزم لتسجيل الدخول يُمكن أن يُقلل بإستخدام الراية `"4"`، التي تقوم بتجاوز البحث ببروتوكول IPv6\. يُمكن تفعيل هذه الميزة بشكل دائم عن طريق إضافة السطر التالي تحت اسم المُضيف المناسب في ملف `/etc/ssh/ssh_config`:

```
AddressFamily inet

```

طريقة اخرى لتفعيل هذه الخيارات بشكل دائم هي إنشاء مكافئ في ملف `~/.bashrc`:

```
alias ssh='ssh -C4c arcfour,blowfish-cbc'

```

### وصل نظام ملفات خاص بحاسب بعيد عن طريق sshfs

يرجى الرجوع الى مقال [SSHFS](/index.php/SSHFS "SSHFS") لمعرفة المزيد حول وصل نظام الملفات خاص بحاسب بعيد -قابل للوصول عبر ssh- الى مجلد محلي. يمكنك القيام بأي تعليمة وبأي أداة على الملفات الموصولة (نسخ، إعداة تسمية، تعديل بمُحرر vim...الخ). استخدم sshfs عوضًا عن shfs (لم يتم إصدار نسخة جديدة منه منذ 2004 !).

### إبقاء الإتصال مفتوحًا

جلسة ssh الخاصة بك سوف تقوم بتسجيل الخروج عندما لا يتم إستخدمها، لإبقاء الإتصال مفتوحًا قم بإضافة السطر التالي لأحد الملفين `~/.ssh/config` أو `/etc/ssh/ssh_config` في جهاز العميل :

```
ServerAliveInterval 120

```

السطر السابق يقوم بإرسال إشارة "keep alive" كل 120 ثانية.

وبشكل آخر يمكن إبقاء الإتصالات مفتوحة عن طريق تعيين القيمة 120 أو أي رقم آخر أكبر من 0 في ملف `/etc/ssh/sshd_config` على الخادم، كالتالي :

```
ClientAliveInterval 120

```

### حفظ بيانات الإتصال في ملف إعدادات ssh

عندما تقوم بالولوج الى خادم ssh، فإنك ستقوم بإدخال اسم المستخدم وعنوان الخادم على الأقل. إذا أردت توقير هذا الوقت; يمكنك استخدام الملف `$HOME/.ssh/config` الخاص بك، أو الملف العام `/etc/ssh/ssh_config` كما في المثال التالي :

 `$HOME/.ssh/config` 
```
Host myserver
    HostName 123.123.123.123
    Port 12345
    User bob
Host other_server
    HostName test.something.org
    User alice
    CheckHostIP no
    Cipher blowfish

```

الآن يمكنك الإتصال بالخادم عن طريق الأمر التالي :

```
$ ssh myserver

```

للإطلاع على القائمة الكاملة للخيارات التي تستطيع إستخدمها يمكنك الرجوع الى صفحة الدليل الخاصة بـ ssh_config أو مقال[ssh_config documentation](http://www.openbsd.org/cgi-bin/man.cgi?query=ssh_config) الموجود في الموقع الرسمي.

### إعادة تشغيل جلسات و انفاق ssh تلقائيًا - Autossh

عندما يتعذر إبقاء جلسة أو نفق ssh مفتوحًا (على سبيل المثال أوضاع الشبكة سيئة تؤدي الى إنقطاع الإتصال بخادم ssh...)، يمكنك إستخدام الحزمة Autossh لإعادة الإتصال تلقائيًاـ حزمة Autossh يمكن تنصيبها من المستودعات الرسمية.

أمثلة عن طرق الإستخدام :

```
$ autossh -M 0 -o "ServerAliveInterval 45" -o "ServerAliveCountMax 2" username@example.com

```

مدمجة مع خدمة [SSHFS](/index.php/SSHFS "SSHFS"):

```
$ sshfs -o reconnect,compression=yes,transform_symlinks,ServerAliveInterval=45,ServerAliveCountMax=2,ssh_command='autossh -M 0' username@example.com: /mnt/example 

```

الإتصال بواسطة وسيط SOCKS :

```
$ autossh -M 0 "ServerAliveInterval 45" -o "ServerAliveCountMax 2" -NCD 8080 username@example.com 

```

عند إستخدام الخيار -f، Autossh سيتم تشغيله كعملية في الخلفية، تشغيله بهذه الطريقة يعني أنظ لا تستطيع إدخال معلومات الإتصال بشكل تفاعلي. سيتم إنهاء الجلسة فقط عندما تتم كتابة exit أو عندما تتلقى Autossh إشارة SIGTERM, SIGINT , SIGKILL

إذا أردت تشغيل autossh تلقائيًا، يُمكنك وبسهولة استخدام systemd، فعلى سبيل المثال يُمكنك إنشاء ملف واحدة خاص بخدمة systemd على الشكل التالي :

```
[Unit]
Description=AutoSSH service for port 2222
After=network.target

[Service]
ExecStart=/usr/bin/autossh -M 0 2222:localhost:2222 foo@bar.com

```

ومن ثم قم بوضعها في ملف -وعلى سبيل المثال- /etc/systemd/system/system/autossh.service، بالطبع يُمكنك إنشاء ملف واحدة أكثر تعقيدًا إذا كان ذلك ضروريًا (يُمكنك الرجوع الى التوثيق الخاص بخدمة systemd لمزيد من التفاصيل)، وبكل تأكيد يُمكنك إستخدام الخيارات الخاصة بك في autossh.

ومن ثم قم بتفعيل أنفاق autossh كالتالي :

```
$ systemctl start autossh

```

(أو حسب ما قمُت بتسمية ملف الواحدة)

من المُمكن أيضًا التعامل مع عدة عمليات autossh سويًا، وذلك لإبقاء الإتصال مفتوحًا في عدة أنفاق. عليك فقط إنشاء ملفات .service متعددة ذات أسماء مُختلفة.

## إستكشاف الأخطاء وإصلاحها

### الإتصالات تُرفض أو تنتهي مدتها

#### هل الراوتر لديك يقوم بتمرير المنافذ؟

قم بتجاوز هذه الخطوة إذا كنت خلف NAT modem/router. (على سبيل المثال VPS أو غيره). أغلب المنازل أو الشركات الصغيرة يكون لديها NAT modem/router.

أو شيئ يجب التحقق منه هو أن الراوتر لديك يقوم بتمرير إتصالات ssh القادمة الى جهازك المحلي. عنوان IP الخارجي الذي تم إعطاؤه لك من قبل مزود خدمة الإنترنت، وهو نفس العنوان الذي يتم ربطه مع الطلبات الخاجية من قبل الراوتر لديك. لذا يجب على الراوتر أن يعلم أن إتصالات SSH القادمة يجب أن يتم تمريرها الى خدمة sshd في جهازك المحلي.

قم بمعرفة عنوان ip الخاص بجهازك في الشبكة المحلية :

```
ip a

```

قم بالبحث عن الحقل الخاص بقيمة inet. ومن ثم قم بالدخول الى لوحة الإعدادات الخاصة بالراوتر لديك مُستخدمًا عنوان IP الخاص به. قم بإخبار الراوتر لديك بأن يقوم بتمرير الإتصالات الى عنوان inet IP قم بزيارة موقع [[1]](http://portforward.com/) لمزيد من المعلومات حول كيفية تمرير المنافذ في الراوتر الخاص بك.

#### هل خدمة ssh تعمل؟

```
$ ss -tnlp

```

إذا لم تُظهر التعليمة السابقة أن منفذ ssh مفتوح فإن خدمة ssh لا تعمل، قم بالتحقق من ملف `/var/log/messages` للحصول على الأخطاء.

#### هل يقوم الجدار الناري الخاص بك بحجب الإتصالات ؟

Flush your iptables rules to make sure they are not interfering:

```
# rc.d stop iptables

```

أو:

```
# iptables -P INPUT ACCEPT
# iptables -P OUTPUT ACCEPT
# iptables -F INPUT
# iptables -F OUTPUT

```

#### هل يصل الإتصال أساسًا الى جهازك؟

قم بعمل traffic dump في الجهاز الذي تواجه فيه المشاكل بإستخدام التعليمة التالية:

```
# tcpdump -lnn -i any port ssh and tcp-syn

```

سيتم إظهار بعض المعلومات البسيطة، الآن قم بتجربة الإتصال. إذا لم تشاهد أي مخرجات خلال عملية الإتصال, فهذا يعني أن شيئاً ما خارج جهازك يمنع الإتصال (على بسيل المثال : جدار ناري خارجي أو NAT راوتر).

#### هل يقوم مزود الخدمة الخاص بك أو أي جهة اخرى بحجب المنفذ الإفتراضي ؟

**Note:** قم بتجريب الخطوة التالية فقط إذا كنت **متأكدًا** من أنك لا تستخدم أي جدار ناري وقمت بإعداد الراوتر لديك إعدادًا صحيحًا وذلك بتمرير المنفذ الى جهازك المحلي.

في بعض الحالات، يقوم مزود الخدمة الخاص بك بحجب المنفذ الإفتراضي 22 لذا مهما حاولت من طرق فهي لن تُجدي نفعًا.

إذا واجهتك رسالة شبيهة بالرسالة التالية :

```
ssh: connect to host www.inet.hr port 22: Connection refused

```

فهذا لا يعني أن المنفذ قم تم حجبه من قبل مزود الخدمة، بل أن الخادم لا يُشغل خدمة SSH على هذا المنفذ(راجع [security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity")).

أما إذا واجهت رسالة كالرسالة التالية :

```
ssh: connect to host 111.222.333.444 port 22: Operation timed out 

```

هذا يعني أن هنالك شيئ يمنع إتصال TCP على المنفذ 22\. إذا كنت متأكدًا تمامًا من الإعداد الصحيح للجدار الناري و/أو الراوتر، فإن ذلك يعني أن المنفذ محجوب من قبل مزود الخدمة. لزيادة التحقق، قم بتشغيل Wireshark على الخادم وقم بمراقبة المرور على المنفذ 22\. بعد إعداده أن لم تحصل على أي مخرجات بينما تحاول الإتصال فهذا يعني ان جهة خارجية تقوم بحجب الإتصال.

##### التحقق بإستخدام Wireshark

قم بتنصيب Wireshark عن طريق الحزمة [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli)، الموجودة في المستودعات الرسمية.

ومن ثم قم بتشغيلها مُستخدمًا التعليمة التالية:

```
tshark -f "tcp port 22" -i NET_IF

```

حيث NET_IF هو واجهة الشبكة لإتصال WAN. إذا لم تتلقى أي حزم إتصال عندما تحاول الإتصال عن بعد، فيمكنك التاكد تمامًا أن مزود الخدمة لديك يحجب المنفذ 22.

##### حل هذه المشكلة

الحل هو إستخدام منفذ آخر لا يقوم مزود الخدمة لديك بحجبه. قم بفتح ملف `/etc/ssh/sshd_config` وضبط الإعدادات فيه لإستخدام منفذ آخر. على سبيل المثال قم بإضاة التالي :

```
Port 22
Port 1234

```

أيضًا تاكد من أن الأسطر التي يوجد فيها إعدادت بقية المنافذ. عند إضافة "Port 1234" وحذف "Port 22" سيجعل خدمة sshd تقبل الإتصالات من المنفذ 1234 فقط. لذا قم بإستخدام كلا المنفذين.

قم بإعادة تشغيل الخدمة عن طريق الأمر `systemctl restart sshd.service`. ولم يبقى عليك سوى إعداد العميل لديك ليستخدم المنفذ الجديد بدلًا من المنفذ الإفتراضي.

#### مشكلة Read from socket failed: connection reset by peer

الإصدارات التي اطلقت مؤخرًا من openssh تفشل في بعض الأحيان مخرجةً رسالة خطأ كالرسالة السابقة بسبب وجود علّة في خاصية التشفير فيها. في هذه الحالة قم بإضافة السطر التالي الى ملف `~/.ssh/config`:

```
HostKeyAlgorithms ssh-rsa-cert-v01@openssh.com,ssh-dss-cert-v01@openssh.com,ssh-rsa-cert-v00@openssh.com,ssh-dss-cert-v00@openssh.com,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,ssh-rsa,ssh-dss

```

في إصدار openssh 5.9 السطر السابق لا يقوم بحل المشكلة. لذا قم بوضع السطور التالية في ملف `~/.ssh/config`:

```
Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc 
MACs hmac-md5,hmac-sha1,hmac-ripemd160

```

راجع أيضًا [discussion](http://www.gossamer-threads.com/lists/openssh/dev/51339) في مركز علل openssh

### "[الصدفة التي تستخدمها]: No such file or directory"

مسبب من مسببات هذه المشكلة هو أن بعض عملاء SSH يحتاجون الى معرفة المسار المطلق عن طريق الأمر `whereis -b [your shell]`، وحتى لوكان الملف التنفيئي للصدفة موجود في `$PATH`. سبب آخر هو أن المستخدم ليس عضوًا في مجموعة *network*.

### ظهور رسالة الخطأ "Terminal unknown" أو "Error opening terminal"

من الممكن عند إستخدام ssh الحصول على أخطاء من من قبيل "Terminal unknown" عندما تحاول تسجيل الدخول. بدء بعض التطبيقات كتطبيق nano يفشل مُظهرًا الرسالة "Error opening terminal". يوجد طريقتين لحل المشاكل من هذا النوع، الطريقة السلهة هي إستخدام المُتغير $TERM، أو باستخدام ملف terminfo.

#### الحل بواسطة المتغير $TERM

بعد الإتصال الى الخادم، قم بتحديد قيمة المتغير $TERM الى "xterm" مُستخدمًا التعليمة التالية :

```
`TERM=xterm`

```

هذا الحل يحوي على بعض المشاكل الجانبية. ويتوجب عليك أيضًا أن تقوم بتكرار هذه التعليمة كل مرة تقوم فيها بتسجيل الدخول الى الخادم. أو بشكل بديل يمكنك وضعها في ملف ~.bashrc .

#### الحل بإستخدام ملف terminfo

حل آخر هو نقل ملف terminfo من جهازك المحلي الى الخادم. في هذا المثال سنقوم بشرح كيفية تهيئة ملف terminfo من أجل طرفية من نوع "rxvt-unicode-256color". قم بإنشاء مجلد يحوي على ملفات terminfo في خادم ssh، عندما تقوم بتسجيل الدخول الى الخادم قم بإستخدام هذه التعليمة :

```
 `mkdir -p ~/.terminfo/r/`

```

الآن قم بنسخ ملف terminfo الخاص بالطرفيتك الى المجلد الجديد. مُستبدلًا *"rxvt-unicode-256color"* بالطرفية الخاصة بك في التعليمة التالية و *ssh-server* بإسم المستخدم وعنوان الخادم الخاصين بك

```
`$ scp  /usr/share/terminfo/r/*rxvt-unicode-256color* ssh-server:~/.terminfo/r/`

```

بعدما تقوم بتسجيل الخروج ومن ثم تسجيل الدخول مُجددًا، تكون المشكلة قد حُلّت.

## شاهد أيضًا

*   [SSH keys](/index.php/SSH_keys "SSH keys")
*   [pam_abl](/index.php/Pam_abl "Pam abl")
*   [fail2ban](/index.php/Fail2ban "Fail2ban")
*   [sshguard](/index.php/Sshguard "Sshguard")
*   [SSHFS](/index.php/SSHFS "SSHFS")
*   [Syslog-ng](/index.php/Syslog-ng "Syslog-ng") : لإرسال log الخاص بـ ssh الى ملف

## Links & references

*   [A Cure for the Common SSH Login Attack](http://www.soloport.com/iptables.html)
*   [Defending against brute force ssh attacks](http://www.la-samhna.de/library/brutessh.html)
*   [OpenSSH key management, Part 1](http://www.ibm.com/developerworks/library/l-keyc/index.html) and [Part 2](http://www.ibm.com/developerworks/library/l-keyc2) on IBM developerWorks