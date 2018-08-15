Related articles

*   [HTTP tunneling](/index.php/HTTP_tunneling "HTTP tunneling")

A proxy is "an interface for a service, especially for one that is remote, resource-intensive, or otherwise difficult to use directly". Source: [Proxy - Wiktionary](http://en.wiktionary.org/wiki/proxy).

## Contents

*   [1 Environment variables](#Environment_variables)
    *   [1.1 Keep proxy through sudo](#Keep_proxy_through_sudo)
    *   [1.2 Automation with network managers](#Automation_with_network_managers)
*   [2 About libproxy](#About_libproxy)
*   [3 Web Proxy Options](#Web_Proxy_Options)
    *   [3.1 Simple Proxy with SSH](#Simple_Proxy_with_SSH)
*   [4 Using a SOCKS proxy](#Using_a_SOCKS_proxy)
    *   [4.1 curl and pacman](#curl_and_pacman)
*   [5 Proxy settings on GNOME3](#Proxy_settings_on_GNOME3)
*   [6 Microsoft NTLM proxy](#Microsoft_NTLM_proxy)
    *   [6.1 Configuration](#Configuration)
    *   [6.2 Usage](#Usage)

## Environment variables

Some programs, such as [wget](/index.php/Wget "Wget") and (used by [pacman](/index.php/Pacman "Pacman")) *curl*, use environment variables of the form "protocol_proxy" to determine the proxy for a given protocol (e.g. HTTP, FTP, ...).

Below is an example on how to set these variables in a shell:

```
 export http_proxy=http://10.203.0.1:5187/
 export https_proxy=$http_proxy
 export ftp_proxy=$http_proxy
 export rsync_proxy=$http_proxy
 export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"

```

Some programs look for the all caps version of the environment variables.

If the proxy environment variables are to be made available to all users and all applications, the above mentioned export commands may be added to a script, say "proxy.sh" inside /etc/profile.d/. The script has to be then made executable. This method is helpful while using a Desktop Environment like [Xfce](/index.php/Xfce "Xfce") which does not provide an option for proxy configuration. For example, [Chromium](/index.php/Chromium "Chromium") browser will make use of the variables set using this method while running XFCE.

Alternatively, there's a tool named [ProxyMan](https://github.com/himanshub16/ProxyMan) which claims to configure system-wide proxy settings easily. It also handles proxy configurations of other software like [git], [npm], Dropbox, etc. The project is inspired from Alan Pope's idea of making a script.

Alternatively you can automate the toggling of the variables by adding a function to your .bashrc (thanks to Alan Pope for original script idea)

```
function proxy_on() {
    export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"

    if (( $# > 0 )); then
        valid=$(echo $@ | sed -n 's/\([0-9]\{1,3\}.\)\{4\}:\([0-9]\+\)/&/p')
        if [[ $valid != $@ ]]; then
            >&2 echo "Invalid address"
            return 1
        fi

        export http_proxy="http://$1/" \
               https_proxy=$http_proxy \
               ftp_proxy=$http_proxy \
               rsync_proxy=$http_proxy
        echo "Proxy environment variable set."
        return 0
    fi

    echo -n "username: "; read username
    if [[ $username != "" ]]; then
        echo -n "password: "
        read -es password
        local pre="$username:$password@"
    fi

    echo -n "server: "; read server
    echo -n "port: "; read port
    export http_proxy="http://$pre$server:$port/" \
           https_proxy=$http_proxy \
           ftp_proxy=$http_proxy \
           rsync_proxy=$http_proxy \
           HTTP_PROXY=$http_proxy \
           HTTPS_PROXY=$http_proxy \
           FTP_PROXY=$http_proxy \ 
           RSYNC_PROXY=$http_proxy
}

function proxy_off(){
    unset http_proxy https_proxy ftp_proxy rsync_proxy \
          HTTP_PROXY HTTPS_PROXY FTP_PROXY RSYNC_PROXY
    echo -e "Proxy environment variable removed."
}

```

Omit username or password if they are not needed.

As an alternative, you may want to use the following script. Change the strings "YourUserName", "ProxyServerAddress:Port", "LocalAddress" and "LocalDomain" to match your own data, then edit your `~/.bashrc` to include the edited functions. Any new bash window will have the new functions. In existing bash windows, type `source ~/.bashrc`. You may prefer to put function definitions in a separate file like `functions` then add `source functions` to `.bashrc` instead of putting everything in `.bashrc`. You may also want to change the name "myProxy" into something short and easy to write.

```
 #!/bin/bash

 assignProxy(){
   PROXY_ENV="http_proxy ftp_proxy https_proxy all_proxy HTTP_PROXY HTTPS_PROXY FTP_PROXY ALL_PROXY"
   for envar in $PROXY_ENV
   do
      export $envar=$1
   done
   for envar in "no_proxy NO_PROXY"
   do
      export $envar=$2
   done
 }

 clrProxy(){
    PROXY_ENV="http_proxy ftp_proxy https_proxy all_proxy HTTP_PROXY HTTPS_PROXY FTP_PROXY ALL_PROXY"
    for envar in $PROXY_ENV
    do
       unset $envar
    done
 }

 myProxy(){
   user=YourUserName
   read -p "Password: " -s pass &&  echo -e " "
   proxy_value="http://$user:$pass@ProxyServerAddress:Port"
   no_proxy_value="localhost,127.0.0.1,LocalAddress,LocalDomain.com"
   assignProxy $proxy_value $no_proxy_value
 }

```

### Keep proxy through sudo

If the proxy environment variables are set for the user only (say, from manual commands or .bashrc) they will get lost when running commands with [sudo](/index.php/Sudo "Sudo") (or when programs use sudo internally).

A way to prevent that is to add the following line to the sudo configuration file (accessible with visudo) :

```
Defaults env_keep += "http_proxy https_proxy ftp_proxy"

```

You may also add any other environment variable, like rsync_proxy, or no_proxy.

### Automation with network managers

*   [NetworkManager](/index.php/NetworkManager "NetworkManager") cannot change the environment variables.
*   [netctl](/index.php/Netctl "Netctl") could set-up these environment variables but they would not be seen by other applications as they are not child of netctl.

## About libproxy

[libproxy](http://code.google.com/p/libproxy/) (which is available in the extra repository) is an abstraction library which should be used by all applications that want to access a network resource. It still is in development but could lead to a unified and automated handling of proxies in GNU/Linux if widely adopted.

The role of libproxy is to read the proxy settings from different sources and make them available to applications which use the library. The interesting part with libproxy is that it offers an implementation of the [Web Proxy Autodiscovery Protocol](https://en.wikipedia.org/wiki/Web_Proxy_Autodiscovery_Protocol "wikipedia:Web Proxy Autodiscovery Protocol") and an implementation of [Proxy Auto-Config](https://en.wikipedia.org/wiki/Proxy_auto-config "wikipedia:Proxy auto-config") that goes with it.

The `/usr/bin/proxy` binary takes URL(s) as argument(s) and returns the proxy/proxies that could be used to fetch this/these network resource(s).

**Note:** the version 0.4.11 does not support http_proxy='wpad:' because `{ pkg-config 'mozjs185 >= 1.8.5'; }` fails .

As of 06/04/2009 libproxy is required by libsoup. It is then indirectly used by the [midori](https://www.archlinux.org/packages/?name=midori) browser.

## Web Proxy Options

*   [Squid](/index.php/Squid "Squid") is a very popular caching/optimizing proxy
*   [Privoxy](/index.php/Privoxy "Privoxy") is an anonymizing and ad-blocking proxy
*   For a simple proxy, ssh with port forwarding can be used

### Simple Proxy with SSH

Connect to a server (HOST) on which you have an account (USER) as follows

```
ssh -D PORT USER@HOST

```

For PORT, choose some number which is not an IANA registered port. This specifies that traffic on the local PORT will be forwarded to the remote HOST. ssh will act as a [SOCKS](https://en.wikipedia.org/wiki/SOCKS "wikipedia:SOCKS") server. Software supporting SOCKS proxy servers can simply be configured to connect to PORT on localhost.

## Using a SOCKS proxy

There are two cases:

*   the application you want to use handles [SOCKS5](https://en.wikipedia.org/wiki/SOCKS#SOCKS5 "wikipedia:SOCKS") proxies (for example [Firefox](/index.php/Firefox "Firefox")), then you just have to configure it to use the proxy.
*   the application you want to use does not handle SOCKS proxies, then you can try to use [tsocks](https://www.archlinux.org/packages/?name=tsocks) or [proxychains-ng](https://www.archlinux.org/packages/?name=proxychains-ng).

In Firefox, you can use the SOCKS proxy in the menu Preferences > Network > Settings. Choose "Manual Proxy Configuration", and set the SOCKS Host (and only this one, make sure the other fields, such as HTTP Proxy or SSL Proxy are left empty). For example, if a SOCKS5 proxy is running on localhost port 8080, put "127.0.0.1" in the SOCKS Host field, "8080" in the Port field, and validate.

If using *proxychains-ng*, the configuration takes place in `/etc/proxychains.conf`. You may have to uncomment the last line (set by default to use [Tor](/index.php/Tor "Tor")), and replace it with the parameters of the SOCKS proxy. For example, if you are using the same SOCKS5 proxy as above, you will have to replace the last line by:

```
socks5 127.0.0.1 8080

```

Then, *proxychains-ng* can be launched with

```
proxychains <program>

```

Where <program> can be any program already installed on your system (e.g. xterm, gnome-terminal, etc).

If using *tsocks*, the configuration takes place in `/etc/tsocks.conf`. See [tsocks.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tsocks.conf.5) for the options. An example minimum configuration looks like this:

 `/etc/tsocks.conf` 
```
server = 127.0.0.1
server_port = 8080
server_type = 5
```

### curl and pacman

You may set the `all_proxy` environment variable to let curl and pacman (which uses curl) use your socks5 proxy:

 `$ export all_proxy="socks5://your.proxy:1080"` 

## Proxy settings on GNOME3

Some programs like [Chromium](/index.php/Chromium "Chromium") prefer to use the settings stored by gnome. These settings can be modified through the gnome-control-center front end and also through gsettings.

```
gsettings set org.gnome.system.proxy mode 'manual' 
gsettings set org.gnome.system.proxy.http host 'proxy.localdomain.com'
gsettings set org.gnome.system.proxy.http port 8080
gsettings set org.gnome.system.proxy.ftp host 'proxy.localdomain.com'
gsettings set org.gnome.system.proxy.ftp port 8080
gsettings set org.gnome.system.proxy.https host 'proxy.localdomain.com'
gsettings set org.gnome.system.proxy.https port 8080
gsettings set org.gnome.system.proxy ignore-hosts "['localhost', '127.0.0.0/8', '10.0.0.0/8', '192.168.0.0/16', '172.16.0.0/12' , '*.localdomain.com' ]"

```

This configuration can also be set to automatically execute when [Network Manager](/index.php/NetworkManager#Proxy_settings "NetworkManager") connects to specific networks , by using the package [proxydriver](https://aur.archlinux.org/packages/proxydriver/) from the [AUR](/index.php/AUR "AUR")

## Microsoft NTLM proxy

In a Windows network, NT LAN Manager (NTLM) is a suite of Microsoft security protocols which provides authentication, integrity, and confidentiality to users.

[cntlm](https://aur.archlinux.org/packages/cntlm/) from the [AUR](/index.php/AUR "AUR") stands between your applications and the NTLM proxy, adding NTLM authentication on-the-fly. You can specify several "parent" proxies and Cntlm will try one after another until one works. All authenticated connections are cached and reused to achieve high efficiency.

```
(NTLM PROXY IP:PORT + CREDENTIALS + OTHER INFO) -----> **(127.0.0.1:PORT)**

```

### Configuration

Change settings in `/etc/cntlm.conf` as needed, except for the password. Then run:

```
$ cntlm -H

```

This will generate encrypted password hashes according to your proxy hostname, username and password.

**Warning:** [ettercap](https://www.archlinux.org/packages/?name=ettercap) can easily sniff your password over LAN when using plain-text passwords instead of encrypted hashes.

Edit `/etc/cntlm.conf` again and include all three generated hashes, then [enable](/index.php/Enable "Enable") `cntlm.service`.

To test settings, run:

```
$ cntlm -v

```

### Usage

Use `127.0.0.1:<port>` or `localhost:<port>` as a proxy adress. `<port>` matches the `Listen` parameter in `/etc/cntlm.conf`, which by default is `3128`.