Взято [отсюда](http://www.squid-cache.org):

	*Squid - кеширующий прокси-сервер поддерживающий HTTP, HTTPS, FTP, и многое другое. It reduces bandwidth and improves response times by caching and reusing frequently-requested web pages. Squid has extensive access controls and makes a great server accelerator. It runs on Unix and Windows and is licensed under the GNU GPL.*

Помимо того что squid отлично работает в больших корпорациях и школах, он может быть использован и дома. Если вы ищите более легкий однопользовательский прокси, вам следует взглянуть на [Polipo](/index.php/Polipo "Polipo") ([website](http://www.pps.jussieu.fr/~jch/software/polipo/)).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [3 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [4 Другие приложения](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
*   [5 NTLM](#NTLM)

## Установка

Для установки последней версии Squid выполните команду:

```
pacman -S squid

```

## Настройка

По умолчанию, папки кэша будут созданы в /var/cache/squid, и будут выставлены соответсвенные права для этих папок. Однако, для более полного контроля, нужно произвести настройку в <tt>/etc/squid/squid.conf</tt>.

Все строки закомментированы, но если вы хотите их раскомментировать, вам следует выполнить:

```
sed -i "/^#/d;/^ *$/d" /etc/squid/squid.conf

```

Следующие опции могут быть полезными. Если такой опции в вашем файле конфигурации нет, то просто добавьте её!

*   <tt>http_port</tt> - Устанавливает порт, который связывается со Squid на локальном компьютере. Вы можете настроить Squid для подключения к нескольким портам, задав несколько http_proxy линий. По умолчанию, Squid соединяется через порт 3128.

```
http_port 3128
http_port 3129

```

*   <tt>http_access</tt> - Это лист доступа, который контролирует доступ для использования прокси. По умолчанию только локальная машина имеет доступ. Для тестирования возможностей, вы можете изменить параметр <tt>http_access deny all</tt> на <tt>http_access allow all</tt>, что обеспечит доступ для любой машины. Если вы хотите обеспечить доступ только к своей сети, вы можете сделать так:

```
acl ip_acl src 192.168.1.0/24
http_access allow ip_acl
http_access deny all

```

*   <tt>cache_mgr</tt> - Это электропочта кэш-менеджера.

```
cache_mgr squid.admin@example.com

```

*   <tt>shutdown_lifetime</tt> - определяет как долго Squid должен ждать, после того как скрипт, лежащий в rc.d, даст команду остановки. Если вы используете Squid на домашнем ПК, возможно вы захотите выставить это значение минимальным.

```
shutdown_lifetime 10 seconds

```

*   <tt>cache_mem</tt> - This is how much memory you want Squid to use to keep objects in memory rather than writing them to disk. Squid's total memory usage will exceed this! By default this is 8MB, so you might want to increase it if you have lots of RAM available.

```
cache_mem 64 MB

```

*   <tt>visible_hostname</tt> - Pretty much self explanatory!

```
visible_hostname cerberus

```

*   <tt>cache_peer</tt> - If you want your Squid to go through another proxy server, rather than directly out to the Internet, you need to specify it here.
*   <tt>never_direct</tt> - Tells the cache to never go direct to the internet to retrieve a page. You will want this if you have set the option above.

```
cache_peer 10.1.1.100 parent 8080 0 no-query default
never_direct allow all

```

*   <tt>maximum_object_size</tt> - The largest size of a cached object. By default this is small (256KB I think), so if you have a lot of disk space you will want to increase the size of it to something reasonable.

```
maximum_object_size 10 MB

```

*   <tt>cache_dir</tt> - This is your cache directory, where all the cached files are stored. There are many options here, but the format should generally go like:

```
cache_dir diskd <directory> <size in MB> 16 256

```

So, in the case of a school's internet proxy:

```
cache_dir diskd /cache0 200000 16 256

```

If you change the cache directory from defaults, you must set the correct permissions on the cache directory before starting Squid, else it won't be able to create its cache directories and will fail to start.

## Запуск

После завершения конфигурирования, необходимо проверить корректность файла конфигурации:

```
squid -k check

```

Создайте кеш-директории:

```
squid -z

```

Теперь запустите Squid

```
/etc/rc.d/squid start

```

Не забудьте добавить <tt>squid</tt> в раздел <tt>DAEMONS=()</tt> файла rc.conf если вы хотите, чтобы Squid запускался при загрузке системы.

## Другие приложения

If you're looking for a content filtering solution to work with Squid, you should check out the very powerful [DansGuardian](/index.php/DansGuardian "DansGuardian") ([website](http://www.dansguardian.org)). If you'd like a web-based frontend for managing Squid, [Webmin](/index.php/Webmin "Webmin") is your best bet.

## NTLM

*This section is really unclear...*

To get Windows authentication, we should change /etc/squid/squid.conf: Что бы получить аутентификацию в Windows,вы должны изменить /etc/squid/squid.conf:

```
http_port 3128
hierarchy_stoplist cgi-bin ?
acl apache rep_header Server ^Apache
broken_vary_encoding allow apache
acl apache rep_header Server ^Apache
broken_vary_encoding allow apache
cache_mem 50 MB
access_log /var/log/squid/access.log squid
auth_param ntlm children 20
auth_param ntlm program /usr/bin/ntlm_auth --helper-protocol=squid-2.5-ntlmssp
authenticate_ip_ttl 9 hour
refresh_pattern ^ftp:           1440    20%     10080
refresh_pattern ^gopher:        1440    0%      1440
refresh_pattern .               0       20%     4320
acl all src 0.0.0.0/0.0.0.0
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
acl to_localhost dst 127.0.0.0/8
acl SSL_ports port 443
acl Safe_ports port 80          # http
acl Safe_ports port 21          # ftp
acl Safe_ports port 443         # https
acl Safe_ports port 70          # gopher
acl Safe_ports port 210         # wais
acl Safe_ports port 1025-65535  # unregistered ports
acl Safe_ports port 280         # http-mgmt
acl Safe_ports port 488         # gss-http
acl Safe_ports port 591         # filemaker
acl Safe_ports port 777         # multiling http
acl CONNECT method CONNECT
acl auth  proxy_auth REQUIRED

http_access allow manager localhost
http_access deny manager
http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access allow all auth
http_access deny all

http_access allow all

http_reply_access allow all
icp_access allow all

cache_effective_user proxy
cache_effective_group proxy

coredump_dir /var/cache/squid

visible_hostname yourhostname

```