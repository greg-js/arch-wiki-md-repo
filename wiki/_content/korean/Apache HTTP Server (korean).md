Related articles

*   [PHP](/index.php/PHP "PHP")
*   [MySQL](/index.php/MySQL "MySQL")
*   [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin")
*   [Adminer](/index.php/Adminer "Adminer")
*   [XAMPP](/index.php/XAMPP "XAMPP")
*   [mod_perl](/index.php/Mod_perl "Mod perl")

[Apache HTTP Server](https://en.wikipedia.org/wiki/Apache_HTTP_Server "wikipedia:Apache HTTP Server")(생략해서 Apache라고도 한다)는 아파치 소프트웨어 재단에서 개발된 유명한 웹 서버이다.

아파치는 보통 MySQL 같은 데이터베이스와 PHP 등의 스크립트 언어와 함께 사용된다. 이러ᅟ한 아파치와의 연동을 흔히 [LAMP](https://en.wikipedia.org/wiki/LAMP_(software_bundle) stack (**L**inux, **A**pache, **M**ySQL, **P**HP)이라고 불린다. 이 문서에서는 아파치 서버 구축 방법과 [PHP](/index.php/PHP "PHP"), [MySQL](/index.php/MySQL "MySQL") 연동 방법에 대해서 설명한다.

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
*   [2 설정](#.EC.84.A4.EC.A0.95)
    *   [2.1 고급 옵션](#.EA.B3.A0.EA.B8.89_.EC.98.B5.EC.85.98)
    *   [2.2 사용자 디렉토리](#.EC.82.AC.EC.9A.A9.EC.9E.90_.EB.94.94.EB.A0.89.ED.86.A0.EB.A6.AC)
    *   [2.3 TLS/SSL](#TLS.2FSSL)
        *   [2.3.1 키 생성과 자체 서명 인증 방법](#.ED.82.A4_.EC.83.9D.EC.84.B1.EA.B3.BC_.EC.9E.90.EC.B2.B4_.EC.84.9C.EB.AA.85_.EC.9D.B8.EC.A6.9D_.EB.B0.A9.EB.B2.95)
    *   [2.4 가상 호스트](#.EA.B0.80.EC.83.81_.ED.98.B8.EC.8A.A4.ED.8A.B8)
        *   [2.4.1 가상 호스트 관리](#.EA.B0.80.EC.83.81_.ED.98.B8.EC.8A.A4.ED.8A.B8_.EA.B4.80.EB.A6.AC)
*   [3 확장 모듈(Extensions)](#.ED.99.95.EC.9E.A5_.EB.AA.A8.EB.93.88.28Extensions.29)
    *   [3.1 PHP](#PHP)
        *   [3.1.1 php-fpm, mod_proxy_fcgi 사용하기](#php-fpm.2C_mod_proxy_fcgi_.EC.82.AC.EC.9A.A9.ED.95.98.EA.B8.B0)
        *   [3.1.2 apache2-mpm-worker, mod_fcgid 사용하기](#apache2-mpm-worker.2C_mod_fcgid_.EC.82.AC.EC.9A.A9.ED.95.98.EA.B8.B0)
        *   [3.1.3 MySQL/MariaDB](#MySQL.2FMariaDB)
    *   [3.2 HTTP2](#HTTP2)
*   [4 문제 해결](#.EB.AC.B8.EC.A0.9C_.ED.95.B4.EA.B2.B0)
    *   [4.1 아파치 서버 상태와 로그](#.EC.95.84.ED.8C.8C.EC.B9.98_.EC.84.9C.EB.B2.84_.EC.83.81.ED.83.9C.EC.99.80_.EB.A1.9C.EA.B7.B8)
    *   [4.2 Error: PID file /run/httpd/httpd.pid not readable (yet?) after start](#Error:_PID_file_.2Frun.2Fhttpd.2Fhttpd.pid_not_readable_.28yet.3F.29_after_start)
    *   [4.3 Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.](#Apache_is_running_a_threaded_MPM.2C_but_your_PHP_Module_is_not_compiled_to_be_threadsafe.)
    *   [4.4 AH00534: httpd: Configuration error: No MPM loaded.](#AH00534:_httpd:_Configuration_error:_No_MPM_loaded.)
    *   [4.5 Changing the max_execution_time in php.ini has no effect](#Changing_the_max_execution_time_in_php.ini_has_no_effect)
*   [5 참조](#.EC.B0.B8.EC.A1.B0)

## 설치

[apache](https://www.archlinux.org/packages/?name=apache) 패키지를 설치([Install](/index.php/Install "Install"))한다.

## 설정

아파치 설정 파일들은 `/etc/httpd/conf`에 위치한다. 주(主) 파일은 `/etc/httpd/conf/httpd.conf`로서 다른 설정파일들을 포함한다. 기본 설정파일은 아파치 설치 과정에서 자동으로 생성되며 정상적으로 동작하는 설정 파일이다. 기본 설정파일은 `/srv/http` 디렉토리를 서버의 웹페이지에 접속한 사용자에게 제공한다.

아파치 서버 서비스를 시작하기 위해서는 [systemd](/index.php/Systemd#Using_units "Systemd")를 이용하여 `httpd.service`를 시작한다.

서비스 시작 후에는 아파치 서버가 정상적으로 동작하고 있을 것이다. 서버의 동작여부를 확인하기 위해서는 웹 브라우저에서 [http://localhost/로](http://localhost/로) 접속한다. 접속하면 간단한 인덱스 페이지가 출력될 것이다.

아파치 설정에 관련된 자세한 정보는 이어지는 절을 참고한다.

### 고급 옵션

아래에 열거된 옵션들은 `/etc/httpd/conf/httpd.conf` 파일 내에 정의되어 있는 것으로서, 서버를 구축하고자 하는 사용자에게 유용한 옵션들이다.

```
User http

```

	아파치는 보안 문제 때문에 root 관리자에 의해 시작된 뒤 곧바로 http UID로 전환된다. 설정파일에 기본으로 등록되는 사용자는 http이며 해당 사용자는 아파치 설치 과정에서 자동으로 생성된다.

```
Listen 80

```

	아파치 서버에서 열어 놓을 포트를 설정한다. 라우터를 이용한 인터넷 접근을 위해서는 반드시 포트포워딩을 설정해주어야 한다.

	만일 아파치 서버를 로컬에서만 접속이 허용되도록 설정하고 싶다면, 해당 줄 내용을 `Listen 127.0.0.1:80`으로 변경한다.

```
ServerAdmin you@example.com

```

	관리자의 이메일 주소를 설정한다. 설정된 이메일 주소는 에러 페이지에서 관리자 메일로 표시된다.

```
DocumentRoot "/srv/http"

```

	호스팅할 웹 페이지들이 위치하는 디렉토리 위치

	DocumentRoot를 변경하면 `<Directory "/srv/http">`도 변경해야한다. 그렇지 않으면 변경된 DocumentRoot에 접근할 때 **403 에러**(권한 부족 에러)가 발생한다. 또한, `Require all denied` 부분을 `Require all granted`으로 변경해야 한다. 해당 라인을 바꾸지 않는 경우에도 **403 에러**가 발생할 수 있다. 언급한 두 가지 경우 외에, DocumentRoot 디텍토리와 그 부모 디렉토리의 권한 문제가 있는 경우에도 **403 에러**가 발생될 수 있다.

두 개의 디렉토리(DocumentRoot, DocumentRoot의 부모 디렉토리)는 반드시 다른 사용자들에게도 실행권한이 부여되어야 한다. (`chmod o+x /path/to/DocumentRoot`를 통해 설정할 수 있다)

위에서 언급된 권한관련 해결방법에는 몇 가지 논란이 있다. 반드시 모든 사용자들에게 실행 권한을 줄 필요가 없고 ACL을 통해 웹서버에만 실행 권한을 줄 수 있는 방법이 있기 때문이다. 자세한 내용은 다음 링크를 살펴보자. [Access Control Lists#Granting execution permissions for private files to a Web Server](/index.php/Access_Control_Lists#Granting_execution_permissions_for_private_files_to_a_Web_Server "Access Control Lists"), [Talk:Apache HTTP Server](/index.php/Talk:Apache_HTTP_Server "Talk:Apache HTTP Server")

```
AllowOverride None

```

	`<Directory>` 섹션 안의 위 디렉티브는 아파치가 `.htaccess` 파일을 완전하게 무시하도록 설정해준다. 하지만 아피치 2.4버전 이후부터 해당 옵션은 기본으로 되어있기 때문에 `.htaccess` 파일을 사용하고 싶다면 명시적으로 허용해주어야 한다. `.htaccess`에서 `mod_rewrite` 혹은 다른 설정들을 사용하고 싶다면 .htaccess파일에 관련 디렉티브를 선언함으로써 서버 설정을 오버라이딩 해야 한다. 이에 관련된 자세한 내용은 다음 링크를 참고한다. [Apache documentation](http://httpd.apache.org/docs/current/mod/core.html#allowoverride).

**Tip:** 만약 아파치 설정파일과 관련된 이슈가 있다면 다음 명령어를 통해 설정파일을 점검할 수 있다: `apachectl configtest`

더 많은 설정 옵션들은 다음 파일에서 확인할 수 있다: `/etc/httpd/conf/extra/httpd-default.conf`:

서버 서명을 비활성화하려면 다음 라인을 추가한다:

```
ServerSignature Off

```

아파치와 PHP 버전과 같은 서버 정보를 숨기려면 다음 라인을 추가한다:

```
ServerTokens Prod

```

### 사용자 디렉토리

사용자 디렉토리는 기본적으로 [http://localhost/~yourusername/를](http://localhost/~yourusername/를) 통해서 접근 가능하며, `~/public_html`의 내용을 표시한다. (`/etc/httpd/conf/extra/httpd-userdir.conf`에서 변경이 가능하다).

만일 유저 디렉토리를 원하지 않는 경우에는 `/etc/httpd/conf/httpd.conf` 파일에서 다음 라인을 주석처리한다:

```
Include conf/extra/httpd-userdir.conf

```

아파치가 사용자의 홈디렉토리에 접근하기 위해서는 반드시 디렉토리의 권한을 적절하게 설정해 주어야 한다. 홈 디렉토리와 `~/public_html`은 반드시 다른 사용자들이 실행권한을 갖고 있어야 한다. (혹은 ACL을 통해 아파치 사용자 http에 한해서만 허용하도록 한다.)

```
$ chmod o+x ~
$ chmod o+x ~/public_html
$ chmod -R o+r ~/public_html

```

권한 설정이 완료되면 `httpd.service`를 재시작한다. [Umask#Set the mask value](/index.php/Umask#Set_the_mask_value "Umask") 참고.

### TLS/SSL

**Warning:** SSL/TLS 구현하고자 한다면 몇몇 변수들과 구현부분에서 [여전히](https://weakdh.org/#affected) [공격에 취약](https://en.wikipedia.org/wiki/Transport_Layer_Security#Attacks_against_TLS.2FSSL "wikipedia:Transport Layer Security")하다는 것을 알고 있어야 한다. 현재 SSL/TLS에서의 취약점과 웹 서버에 어떻게 반영시켜야 하는지 알고 싶다면 [http://disablessl3.com/와](http://disablessl3.com/와) [https://weakdh.org/sysadmin.html](https://weakdh.org/sysadmin.html) 사이트를 방문하면 더 자세한 정보를 얻을 수 있다.

[openssl](https://www.archlinux.org/packages/?name=openssl)는 TLS/SSL을 지원하고 아치에서 기본으로 설치된다.

`/etc/httpd/conf/httpd.conf`파일에서 다음 세 개의 라인의 주석처리를 해제한다:

```
LoadModule ssl_module modules/mod_ssl.so
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
Include conf/extra/httpd-ssl.conf

```

TLS/SSL를 위해서는 키와 인증이 필요하다. 만약 공공 도메인을 가지고 있다면 무료로 인증을 받기 위해 [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt")를 사용할 수 있다. 공공 도메인을 가지고 있지 않다면 [#키 생성과 자체 서명 인증 방법](#.ED.82.A4_.EC.83.9D.EC.84.B1.EA.B3.BC_.EC.9E.90.EC.B2.B4_.EC.84.9C.EB.AA.85_.EC.9D.B8.EC.A6.9D_.EB.B0.A9.EB.B2.95)방법을 참고한다.

키와 인증을 얻고 나서는 `/etc/httpd/conf/extra/httpd-ssl.conf` 파일 내의 `SSLCertificateFile`, `SSLCertificateKeyFile` 라인에서 해당 키와 인증을 가리키도록 설정한다.

마지막으로 변경 사항 적용을 위해 `httpd.service` 를 재시작한다.

**Tip:** Mozilla has a useful [SSL/TLS article](https://wiki.mozilla.org/Security/Server_Side_TLS) which includes [Apache specific](https://wiki.mozilla.org/Security/Server_Side_TLS#Apache) configuration guidelines as well as an [automated tool](https://mozilla.github.io/server-side-tls/ssl-config-generator/) to help create a more secure configuration.

#### 키 생성과 자체 서명 인증 방법

개인키와 자체 서명 인증을 생성한다. 이것은 [CSR](https://en.wikipedia.org/wiki/Certificate_signing_request "wikipedia:Certificate signing request")가 요구되지 않는 대부분의 설치로는 적절하다.

```
# cd /etc/httpd/conf
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout server.key -out server.crt -days 1095
# chmod 400 server.key

```

**Note:** -days 스위치는 옵션이며 RSA 키 크기는 최소 2048(기본값) 이상이어야 한다.

만약 [CSR](https://en.wikipedia.org/wiki/Certificate_signing_request "wikipedia:Certificate signing request")의 생성이 필요하다면, 위의 방법 대신 아래의 키 생성 방법을 따르도록 한다.

```
# openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:4096 -out server.key
# chmod 400 server.key
# openssl req -new -sha256 -key server.key -out server.csr
# openssl x509 -req -days 1095 -in server.csr -signkey server.key -out server.crt

```

**Note:** 더 많은 openssl 옵션을 보려면 [man page](https://www.openssl.org/docs/apps/openssl.html) 또는 peruse openssl의 [extensive documentation](https://www.openssl.org/docs/)를 참고한다.

### 가상 호스트

**Note:** SSL 가상 호스트를 사용하기 위해서는 독립적인 <VirtualHost dommainame:443> 섹션을 추가해야한다. 관련된 예제는 다음 링크를 참고한다: [#Managing many virtual hosts](#Managing_many_virtual_hosts)

한 개 이상의 호스트를 원하는 경우에 `/etc/httpd/conf/httpd.conf` 설정 파일에서 아래 기술된 부분의 주석을 해제한다.

```
Include conf/extra/httpd-vhosts.conf

```

또한, `/etc/httpd/conf/extra/httpd-vhosts.conf` 파일에서 가상 호스트를 설정할 수 있다. 제공되는 기본 설정파일에는 자세한 예제가 많기 때문에 호스트 설정을 위해 참고하기에 유용하다.

로컬 머신에서 가상 호스트를 테스트하고 싶다면, `/etc/hosts` 파일에 가상 도메인명을 다음과 같이 등록한다:

```
127.0.0.1 domainname1.dom 
127.0.0.1 domainname2.dom

```

파일 변경 후, 설정 적용을 위해 `httpd.service`를 재시작한다.

#### 가상 호스트 관리

이 절에서는 엄청나게 많은 가상 호스트를 가지고 있는 경우에 가상 호스트들을 관리하는 방법에 대하여 기술한다. 이러한 경우에는 가상 호스트별로 설정 파일을 만들고 이를 하나의 디렉토리(예: `/etc/httpd/conf/vhosts`)에 저장하는 것을 권장한다.

먼저 디렉토리를 하나 생성한다:

```
# mkdir /etc/httpd/conf/vhosts

```

각 가상 호스트별 설정 파일을 생성한 디렉토리 안에 생성한다:

```
# nano /etc/httpd/conf/vhosts/domainname1.dom
# nano /etc/httpd/conf/vhosts/domainname2.dom
...

```

마지막으로 아파치 메인 설정파일인 `/etc/httpd/conf/httpd.conf` 안에 `Include`를 사용하서 가상 호스트별로 생성해둔 설정 파일들을 포함시킨다:

```
#Enabled Vhosts:
Include conf/vhosts/domainname1.dom
Include conf/vhosts/domainname2.dom

```

위처럼 각각의 가상 호스트를 주석처리를 통해 간단하게 활성화/비활성화할 수 있다.

다음은 각 가상 호스트별 파일의 예제이다:

 `/etc/httpd/conf/vhosts/domainname1.dom` 
```
<VirtualHost domainname1.dom:80>
    ServerAdmin webmaster@domainname1.dom
    DocumentRoot "/home/user/http/domainname1.dom"
    ServerName domainname1.dom
    ServerAlias domainname1.dom
    ErrorLog "/var/log/httpd/domainname1.dom-error_log"
    CustomLog "/var/log/httpd/domainname1.dom-access_log" common

    <Directory "/home/user/http/domainname1.dom">
        Require all granted
    </Directory>
</VirtualHost>

<VirtualHost domainname1.dom:443>
    ServerAdmin webmaster@domainname1.dom
    DocumentRoot "/home/user/http/domainname1.dom"
    ServerName domainname1.dom:443
    ServerAlias domainname1.dom:443
    ErrorLog "/var/log/httpd/domainname1.dom-error_log"
    CustomLog "/var/log/httpd/domainname1.dom-access_log" common

    <Directory "/home/user/http/domainname1.dom">
        Require all granted
    </Directory>

    SSLEngine on
    SSLCertificateFile "/etc/httpd/conf/apache.crt"
    SSLCertificateKeyFile "/etc/httpd/conf/apache.key"
</VirtualHost>
```

## 확장 모듈(Extensions)

### PHP

[PHP](/index.php/PHP "PHP") 설치를 위해서는 [php](https://www.archlinux.org/packages/?name=php), [php-apache](https://www.archlinux.org/packages/?name=php-apache) 패키지를 설치한다.

`/etc/httpd/conf/httpd.conf` 파일에서 아래의 줄을 주석처리 한다:

```
#LoadModule mpm_event_module modules/mod_mpm_event.so

```

그리고 아래의 줄의 주석을 해제한다:

```
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

**Note:** [php-apache](https://www.archlinux.org/packages/?name=php-apache)에 포함된 `libphp7.so`이 `mod_mpm_event`와는 제대로 동작하지 않고 `mod_mpm_prefork`에서만 정상적으로 동작하기 때문에 위에서 기술된 것처럼 설정해주어야 한다.(참고: [FS#39218](https://bugs.archlinux.org/task/39218))

위의 처리를 해주지 않는 경우 다음과 같은 에러 메세지가 출력된다:

```
Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.
AH00013: Pre-configuration failed
httpd.service: control process exited, code=exited status=1
```
또 다른 해결 방법으로, `mod_proxy_fcgi`를 사용하는 방법이 있다. 자세한 방법은 이하 절의 [#Using php-fpm and mod_proxy_fcgi](#Using_php-fpm_and_mod_proxy_fcgi)를 참고한다.

PHP를 활성화하기 위해서 `/etc/httpd/conf/httpd.conf` 파일에 아래 코드를 추가해준다:

*   `LoadModule` 리스트에서, `LoadModule dir_module modules/mod_dir.so` 다음의 원하는 곳에 아래 코드를 추가한다:

```
LoadModule php7_module modules/libphp7.so

```

*   `Include` 리스트 마지막 부분에 다음을 추가한다:

```
Include conf/extra/php7_module.conf

```

설정을 완료한 후, [systemd를 사용하여](/index.php/Systemd#Using_units "Systemd") `httpd.service`를 재시작한다.

PHP가 올바르게 설정되었는지 확인하려면 아파치 `DocumentRoot` 디렉토리(예. `/srv/http/` 혹은 `~/public_html`)에 `test.php` 파일을 생성하여 다음 코드를 해당 파일에 추가한다:

```
<?php phpinfo(); ?>

```

파일을 저장한 뒤, PHP가 제대로 작동하는지 확인하기 위하여 브라우저를 통해 다음 URL을 연다: [http://localhost/test.php](http://localhost/test.php) 또는 [http://localhost/~myname/test.php](http://localhost/~myname/test.php)

더 많은 설정 옵션과 확장 모듈(extensions)에 대한 정보는 [PHP](/index.php/PHP "PHP")를 참고한다.

#### php-fpm, mod_proxy_fcgi 사용하기

**Note:** 널리 알려진 ProxyPass를 이용한 설정과 다르게 SetHandler를 이용한 프록시 설정은 DirectoryIndex와 같이 아파치에서 사용되는 디렉티브를 방해하지 않는다. 이러한 특징ᅟ 덕분에 libphp7, mod_fastcgi, mod_fcgid 등으로 디자인된 소프트웨어와 더 나은 호환성을 보장한다. 하지만 그래도 ProxyPass를 계속해서 사용하고 싶다면, 아래 코드와 같이 시도하여 사용할 수 있다: `ProxyPassMatch ^/(.*\.php(/.*)?)$ unix:/run/php-fpm/php-fpm.sock|fcgi://localhost/srv/http/$1` 

[php-fpm](https://www.archlinux.org/packages/?name=php-fpm) 패키지를 설치한다.

아래의 내용으로 `/etc/httpd/conf/extra/php-fpm.conf` 파일을 생성한다:

 `/etc/httpd/conf/extra/php-fpm.conf` 
```
<FilesMatch \.php$>
    SetHandler "proxy:unix:/run/php-fpm/php-fpm.sock|fcgi://localhost/"
</FilesMatch>
<Proxy "fcgi://localhost/" enablereuse=on max=10>
</Proxy>
<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>

```

그리고 나서 `/etc/httpd/conf/httpd.conf` 파일의 최하단에 include 코드를 추가한다:

```
Include conf/extra/php-fpm.conf

```

**Note:** 위 코드에서 `sock`과 `fcgi` 사이의 파이프 좌우로 빈칸은 허용되지 않는 점에 유의해야 한다. `localhost`는 다른 문자열로 치환될 수 있으며, 치환된 문자열은 반드시 `SetHandler`와 `Proxy` 디렉티브에서도 일치해야 한다. 더 자세한 정보는 [이곳](https://httpd.apache.org/docs/2.4/mod/mod_proxy_fcgi.html)에서 확인할 수 있다. `SetHandler`와 `Proxy`는 가상 호스트 설정 파일별로 사용가능하지만 `fcgi://` 이후의 이름은 반드시 가상 호스트들끼리 서로 달라야 한다.

`/etc/php/php-fpm.d/www.conf`에서 PHP-FPM을 설정할 수 있지만 기본 설정으로도 정상적으로 동작한다.

**Note:**

아래 코드는 더이상 필요하지 않기 때문에 만약 `httpd.conf` 파일에 추가했다면 삭제하도록 한다.

```
LoadModule php7_module modules/libphp7.so
Include conf/extra/php7_module.conf

```

`httpd.service`와 `php-fpm.service`를 재시작한다.

#### apache2-mpm-worker, mod_fcgid 사용하기

[mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid)와 [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) 패키지를 설치한다.

PHP wrapper를 위해 필요한 디렉토리와 심볼릭 링크를 만들어준다:

```
# mkdir /srv/http/fcgid-bin
# ln -s /usr/bin/php-cgi /srv/http/fcgid-bin/php-fcgid-wrapper

```

다음 내용으로 `/etc/httpd/conf/extra/php-fcgid.conf` 파일을 생성한다:

 `/etc/httpd/conf/extra/php-fcgid.conf` 
```
# Required modules: fcgid_module

<IfModule fcgid_module>
    AddHandler php-fcgid .php
    AddType application/x-httpd-php .php
    Action php-fcgid /fcgid-bin/php-fcgid-wrapper
    ScriptAlias /fcgid-bin/ /srv/http/fcgid-bin/
    SocketPath /var/run/httpd/fcgidsock
    SharememPath /var/run/httpd/fcgid_shm
        # If you don't allow bigger requests many applications may fail (such as WordPress login)
        FcgidMaxRequestLen 536870912
        # Path to php.ini – defaults to /etc/phpX/cgi
        DefaultInitEnv PHPRC=/etc/php/
        # Number of PHP childs that will be launched. Leave undefined to let PHP decide.
        #DefaultInitEnv PHP_FCGI_CHILDREN 3
        # Maximum requests before a process is stopped and a new one is launched
        #DefaultInitEnv PHP_FCGI_MAX_REQUESTS 5000
        <Location /fcgid-bin/>
        SetHandler fcgid-script
        Options +ExecCGI
    </Location>
</IfModule>

```

`/etc/httpd/conf/httpd.conf` 파일을 편집하여 actions 모듈을 활성화한다:

```
LoadModule actions_module modules/mod_actions.so

```

다음을 추가해준다.

```
LoadModule fcgid_module modules/mod_fcgid.so
Include conf/extra/httpd-mpm.conf
Include conf/extra/php-fcgid.conf

```

**Note:**

아래 코드는 더이상 필요하지 않기 때문에 만약 `httpd.conf` 파일에 추가했다면 삭제하도록 한다.

```
LoadModule php7_module modules/libphp7.so
Include conf/extra/php7_module.conf

```

`httpd.service`을 재시작한다.

#### MySQL/MariaDB

[PHP#MySQL/MariaDB](/index.php/PHP#MySQL.2FMariaDB "PHP") 위키페이지의 설명서를 따른다.

설정이 완료되면 `httpd.service`를 재시작한다.

### HTTP2

HTTP/2 지원을 위해서는 [nghttp2](https://www.archlinux.org/packages/?name=nghttp2) 패키지를 설치해야 한다.

설치 후에 `httpd.conf` 파일에서 다음 줄의 주석을 해제한다:

```
LoadModule http2_module modules/mod_http2.so

```

다음 줄을 추가한다:

```
Protocols h2 http/1.1

```

더 자세한 내용은 [mod_http2](https://httpd.apache.org/docs/2.4/mod/mod_http2.html) 문서를 참고한다.

## 문제 해결

### 아파치 서버 상태와 로그

[systemctl](/index.php/Systemctl "Systemctl")를 통해 아파치 데몬의 현재 상태를 확인할 수 있다.

아파치 로그파일은 `/var/log/httpd/`에서 찾을 수 있다.

### Error: PID file /run/httpd/httpd.pid not readable (yet?) after start

`httpd.conf`파일에서 `unique_id_module` 부분을 주석처리한다: `#LoadModule unique_id_module modules/mod_unique_id.so`

### Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.

`httpd.service`가 `php7_module`을 로딩할 때 다음과 같은 에러메세지가 출력되는 경우:

```
Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.

```

설정파일에서 다음과 같이 `mpm_event_module`를 `mpm_prefork_module`로 바꿔준다:

 `/etc/httpd/conf/httpd.conf` 
```
~~LoadModule mpm_event_module modules/mod_mpm_event.so~~
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

그리고나서, `httpd.service`를 재시작한다.

### AH00534: httpd: Configuration error: No MPM loaded.

아파치를 최신 버전으로 업그레이드하면서 나타나는 문제다. 이는 최신 아파치 설정 부분에서 변경된 부분이 이전의 설정파일에 반영되지 않았기 때문에 생기는 문제로서 다음 부분의 주석을 해제해주면 해결이 가능하다.

 `/etc/httpd/conf/httpd.conf` 
```
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

이 후에도 계속해서 에러메세지가 출력된다면 [위에서 언급된 부분](#Apache_is_running_a_threaded_MPM.2C_but_your_PHP_Module_is_not_compiled_to_be_threadsafe.)을 참고한다.

### Changing the max_execution_time in php.ini has no effect

`php.ini`파일에서 `max_execution_time`의 값을 30(초)보다 큰 값으로 변경하면 30초 후에 아파치로부터 `503 Service Unavailable`라는 응답을 받게 된다. 이를 해결하기 위해서는 http 설정에서 `<FilesMatch \.php$>` 부분 이전에 `ProxyTimeout` 디렉티브를 추가해주면 해결 가능하다:

 `/etc/httpd/conf/httpd.conf` 
```
ProxyTimeout 300

```

변경 후에는 `httpd.service`를 재시작한다.

## 참조

*   [Apache Official Website](http://www.apache.org/)
*   [Tutorial for creating self-signed certificates](http://www.akadia.com/services/ssh_test_certificate.html)
*   [Apache Wiki Troubleshooting](http://wiki.apache.org/httpd/CommonMisconfigurations)