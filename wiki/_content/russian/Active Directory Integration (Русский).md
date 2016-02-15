**Warning:** Так как Arch Linux использует систему распространения rolling release,возможно,некоторая информация на странице может быть устаревшей из-за изменений в пакетах или конфигурациях,сделанных разработчиками. Никогда слепо не следуйте этой или любой другой инструкции. Когда в инструкции сказано изменить какой-либо файл, обязательно сделайте бэкап. Проверяйте дату последней проверки статьи.

Основной задачей системных администраторов являются попытки совместного изпользования разнообразных окружений. Мы имеем в виду смешивание разных серверных операционных систем (Обычно Microsoft Windows & Unix/Linux). Управление пользователями и аутентификацией на данный момент является наиболее сложной задачей. Популярнейший способ решения это задачи - Directory Server. Существует много открытых и коммерческих решений для разный типов *NIX; однако, только немногие решают проблему взаимодействия с Windows. Активный Каталог (AD) - служба каталогов созданная Microsoft для доменных сетей Windows. Он входит в большинство операционных систем Windows Server. Сервера,на которых запущен AD, называются контроллерами доменов(domain controllers)

[Активный каталог](https://en.wikipedia.org/wiki/Active_Directory "wikipedia:Active Directory") используется как главное средство администрирования сети и безопасности.Он отвечает за аутентификацию и авторизацию все пользователей и компьютеров в доменной сети Windows, назначая и следя за правилами безопасности для всех компьютеров в сети, также устанавливая и обновляя ПО на компьютерах в этой сети. Например,когда пользователь авторизуется в компьютер,который является частью доменной сети, AD проверяет его пароль и яляется он обычным пользователем или же системным администратором.

Активный католог использует [Lightweight Directory Access Protocol (LDAP)](https://en.wikipedia.org/wiki/Ldap "wikipedia:Ldap") версий 2 и 3, [Kerberos](https://en.wikipedia.org/wiki/Kerberos_(protocol) "wikipedia:Kerberos (protocol)") и DNS. Эти же стандарты доступны в Linux, но их комбинирование - непростая задача. Эта статья поможет вам настроить хост ArchLinux для аутентификация в домене AD.

Эта статья объясняет, как интегрировать хост Arch Linux в сущестующий домен AD. Перед продолжением у вас должен быть существующий домен AD, и пользователь с правами на добавление пользователей и компьютерных аккаунтов. Эта сатья не предназначена ни как полное описание AD,ни как полно описание работы с Samba. Обратитесь к разделу ресурсов для дополнительной информации.

## Contents

*   [1 Терминология](#.D0.A2.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.BE.D0.BB.D0.BE.D0.B3.D0.B8.D1.8F)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Настройка AD](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_AD)
        *   [2.1.1 Обновление GPO](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_GPO)
    *   [2.2 Настройка Linux хоста](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Linux_.D1.85.D0.BE.D1.81.D1.82.D0.B0)
    *   [2.3 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [2.4 Обновление DNS](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_DNS)
    *   [2.5 Настройка NTP](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_NTP)
    *   [2.6 Kerberos](#Kerberos)
        *   [2.6.1 Создание ключа Kerberos](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D1.8E.D1.87.D0.B0_Kerberos)
        *   [2.6.2 Подтверждение ключа](#.D0.9F.D0.BE.D0.B4.D1.82.D0.B2.D0.B5.D1.80.D0.B6.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D1.8E.D1.87.D0.B0)
    *   [2.7 pam_winbind.conf](#pam_winbind.conf)
    *   [2.8 Samba](#Samba)
*   [3 Запуск и проверка сервисов](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B8_.D0.BF.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D1.81.D0.B5.D1.80.D0.B2.D0.B8.D1.81.D0.BE.D0.B2)
    *   [3.1 Запуск Samba](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Samba)
    *   [3.2 Присоединение к Домену](#.D0.9F.D1.80.D0.B8.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA_.D0.94.D0.BE.D0.BC.D0.B5.D0.BD.D1.83)
    *   [3.3 Перезапуск Samba](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Samba)
    *   [3.4 Проверка Winbind](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_Winbind)
    *   [3.5 Проверка nsswitch](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_nsswitch)
    *   [3.6 Проверка команд Samba](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4_Samba)
*   [4 Настройка PAM](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_PAM)
    *   [4.1 system-auth](#system-auth)
        *   [4.1.1 Раздел "auth"](#.D0.A0.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB_.22auth.22)
        *   [4.1.2 Раздел "account"](#.D0.A0.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB_.22account.22)
        *   [4.1.3 Раздел "session"](#.D0.A0.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB_.22session.22)
        *   [4.1.4 Раздел "password"](#.D0.A0.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB_.22password.22)
    *   [4.2 Проверка входа](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0)
*   [5 Настройка общих файлов](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BE.D0.B1.D1.89.D0.B8.D1.85_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2)
*   [6 Добавление файла keytab и включение беспарольного входа на машину через Kerber и ssh](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_keytab_.D0.B8_.D0.B2.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B1.D0.B5.D1.81.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.BD.D0.B0_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D1.83_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_Kerber_.D0.B8_ssh)
    *   [6.1 Создание key tab файла](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_key_tab_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0)
    *   [6.2 Включение входа через keytab](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_keytab)
    *   [6.3 Подготовка sshd на сервере](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0_sshd_.D0.BD.D0.B0_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B5)
    *   [6.4 Добавление опций, нужных для клиента](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D0.BF.D1.86.D0.B8.D0.B9.2C_.D0.BD.D1.83.D0.B6.D0.BD.D1.8B.D1.85_.D0.B4.D0.BB.D1.8F_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0)
    *   [6.5 Проверка установки](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [6.6 Настройка для полной аутентификации Kerberos без пароля.](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B4.D0.BB.D1.8F_.D0.BF.D0.BE.D0.BB.D0.BD.D0.BE.D0.B9_.D0.B0.D1.83.D1.82.D0.B5.D0.BD.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8.D0.B8_Kerberos_.D0.B1.D0.B5.D0.B7_.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D1.8F.)
*   [7 Генерирование keytab, которые будет принимать AD](#.D0.93.D0.B5.D0.BD.D0.B5.D1.80.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_keytab.2C_.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D0.B5_.D0.B1.D1.83.D0.B4.D0.B5.D1.82_.D0.BF.D1.80.D0.B8.D0.BD.D0.B8.D0.BC.D0.B0.D1.82.D1.8C_AD)
    *   [7.1 Интересно знать](#.D0.98.D0.BD.D1.82.D0.B5.D1.80.D0.B5.D1.81.D0.BD.D0.BE_.D0.B7.D0.BD.D0.B0.D1.82.D1.8C)
*   [8 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)
    *   [8.1 Коммерческие решения](#.D0.9A.D0.BE.D0.BC.D0.BC.D0.B5.D1.80.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F)

## Терминология

Если вы не знакомы с AD, здесь приведены некоторые ключевые слова, которые будет полезно знать.

*   **Домен(Domain)** : Имя,используемое для группы компьютеров и аккаунтов.
*   **SID** : Каждый компьютер,присоединяющийся к сети должен иметь уникальный SID / Системный идентификатор.
*   **SMB** : Блок сообщения сервера.
*   **NETBIOS**: Network naming protocol used as an alternative to DNS. Mostly legacy, but still used in Windows Networking.
*   **WINS**: Windows Information Naming Service. Used for resolving Netbios names to windows hosts.
*   **Winbind**: Protocol for windows authentication. Протокол для авторизации windows.

## Настройка

### Настройка AD

**Важно:** Эта часть не была проверена, продолжайте с отсторожностью.

#### Обновление GPO

Возможно, нужно будет отключить _Digital Sign Communication (Always)_ в настройках групп AD. А именно:

	`Local policies` -> `Security policies` -> `Microsoft Network Server` -> `Digital sign communication (Always)` -> выбрать `define this policy` и поставить "галочку" на `disable`.

Если вы используете Windows Server 2008 R2, то вам нужно настроить GPO в GPO for Default Domain Controller Policy -> Computer Setting -> Policies -> Windows Setting -> Security Setting -> Local Policies -> Security Option -> _Microsoft network client: Digitally sign communications (always)_

### Настройка Linux хоста

Следующие несколько шагов - начало конфигурации хоста. Вам понадобиться root или sudo доступ.

### Установка

[Установите](/index.php/Pacman "Pacman") следующие пакеты:

*   [samba](https://www.archlinux.org/packages/?name=samba), см. [Samba](/index.php/Samba "Samba")
*   [pam-krb5](https://aur.archlinux.org/packages/pam-krb5/) из [AUR](/index.php/AUR "AUR")
*   [ntp](https://www.archlinux.org/packages/?name=ntp) или [openntpd](https://www.archlinux.org/packages/?name=openntpd), см. также [NTPd](/index.php/NTPd "NTPd") или [OpenNTPD](/index.php/OpenNTPD "OpenNTPD")

### Обновление DNS

AD сильно зависит от DNS. Вам нужно будет обновить `/etc/resolv.conf`, чтобы использовать контроллеры доменов AD:

 `/etc/resolv.conf` 

```
nameserver <IP1>
nameserver <IP2>

```

Замените <IP1> и <IP2> IP адресами для сервера AD.Есили ваши AD домены не позволяют использовать DNS форвардинг или рекурсию,возможно,придётся добавить некоторые вещи. Если ваша машина имеет дуалбут Windows и Linux, стоит использовать разные имена DNS и netbios для linux,если обе операционные системы будут членами одного домена.

### Настройка NTP

См. [NTPd](/index.php/NTPd "NTPd") или [OpenNTPD](/index.php/OpenNTPD "OpenNTPD") для инструкции по настройке NTP. Стоит отметить, что OpenNTPD больше не поддерживается.

При настройке используйте IP адреса серверов AD.Как альтернативу можно использовать другие NTP сервера,которые обеспечат синхронизацию AD в то же место.Тем не менее,AD обычно запускают NTP в качестве службы.

Убедитесь,что демон настроен на **sync automatically on startup**.

### Kerberos

Допустим,что ваша AD называется example.com. Далее допустим что ваша AD управляется двумя доменными контроллерами, главным и вторичным, которые называются PDC и BDS, pdc.example.com и bdc.example.com соответственно. Их адреса будут,например, 192.168.1.2 и 192.168.1.3\. Следите за написанием,верхний регистр очень важен.

 `/etc/krb5.conf` 

```
[libdefaults]
        default_realm 	= 	EXAMPLE.COM
	clockskew 	= 	300
	ticket_lifetime	=	1d
        forwardable     =       true
        proxiable       =       true
        dns_lookup_realm =      true
        dns_lookup_kdc  =       true

[realms]
	EXAMPLE.COM = {
		kdc 	= 	PDC.EXAMPLE.COM
                admin_server = PDC.EXAMPLE.COM
		default_domain = EXAMPLE.COM
	}

[domain_realm]
        .kerberos.server = EXAMPLE.COM
	.example.com = EXAMPLE.COM
	example.com = EXAMPLE.COM
	example	= EXAMPLE.COM

[appdefaults]
	pam = {
	ticket_lifetime 	= 1d
	renew_lifetime 		= 1d
	forwardable 		= true
	proxiable 		= false
	retain_after_close 	= false
	minimum_uid 		= 0
	debug 			= false
	}

[logging]
	default 		= FILE:/var/log/krb5libs.log
	kdc 			= FILE:/var/log/kdc.log
        admin_server            = FILE:/var/log/kadmind.log

```

**Note:** Heimdal 1.3.1 не принимает DES шифрование,которое необходимо для аутентификации AD до Windows Server 2008\. Скорее всего вам придётся добавить `allow_weak_crypto = true` в раздел `[libdefaults]`

#### Создание ключа Kerberos

Теперь во можете запросить ключи для AD (**верхний регистр необходим**):

 `kinit administrator@EXAMPLE.COM` 

Можно использовать любое имя пользователя,у которого есть права администратора домена.

#### Подтверждение ключа

Запустите **klist** чтобы проверить,получили ли вы токен,должно быть нечто подобное:

 `# klist` 

```
 Ticket cache: FILE:/tmp/krb5cc_0
 Default principal: administrator@EXAMPLE.COM

 Valid starting    Expires           Service principal 
 02/04/12 21:27:47 02/05/12 07:27:42 krbtgt/EXAMPLE.COM@EXAMPLE.COM
         renew until 02/05/12 21:27:47

```

### pam_winbind.conf

Если вы получаете ошибки "/etc/security/pam_winbind.conf не найден",создайте этот файл и отредактируйте его следующим образом:

 `/etc/security/pam_winbind.conf` 

```
debug=no
debug_state=no
try_first_pass=yes
krb5_auth=yes
krb5_cache_type=FILE
cached_login=yes
silent=no
mkhomedir=yes

```

### Samba

Samba — бесплатная реализация протокола SMB/CIFS. Также она включает инструменты для Linux машин,которые заставляют их вести себя будто Windows сервера и клиенты.

**Note:** Настройка может разниться в зависимости от конфигурации сервера Windows. Будьте готовы изучать и решать проблемы.

В этом разделе мы сначала сфокусируемся на работе аутентификации с помощью изменения секции 'Global'. Далее, мы вернёмся к остальным.

 `/etc/samba/smb.conf` 

```
[Global]
  netbios name = MYARCHLINUX
  workgroup = EXAMPLE
  realm = EXAMPLE.COM
  server string = %h ArchLinux Host
  security = ads
  encrypt passwords = yes
  password server = pdc.example.com

  idmap config * : backend = rid
  idmap config * : range = 10000-20000

  winbind use default domain = Yes
  winbind enum users = Yes
  winbind enum groups = Yes
  winbind nested groups = Yes
  winbind separator = +
  winbind refresh tickets = yes

  template shell = /bin/bash
  template homedir = /home/%D/%U

  preferred master = no
  dns proxy = no
  wins server = pdc.example.com
  wins proxy = no

  inherit acls = Yes
  map acl inherit = Yes
  acl group control = yes

  load printers = no
  debug level = 3
  use sendfile = no

```

Теперь надо "объяснить" Samba, что мы будет использовать базы даннх PDC для аутенификации.Будем использовать winbindd, который входит в поставку Samba.Winbind указывает UID и GID Linux машины для AD. Winbind использует UNIX реализацию RPC вызовов, Pluggable Authentication Modules (aka PAM) и Name Service Switch (NSS), чтобы разрешить допуск пользователей и Windows AD на Linux-машинах. Лучшая часть winbindd то,что вам не нужно размечать самому, от вас требуется только указать диапазон UID и GID! Именно их мы объявили в smb.conf.

Обновите файл настроек samba чтобы включить демона winbind

 `/etc/conf.d/samba` 

```
 ##### /etc/conf.d/samba #####
 #SAMBA_DAEMONS=(smbd nmbd)
 SAMBA_DAEMONS=(smbd nmbd winbindd)

```

Далее, настройте `samba` так, для запуска вместе со стартом системы. См. [Daemons](/index.php/Daemons "Daemons") для подробностей.

## Запуск и проверка сервисов

### Запуск Samba

Надеемся,вы ещё не перезагрузились! Хорошо. Если у вас запущена X-сессия - выходите из неё,чтобы проверить вход в другой терминал не выходя из своей сессии.

[Запуск](/index.php/Daemons "Daemons") Samba (включая smbd, nmbd и winbindd):

Если вы проверите список процессов,то заметите,что на самом деле winbind не запустился. Быстрый осмотр логов говорит,что SID для этого хоста может быть получен от домена:

 `# tail /var/log/samba/log.winbindd` 

```
[2012/02/05 21:51:30.085574,  0] winbindd/winbindd_cache.c:3147(initialize_winbindd_cache)
  initialize_winbindd_cache: clearing cache and re-creating with version number 2
[2012/02/05 21:51:30.086137,  2] winbindd/winbindd_util.c:233(add_trusted_domain)
  Added domain BUILTIN  S-1-5-32
[2012/02/05 21:51:30.086223,  2] winbindd/winbindd_util.c:233(add_trusted_domain)
  Added domain MYARCHLINUX  S-1-5-21-3777857242-3272519233-2385508432
[2012/02/05 21:51:30.086254,  0] winbindd/winbindd_util.c:635(init_domain_list)
  Could not fetch our SID - did we join?
[2012/02/05 21:51:30.086408,  0] winbindd/winbindd.c:1105(winbindd_register_handlers)
  unable to initialize domain list

```

### Присоединение к Домену

Вам нужен аккаунт администратора AD чтобы сделать это. Пусть наш логин: Administrator. Комана - 'net ads join'

 `# net ads join -U Administrator` 

```
Administrator's password: xxx
Using short domain name -- EXAMPLE
Joined 'MYARCHLINUX' to realm 'EXAMPLE.COM'

```

### Перезапуск Samba

**winbindd** не смог запуститься потому,что пока что мы не домен.

[Перезапустите](/index.php/Daemons "Daemons") сервис Samba и winbind тоже должен запуститься.

NSSwitch говорит Linux хосту как получить игформацию из различных источников и к каком порядке это сделать. В нашем случае мы добаим AD как дополнительный источник для пользователей, групп и хостов.

 `/etc/nsswitch.conf` 

```
 passwd:            files winbind
 shadow:            files winbind
 group:             files winbind 

 hosts:             files dns wins

```

### Проверка Winbind

Проверим, может ли winbind получить доступ к AD. Следующие команды возвращают список пользователей AD:

 `# wbinfo -u` 

```
administrator
guest
krbtgt
test.user

```

*   Note мы создали пользователя AD 'test.user' в домменом контоллере.

Можно сделать то же самое для групп AD:

 `# wbinfo -g` 

```
domain computers
domain controllers
schema admins
enterprise admins
cert publishers
domain admins
domain users
domain guests
group policy creator owners
ras and ias servers
allowed rodc password replication group
denied rodc password replication group
read-only domain controllers
enterprise read-only domain controllers
dnsadmins
dnsupdateproxy

```

### Проверка nsswitch

Дабы убедиться,что нащ хост имеет доступ к домену для пользователей и групп, мы проверим настройки nsswitch, используя 'getent'. Следующий вывод показывает,как оно дожно выглядеть на нетронутом ArchLinux:

 `# getent passwd` 

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/bin/false
daemon:x:2:2:daemon:/sbin:/bin/false
mail:x:8:12:mail:/var/spool/mail:/bin/false
ftp:x:14:11:ftp:/srv/ftp:/bin/false
http:x:33:33:http:/srv/http:/bin/false
nobody:x:99:99:nobody:/:/bin/false
dbus:x:81:81:System message bus:/:/bin/false
ntp:x:87:87:Network Time Protocol:/var/empty:/bin/false
avahi:x:84:84:avahi:/:/bin/false
administrator:*:10001:10006:Administrator:/home/EXAMPLE/administrator:/bin/bash
guest:*:10002:10007:Guest:/home/EXAMPLE/guest:/bin/bash
krbtgt:*:10003:10006:krbtgt:/home/EXAMPLE/krbtgt:/bin/bash
test.user:*:10000:10006:Test User:/home/EXAMPLE/test.user:/bin/bash

```

Для групп:

 `# getent group` 

```
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin
adm:x:4:root,daemon
tty:x:5:
disk:x:6:root
lp:x:7:daemon
mem:x:8:
kmem:x:9:
wheel:x:10:root
ftp:x:11:
mail:x:12:
uucp:x:14:
log:x:19:root
utmp:x:20:
locate:x:21:
rfkill:x:24:
smmsp:x:25:
http:x:33:
games:x:50:
network:x:90:
video:x:91:
audio:x:92:
optical:x:93:
floppy:x:94:
storage:x:95:
scanner:x:96:
power:x:98:
nobody:x:99:
users:x:100:
dbus:x:81:
ntp:x:87:
avahi:x:84:
domain computers:x:10008:
domain controllers:x:10009:
schema admins:x:10010:administrator
enterprise admins:x:10011:administrator
cert publishers:x:10012:
domain admins:x:10013:test.user,administrator
domain users:x:10006:
domain guests:x:10007:
group policy creator owners:x:10014:administrator
ras and ias servers:x:10015:
allowed rodc password replication group:x:10016:
denied rodc password replication group:x:10017:krbtgt
read-only domain controllers:x:10018:
enterprise read-only domain controllers:x:10019:
dnsadmins:x:10020:
dnsupdateproxy:x:10021:

```

### Проверка команд Samba

Попробуйте некоторые команды,чтобу увидеть,может ли Samba взаимодействовать с AD:

 `# net ads info` 

```
[2012/02/05 20:21:36.473559,  0] param/loadparm.c:7599(lp_do_parameter)
  Ignoring unknown parameter "idmapd backend"
LDAP server: 192.168.1.2
LDAP server name: PDC.example.com
Realm: EXAMPLE.COM
Bind Path: dc=EXAMPLE,dc=COM
LDAP port: 389
Server time: Sun, 05 Feb 2012 20:21:33 CST
KDC server: 192.168.1.2
Server time offset: -3

```

 `# net ads lookup` 

```
[2012/02/05 20:22:39.298823,  0] param/loadparm.c:7599(lp_do_parameter)
  Ignoring unknown parameter "idmapd backend"
Information for Domain Controller: 192.168.1.2

Response Type: LOGON_SAM_LOGON_RESPONSE_EX
GUID: 2a098512-4c9f-4fe4-ac22-8f9231fabbad
Flags:
        Is a PDC:                                   yes
        Is a GC of the forest:                      yes
        Is an LDAP server:                          yes
        Supports DS:                                yes
        Is running a KDC:                           yes
        Is running time services:                   yes
        Is the closest DC:                          yes
        Is writable:                                yes
        Has a hardware clock:                       yes
        Is a non-domain NC serviced by LDAP server: no
        Is NT6 DC that has some secrets:            no
        Is NT6 DC that has all secrets:             yes
Forest:                 example.com
Domain:                 example.com
Domain Controller:      PDC.example.com
Pre-Win2k Domain:       EXAMPLE
Pre-Win2k Hostname:     PDC
Server Site Name :              Office
Client Site Name :              Office
NT Version: 5
LMNT Token: ffff
LM20 Token: ffff

```

 `# net ads status -U administrator | less` 

```
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: user
objectClass: computer
cn: myarchlinux
distinguishedName: CN=myarchlinux,CN=Computers,DC=leafscale,DC=inc
instanceType: 4
whenCreated: 20120206043413.0Z
whenChanged: 20120206043414.0Z
uSNCreated: 16556
uSNChanged: 16563
name: myarchlinux
objectGUID: 2c24029c-8422-42b2-83b3-a255b9cb41b3
userAccountControl: 69632
badPwdCount: 0
codePage: 0
countryCode: 0
badPasswordTime: 0
lastLogoff: 0
lastLogon: 129729780312632000
localPolicyFlags: 0
pwdLastSet: 129729764538848000
primaryGroupID: 515
objectSid: S-1-5-21-719106045-3766251393-3909931865-1105
...<snip>...

```

## Настройка PAM

Теперь мы будем менять разные правила в PAM, чтобы допустить пользователей AD к использованию системы для входа и к sudo доступу. Когда вы меняете правила, запоминание их порядка и помечены ли они как **required** или как _sufficient_ критически важно,если вы хотите,чтобы всё работало,как вы задумали.Вам не стоит отклоняться от этих правил,если только вы не знаете как писать правила для PAM

В случае со входом,PAM следует сначала запросить аккаунт AD и проверять локальные аккаунты только если аккаунту AD не соответствует локальный аккаунт.Поэтому, мы добавим записи,которые включат `pam_winbindd.so` в процесс аутентификации.

Главный процесс аутентификации в конфигурации PAM ArchLinux находится в `/etc/pam.d/system-auth`. Начав со стандартной конфигурации из `pambase`, измените её следующим образом:

### system-auth

#### Раздел "auth"

Найдите строку:

```
auth required pam_unix.so ...

```

Удалите её, и замените следующим:

```
auth [success=1 default=ignore] pam_localuser.so
auth [success=2 default=die] pam_winbind.so
auth [success=1 default=die] pam_unix.so nullok
auth requisite pam_deny.so

```

#### Раздел "account"

Найдите строку:

```
account required pam_unix.so

```

Под ней допишите следующее:

```
account [success=1 default=ignore] pam_localuser.so
account required pam_winbind.so

```

#### Раздел "session"

Найдите строку:

```
session required pam_unix.so

```

Под ней допишите следующее:

```
session [success=1 default=ignore] pam_localuser.so
session required pam_winbind.so

```

#### Раздел "password"

Найдите строку:

```
password required pam_unix.so ...

```

Удалите её и замените следующими:

```
password [success=1 default=ignore] pam_localuser.so
password [success=2 default=die] pam_winbind.so
password [success=1 default=die] pam_unix.so sha512 shadow
password requisite pam_deny.so

```

### Проверка входа

Теперь запустите новую сессию/войдите через ssh и попробуйте войти,использую данные аккаунта AD. Имя домена опционально, так как это было задано в настройках Winbind как 'default realm'. Заметьте,что в случае с ssh, вам нужно изменить `/etc/ssh/sshd_config`, чтобы он разрешал аутентификацию через kerberos: `(KerberosAuthentication yes)`.

```
test.user
EXAMPLE+test.user

```

Оба должны работать. Стоит подметить,что `/home/example/test.user` будет создан автоматически.

**Войдите в другую сессию использую аккаунт Linux. Удостоверьтесь,что всё ещё можете войти как root - запомните,что вы должны быть под аккаунтом root как минимум в одной сессии!**

## Настройка общих файлов

Ранее мы пропустили настройку общих файлов. Теперь,когда всё работает, вернитесь к `/etc/smb.conf` и добавьте эксопрт для хостов,которые вы желаете сделать доступными в Windows

 `/etc/smb.conf` 

```
[MyShare]
  comment = Example Share
  path = /srv/exports/myshare
  read only = no
  browseable = yes
  valid users = @NETWORK+"Domain Admins" NETWORK+test.user

```

В примере выше, ключевое слово **NETWORK**. Не путайте его с именем домена. Для добавления групп,добавьте символ '@' к группе. Заметьте, `Domain Admins` заключается в "цитаты", чтобы Samba корректно считывала их,когда просматривает файл конфигурации.

## Добавление файла keytab и включение беспарольного входа на машину через Kerber и ssh

Это объясняет,как сгенерировать keytab файл,который вам нужен,например,чтобы включить беспарольный вход на машину через Kerber и ssh с другой машины в том же домене. Допустим, что у вас много компьютеров в домене и вы только что добавили сервер/рабочую станцию использую описание выше в ваш домен, в котором пользователям нужен ssh для работы - например рабочаю станция GPU или вычислительный узел OpenMP и т.д. В этом случае вам, наверное, не захочется вводить пароль каждый раз при входе. С другой стороны аутентификация с помощью ключа используется множеством пользователей, в этом случае нужных полномочий для,например,монтирования общего NFSv4 с Kerberos. Так что это поможет включить беспарольные входы на машины используя "kerberos ticket forwarding".

### Создание key tab файла

Запустите 'net ads keytab create -U administrator' как суперпользователь дабы создать keytab файл в '/etc/krb5.keytab'. Она напишет ваи,что необходимо включить аутентификацию с помощью keytab в файле конфигурации, чтобы мы могли совершить следующий шаг. Иногда возникают проблемы, если файл krb5.keytab уже существует,в таком случае нужно переименовать его и запустить команду ещё раз, это должно помочь.

 `# net ads keytab create -U administrator` 

Проверьте содержание файла следующим образом:

 `# klist -k /etc/krb5.keytab` 

```
Keytab name: FILE:/etc/krb5.keytab
KVNO Principal
---- --------------------------------------------------------------------------
   4 host/myarchlinux.example.com@EXAMPLE.COM
   4 host/myarchlinux.example.com@EXAMPLE.COM
   4 host/myarchlinux.example.com@EXAMPLE.COM
   4 host/myarchlinux.example.com@EXAMPLE.COM
   4 host/myarchlinux.example.com@EXAMPLE.COM
   4 host/MYARCHLINUX@EXAMPLE.COM
   4 host/MYARCHLINUX@EXAMPLE.COM
   4 host/MYARCHLINUX@EXAMPLE.COM
   4 host/MYARCHLINUX@EXAMPLE.COM
   4 host/MYARCHLINUX@EXAMPLE.COM
   4 MYARCHLINUX$@EXAMPLE.COM
   4 MYARCHLINUX$@EXAMPLE.COM
   4 MYARCHLINUX$@EXAMPLE.COM
   4 MYARCHLINUX$@EXAMPLE.COM
   4 MYARCHLINUX$@EXAMPLE.COM

```

### Включение входа через keytab

Теперь вам нужно указать winbind,что он должен использовать keytab файлы,добавив следующий строки в /etc/samba/smb.conf:

 `/etc/samba/smb.conf` 

```
 kerberos method = system keytab
 dedicated keytab file = /etc/krb5.keytab

```

В итоге всё должно выглядеть примерно так:

 `/etc/samba/smb.conf` 

```
[Global]
  netbios name = MYARCHLINUX
  workgroup = EXAMPLE
  realm = EXAMPLE.COM
  server string = %h ArchLinux Host
  security = ads
  encrypt passwords = yes
  password server = pdc.example.com
  kerberos method = system keytab
  dedicated keytab file = /etc/krb5.keytab

  idmap config * : backend = tdb
  idmap config * : range = 10000-20000

  winbind use default domain = Yes
  winbind enum users = Yes
  winbind enum groups = Yes
  winbind nested groups = Yes
  winbind separator = +
  winbind refresh tickets = yes

  template shell = /bin/bash
  template homedir = /home/%D/%U

  preferred master = no
  dns proxy = no
  wins server = pdc.example.com
  wins proxy = no

  inherit acls = Yes
  map acl inherit = Yes
  acl group control = yes

  load printers = no
  debug level = 3
  use sendfile = no

```

Перезапустите winbind.service с помощью 'systemctl restart winbind.service' с привелегиями суперпользователя.

 `# systemctl restart winbind.service` 

Проверьте,всё ли работает,получив тикет для вашей системы и запустив

 `# kinit MYARCHLINUX$ -kt /etc/krb5.keytab` 

Эта команда не должна написать ничего в консоль,ондако 'klist' должен показать что-то вроде этого:

 `# klist` 

```
 Ticket cache: FILE:/tmp/krb5cc_0
 Default principal: MYARCHLINUX$@EXAMPLE.COM

 Valid starting    Expires           Service principal 
 02/04/12 21:27:47 02/05/12 07:27:42 krbtgt/EXAMPLE.COM@EXAMPLE.COM
         renew until 02/05/12 21:27:47

```

Некоторые частые ошибки : a)забывают поставить $ или b) игнорируют чувствительный регистр - он должен быть точно таким же,как записьв keytab

### Подготовка sshd на сервере

Всё,что нам нужно сделать - это добавить некоторые опции в sshd_config и перезапустить sshd.service.

Измените '/etc/ssh/sshd_config' чтобы он выглядел так в нужных местах:

 `# /etc/ssh/sshd_config` 

```

...

# Изсенить на no чтобы выключить s/key пароли
ChallengeResponseAuthentication no

# Опции Kerberos 
KerberosAuthentication yes
#KerberosOrLocalPasswd yes
KerberosTicketCleanup yes
KerberosGetAFSToken yes

# Опции GSSAPI
GSSAPIAuthentication yes
GSSAPICleanupCredentials yes

...

```

Перезапустите sshd.service:

 `# systemctl restart sshd.service` 

### Добавление опций, нужных для клиента

Для начала нам нужно убедиться в том, что тикеты доступны для клиента. Обычно всё работает, но, на всякий случай, используйте следующий параметр:

```
forwardable = true

```

Далее надо добавить опции:

```
GSSAPIAuthentication yes
GSSAPIDelegateCredentials yes

```

в наш файл `.ssh/config`, который говорит _ssh_ использовать эту опцию, как альтернативу: можно использовать 'ssh -o' (смотрите страницу справочного руководства `man ssh`).

### Проверка установки

Клиент:

Убедитесь,что у вас правильный тикет, используя 'kinit'. Затем подключитесь к своем машине через ssh

 `ssh myarchlinux.example.com ` 

Вы должны подключится без просьбы ввести пароль

Если у вас также включна аутентификация ключем,нужно выполнить

 `ssh -v myarchlinux.example.com ` 

чтобы увидеть,какой метод аутентификации используется на самом деле.

Для дебага вы можете включить DEBUG3 на сервере и посмотреть лог через 'journalctl'

### Настройка для полной аутентификации Kerberos без пароля.

Если ваши клиенты не используют доменные аккаунты на их локальных машинах (по какой бы то не было причине),довольно сложно будет научить их использовать 'kinit' перед тем,как ssh подключится к рабочей станции.Так что есть классный способ это решить:

## Генерирование keytab, которые будет принимать AD

Пользователь должен выполнить:

```
ktutil
addent -password -p username@EXAMPLE.COM -k 1 -e RC4-HMAC
- enter password for username -
wkt username.keytab
q

```

Теперь провертьте файл:

 `kinit -kt username.keytab` 

Оно не должно спросить пароль, теперь просто скопируйте это в '~/.bashrc', это позволит не вводит пароль каждый раз.

### Интересно знать

Файл 'username.keytab' не спецефичен для машины,и,следовательно,может быть скопирован на другие машины. Например,мы создали файл на Linux машине и скопировали на Mac клиента так как команды в неё другие...

## Смотрите также

*   [Wikipedia: Active Directory](https://en.wikipedia.org/wiki/ru:Active_Directory "wikipedia:ru:Active Directory")
*   [Wikipedia: Samba](https://en.wikipedia.org/wiki/ru:Samba "wikipedia:ru:Samba")
*   [Wikipedia: Kerberos](https://en.wikipedia.org/wiki/ru:Kerberos "wikipedia:ru:Kerberos")
*   [Samba: Documentation](http://www.samba.org/samba/docs)
*   [Samba Wiki: Samba & Active Directory](https://wiki.samba.org/index.php/Setup_a_Samba_AD_Member_Server)
*   [Samba Man Page: smb.conf](http://www.samba.org/samba/docs/man/manpages-3/smb.conf.5.html)

### Коммерческие решения

*   Centrify
*   Likewise