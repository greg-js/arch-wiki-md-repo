이 문서는 델루지의 데몬으로 어떻게 토렌트를 이용 할 수 있는지 설명합니다.

## Contents

*   [1 설치](#.EC.84.A4.EC.B9.98)
*   [2 설정](#.EC.84.A4.EC.A0.95)
    *   [2.1 데몬과 web ui](#.EB.8D.B0.EB.AA.AC.EA.B3.BC_web_ui)
    *   [2.2 SSL](#SSL)

## 설치

설치는 간단합니다. 아래와 같이 deluge 패키지를 설치 해주면 끝납니다.

```
# pacman -S deluge

```

web ui 사용을 위해서 **python-mako** 패키지를 필요로 합니다 :

```
# pacman -S python-mako

```

gtk ui를 사용시에는 **pygtk** and **librsvg** 패키지가 추가로 필요 합니다 :

```
# pacman -S pygtk librsvg

```

## 설정

### 데몬과 web ui

The default user for deluged, the Deluge daemon, is "deluge". You can change this in `/etc/conf.d/deluged`. Of course, the user needs to exist. In the case of the default "deluge" user, no manual user creation is necessary as the package script has done that for you.

The rest of this guide will assume you use the default "deluge" user. This user's default home dir and therefore its configuration location is in */srv/deluge*. This should be fine under most circumstances. Note that this is NOT the default download location, it only holds its configuration and ssl certificates. You will be able to change all other options later on once you get a client working.

Next, start the daemon to generate its default configuration in its homedir:

```
# /etc/rc.d/deluged start

```

Finally, start the web ui:

```
# /etc/rc.d/deluge-web start

```

and login in on *[http://deluge-machine:8112](http://deluge-machine:8112)*. Where 'deluge-machine' is name of your deluge server or its private or public IP address. When asked for a password, enter "deluge" as it's the default password.

The preferences in the web ui should be rather self explanatory and the first obvious thing to do is to change your password.

As usual, you should add the daemons to your `/etc/rc.conf`:

```
DAEMONS=( ... network deluged deluge-web ... )

```

Just make sure your network connection is up at the time you start either of those Deluge daemons.

### SSL

In case you want SSL for the web ui, you need to generate a new cert/key set. To do this, first stop the web ui:

```
# /etc/rc.d/deluge-web stop

```

then go to */srv/deluge/.config/deluge/ssl/* and issue:

```
# openssl req -new -x509 -nodes -out deluge.cert.pem -keyout deluge.key.pem

```

Next you need to edit `/srv/deluge/.config/deluge/web.conf` and change the **pkey** and **cert** configuration directives to use your new self-signed certificates and also enable SSL:

```
...
"pkey": "ssl/deluge.key.pem",
...
"cert": "ssl/deluge.cert.pem",
...
"https": true,

```

Afterwards just start the web ui again and you should be good to go:

```
# /etc/rc.d/deluge-web start

```