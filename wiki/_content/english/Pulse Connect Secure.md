[Pulse Connect Secure](https://www.pulsesecure.net/connect-secure) (PCS), previously known as Juniper SSL VPN, is a commercial VPN solution targeted at businesses.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 AUR](#AUR)
    *   [1.2 OpenConnect](#OpenConnect)
*   [2 Third-party scripts](#Third-party_scripts)
    *   [2.1 JNC](#JNC)
    *   [2.2 MSJNC](#MSJNC)
        *   [2.2.1 Instructions for 64-bit users](#Instructions_for_64-bit_users)
        *   [2.2.2 Automatic installation of ncsvc using msjnc](#Automatic_installation_of_ncsvc_using_msjnc)
        *   [2.2.3 Manual installation of msjnc](#Manual_installation_of_msjnc)
        *   [2.2.4 Note regarding Server/URL](#Note_regarding_Server.2FURL)
    *   [2.3 JVPN](#JVPN)
        *   [2.3.1 Installation](#Installation_2)
        *   [2.3.2 Running as root](#Running_as_root)
        *   [2.3.3 Running as a regular user](#Running_as_a_regular_user)
*   [3 Workarounds](#Workarounds)
    *   [3.1 64-bit Java (workaround 1)](#64-bit_Java_.28workaround_1.29)
    *   [3.2 64-bit Java (workaround 2)](#64-bit_Java_.28workaround_2.29)
    *   [3.3 Motif and libstdc++-libc6.2-2.so.3](#Motif_and_libstdc.2B.2B-libc6.2-2.so.3)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Password incorrect](#Password_incorrect)
    *   [4.2 Login succeeds but Network Connect will not launch](#Login_succeeds_but_Network_Connect_will_not_launch)
    *   [4.3 Network Connect launched but the VPN does not work](#Network_Connect_launched_but_the_VPN_does_not_work)
    *   [4.4 Network Connect launched and a configuration error message is displayed](#Network_Connect_launched_and_a_configuration_error_message_is_displayed)
    *   [4.5 ncapp.error Failed to connect/authenticate with IVE.](#ncapp.error_Failed_to_connect.2Fauthenticate_with_IVE.)
    *   [4.6 ncsvc and kernel versions 3.19 and 4.5 to 4.9](#ncsvc_and_kernel_versions_3.19_and_4.5_to_4.9)
    *   [4.7 Unauthorized new route has been added, disconnecting](#Unauthorized_new_route_has_been_added.2C_disconnecting)

## Installation

### AUR

[Install](/index.php/Install "Install") the [pulse-secure](https://aur.archlinux.org/packages/pulse-secure/) package and run the service:

```
$ pulsesvc -h <hostname> -Port <port number> -u <username> -realm <realm> -Url <login URL>

```

Note that the login URL is different from the URL used in browsers. Check "Note regarding Server/URL" section below.

To use the `pulseUi` GUI client you need to additionally install [webkitgtk](https://aur.archlinux.org/packages/webkitgtk/). In the GUI client, the URL should be same as that used in browsers.

### OpenConnect

The [OpenConnect](/index.php/OpenConnect "OpenConnect") VPN client also supports Pulse Connect Secure. See the [initial announcement](http://lists.infradead.org/pipermail/openconnect-devel/2015-January/002628.html) for more details.

To use, install [openconnect](https://www.archlinux.org/packages/?name=openconnect). If your Juniper VPN setup doesn't require any input after connecting you can use this command in order to connect

```
# openconnect --juniper https://vpn.example.com/

```

If you want [NetworkManager](/index.php/NetworkManager "NetworkManager") support, install [networkmanager-openconnect](https://www.archlinux.org/packages/?name=networkmanager-openconnect), or try the latest git version. The VPN connection can be created through the GUI or by using this command:

```
$ nmcli con add type vpn con-name "Connection Name" ifname "*" vpn-type openconnect -- vpn.data "gateway=vpn.example.com,protocol=nc"

```

## Third-party scripts

### JNC

**Note:** In [some cases](http://kb.juniper.net/InfoCenter/index?page=content&id=KB20490&actp=RSS), depending on your corporate policy configuration, you **must** login through the browser. If this is the case, command-line tools (jnc, junipernc) will not work.

1\. Go to your company's VPN site, log in and download/install the Juniper client.

2\. Install [jnc](https://aur.archlinux.org/packages/jnc/). For 64-bit Arch, you will need to install 32-bit packages ([Multilib](/index.php/Multilib "Multilib")), see the [upstream website](http://www.scc.kit.edu/scc/net/juniper-vpn/linux/).

3\. Make a directory for the *.config* file:

```
$ mkdir -p ~/.juniper_networks/network_connect/config

```

4\. Copy and adapt this *.config* file in this directory:

 `~/.juniper_networks/network_connect/config/.config` 
```
host=foo.bar.com
user=username
password=secret
realm= realm with spaces
cafile=/etc/ssl/bar-chain.pem
certfile=
```

	cafile

	ca chain to verify the host certificate

	certfile

	host certificate in DER format. Cafile or certfile must be configured, you can download them from your VPN sign-in page (certificate information, export certificate).

	realm

	You can find out your realm by viewing the page source of your VPN sign-in page: just search for the word realm in it.

5\. Start/stop network connect:

```
$ jnc --nox

```

for use without GUI. To stop the client, execute

```
$ jnc stop

```

### MSJNC

The [Mad Scientist's "msjnc" script](http://mad-scientist.us/juniper.html) requires [gtk2-perl](https://www.archlinux.org/packages/?name=gtk2-perl), [glib-perl](https://www.archlinux.org/packages/?name=glib-perl) and [unzip](https://www.archlinux.org/packages/?name=unzip).

#### Instructions for 64-bit users

[Enable multilib](/index.php/Multilib#Enabling "Multilib") and then [install](/index.php/Install "Install") [lib32-zlib](https://www.archlinux.org/packages/?name=lib32-zlib), [net-tools](https://www.archlinux.org/packages/?name=net-tools), [glib-perl](https://www.archlinux.org/packages/?name=glib-perl), [perl-libwww](https://www.archlinux.org/packages/?name=perl-libwww) and [gtk2-perl](https://www.archlinux.org/packages/?name=gtk2-perl).

Access the the Juniper VPN website you need to use. Log in and allow the installation to attempt and fail (due to non-32 bit Java). You should get an error similar to the following:

```
Setup failed.
Please install 32 bit Java and update alternatives links using update-alternatives command.
For more details, refer KB article KB25230
```

You should now have the file `~/.juniper_networks/ncLinuxApp.jar` present.

However, if `ncLinuxApp.jar` is not downloaded, fetch it manually - see the following example URL: `[https://server/dana-cached/nc/ncLinuxApp.jar](https://server/dana-cached/nc/ncLinuxApp.jar)` (note: you need to log in first).

Then download the [msjnc](https://raw.github.com/madscientist/msjnc/master/msjnc) script, make it executable, and put it in your `PATH`.

#### Automatic installation of ncsvc using msjnc

The first time you launch *msjnc* (before *ncsvc* is installed), it will extract `ncLinuxApp.jar` and prompt for your password in order to install the service. This requires *sudo* to be configured to allow all commands to your user.

After the service is installed to `~/.juniper_networks/network_connect/ncsvc` with suid, create a profile and connect.

#### Manual installation of msjnc

Create these directories:

```
$ mkdir -p ~/.juniper_networks/network_connect
$ mkdir -p ~/.juniper_networks/tmp

```

Extract the software:

```
$ unzip ~/.juniper_networks/ncLinuxApp.jar -d ~/.juniper_networks/tmp

```

Copy `NC.jar` to the `network_connect` directory:

```
$ cp ~/.juniper_networks/tmp/NC.jar ~/.juniper_networks/network_connect

```

Install the service:

```
$ sh ~/.juniper_networks/tmp/installNC.sh ~/.juniper_networks/network_connect

```

Launch *msjnc*, create a profile, and connect.

#### Note regarding Server/URL

For the Server/URL, you may have to provide the URL that processes the login form rather than the login page itself. As an example, one company's login form is on `/dana-na/auth/url_0/welcome.cgi` but the form is actually processed by `/dana-na/auth/url_0/login.cgi`. You may have to inspect the html of the login page to find the form's action attribute.

### JVPN

The [JVPN Perl script](https://github.com/samm-git/jvpn) establishes a Juniper VPN connection and supports the following features:

*   Connection using Host Checker.
*   Automatic download of the required Juniper java and daemon files (ncsvc) when run as root.

#### Installation

[Install](/index.php/Install "Install") the perl dependencies [perl-term-readkey](https://www.archlinux.org/packages/?name=perl-term-readkey) and [perl-lwp-protocol-https](https://www.archlinux.org/packages/?name=perl-lwp-protocol-https). Once you have done so, you must choose whether to run *jvpn* as root (easiest method) or as a regular user and run the steps below accordingly.

#### Running as root

Run the command:

```
# curl -L [https://github.com/samm-git/jvpn/archive/v0.7.0.tar.gz](https://github.com/samm-git/jvpn/archive/v0.7.0.tar.gz) | tar xz

```

The command creates a file `jvpn-0.7.0` in current directory.

Finally, start the script with:

```
# ./jvpn.pl

```

On first run, the script will download all the necessary files

#### Running as a regular user

Use your web browser (no need for 32-bit Java) to connect to the VPN website and download the appropriate software. The files downloaded will be located in `~/.juniper_networks/network_connect/` (even if the VPN connection actually fails).

This step is considered more complex because you have to have a functional Java plugin in your browser (configured with appropriate security settings). During installation of Network Connect, the browser will request a root password to set the setuid flag on *ncsvc* (Juniper daemon).

Then install *jvpn* into the folder by executing the following:

```
$ cd ~/.juniper_networks/network_connect
$ curl -L [https://github.com/samm-git/jvpn/archive/v0.7.0.tar.gz](https://github.com/samm-git/jvpn/archive/v0.7.0.tar.gz) | tar xz --strip-components=1

```

Next, edit `jvpn.ini` (directions are included in the file).

Finally, start the script with the following:

```
$ cd ~/.juniper_networks/network_connect
$ ./jvpn.pl

```

## Workarounds

### 64-bit Java (workaround 1)

**Warning:** These steps are **not recommended**. Updating your JRE will break this workaround and you will have to repeat these steps.

1) Install [bin32-jre](https://aur.archlinux.org/packages/bin32-jre/). Make sure the PKGBUILD installs it to `/opt/bin32-jre`, rather than `/opt/java`, where it will conflict with the 64-bit JRE.

2) Install [jre](https://aur.archlinux.org/packages/jre/).

3) Move the java binary to `java.orig`:

```
# mv /opt/java/jre/bin/java /opt/java/jre/bin/java.orig

```

4) Create a bash script `java` and make it executable:

```
# touch /opt/java/jre/bin/java
# chmod 755 /opt/java/jre/bin/java

```

5) Finally, edit the bash script as per the below:

 `/opt/java/jre/bin/java` 
```
#!/bin/bash
if [ $3x = "NCx" ]
then
    /opt/bin32-jre/jre/bin/java "$@"
else
    /opt/java/jre/bin/java.orig "$@"
fi
```

### 64-bit Java (workaround 2)

**Warning:** Installing non-packaged versions of Java and symlinking libraries into arbitrary locations is **not recommended**.

Another approach is to install an alternative version of Java and link the Java plugin for Firefox manually - this avoids the necessity of using a *chroot* environment. Follow the instructions below:

1.  [install](/index.php/Install "Install") [xterm](https://www.archlinux.org/packages/?name=xterm).
2.  Install a custom 64-bit Java environment from [java.com](http://www.java.com/en/download). Select the Linux x64 version. Once you have decided upon a location for the installation, extract the binary into that location and then mark it executable. Finally, run the binary to install Java.
3.  Install a custom 32-bit Java environment, also from [java.com](http://www.java.com/en/download) but this time, select the Linux (self-extracting) option. Extract the new binary to the same location created above, mark it executable, and run the binary. It will ask you whether you want to replace the files to 32 bit: **Type "A" to overwrite all the 64-bit files with the 32-bit ones.**
4.  Finally, link the library into the required location. The relevant library for Firefox is `libnpjp2.so`. To link it, use the following command `ln -s *location-of-custom-java-installation*/lib/amd64/libnpjp2.so /usr/lib/mozilla/plugins/libnpjp2.so`.

**Note:** Firefox 5 and higher check `/usr/lib/mozilla/plugins` for plugins instead of `~/.mozilla/plugins` which was used in previous versions.

For more information, see the following guide from [Southern Illinois University](https://web.archive.org/web/20120114155121/http://wireless.siu.edu:80/install-ubuntu-64.htm).

### Motif and libstdc++-libc6.2-2.so.3

**Warning:** The steps involved in this section, including using obsolete libraries and symlinking new library names to old are **absolutely not recommended**.

When trying to use Juniper VPN, you may be informed that there are missing libraries. If so, follow the instructions below.

1) Install a Java Runtime Environment (JRE) - see [Java](/index.php/Java "Java").

2) Install [libstdc++296](https://aur.archlinux.org/packages/libstdc%2B%2B296/) which provides the required `libstdc++-libc6.2-2.so.3` library.

3) Install the Motif toolkit. Note that *lesstif* must be used - the [openmotif](https://www.archlinux.org/packages/?name=openmotif) package provides a version of Motif that is too recent. Specifically, it provides `libXm.so.4` instead of `libXm.so.3`.

4) Then create symlinks in order to be able to use lesstif as if it is official Motif - see the reference below.

5) Install [xterm](https://www.archlinux.org/packages/?name=xterm) - the installation uses xterm to ask for the root password.

6) Next, run: `modprobe tun` as root. You will need to do this every time before you connect. As such, you might want to setup the tun module to be autoloaded at startup.

7) Finally, head over to your VPN portal page and initiate the connection by clicking on *Network Connect*.

For more information see: [Gentoo Wiki Archives](https://web.archive.org/web/20151215041949/http://www.gentoo-wiki.info/HOWTO_Juniper_SSL_Network_Connect_VPN)

## Troubleshooting

### Password incorrect

If your username and password are correct but the system reports that they are incorrect, that means the POST request to the Juniper IVE box failed.

The [Tamper Data](https://addons.mozilla.org/en-US/firefox/addon/966) addon for Firefox can be used to debug. Try changing the fields in the headers.

Note that Juniper IVE does not support UTF-8\. The `intl.charset.default` setting in `about:config` for Firefox is UTF-8, causing a POST request to have only UTF-8 in the charset. Setting it to `ISO-8859-1` might fix the problem. Also double check the `intl.accept_charsets` Firefox setting. Using UTF-8, Chinese and European charsets is possible but ensure you have `ISO-8859-1` as a fallback. Note that you can use the Tamper Data addon to make sure you really are accepting `ISO-8859-1` in the HTTP header.

Finally, ensure that the useragent is `Firefox`, not `Bon Echo`. You may need to change this under `general.useragent.extra.firefox` in `about:config`.

### Login succeeds but Network Connect will not launch

1.  Firstly, verify your Java installation.
2.  Then navigate to `~/.juniper_networks/network_connect`.
3.  Check that `ncsvc` is setuid root. Fix it if not.
4.  Run `ldd ncsvc` and see if there are any missing libraries.
5.  Follow the instructions from the [Juniper forum](http://www.juniperforum.com/index.php/topic,2043.0.html) to run it from command line. Use the `-L 5` switch to log everything and use *strace* as root. Also try consulting `ncsvc.log` for any possible errors.

### Network Connect launched but the VPN does not work

Run `ip route` to to check if the route is present. Network connect has a diagnosis tool in the GUI. You can also checks the logs (also available in the GUI).

**Note:** `/etc/resolv.conf` will periodically get overwritten by DHCPCD so your VPN will stop working eventually. If that happens, just restart Network Connect. You might also wish to save your `/etc/resolv.conf` file so that your VPN settings can be easily restored. As of 2007, there is no known solution to the problem but there is a bug report on Red Hat Bugzilla.

### Network Connect launched and a configuration error message is displayed

Check that you have [net-tools](https://www.archlinux.org/packages/?name=net-tools) installed.

### ncapp.error Failed to connect/authenticate with IVE.

See [this post](http://ubuntuforums.org/showthread.php?p=12127450#post12127450) on the Ubuntu forums. Note that in some cases, the policy will not permit a connection initiated from the command line. Instead, you have to install both [bin32-jre](https://aur.archlinux.org/packages/bin32-jre/) and [bin32-firefox](https://aur.archlinux.org/packages/bin32-firefox/) and authenticate through the browser.

### ncsvc and kernel versions 3.19 and 4.5 to 4.9

Juniter VPN does not support [linux](https://www.archlinux.org/packages/?name=linux) 3.19\. See [UNIXgr](http://www.unixgr.com/juniper-ncsvc-and-linux-3-19/).

There are also issues with [linux](https://www.archlinux.org/packages/?name=linux) versions 4.5 to 4.9 (and probably later versions too). See [Bug 121131 on the Kernel bug tracker](https://bugzilla.kernel.org/show_bug.cgi?id=121131) for more information. There are two ways to work around this issue:

*   [Downgrade](/index.php/Downgrade "Downgrade") to version 4.4, or [install](/index.php/Install "Install") [linux-lts](https://www.archlinux.org/packages/?name=linux-lts).
*   According to a comment on the [kernel bugzilla](https://bugzilla.kernel.org/show_bug.cgi?id=121131#c24) disabling router solicitations for IPv6 and reconnecting will also solve the issue. This can be done with the following command:

```
# echo 0 > /proc/sys/net/ipv6/conf/default/router_solicitations

```

	To make this setting automatically on boot time use [systemd-tmpfiles](/index.php/Systemd#Temporary_files "Systemd"):

 `/etc/tmpfiles.d/disable-router-solicitations.conf`  `w /proc/sys/net/ipv6/conf/default/router_solicitations - - - - 0` 

### Unauthorized new route has been added, disconnecting

When using the [pulse-secure](https://aur.archlinux.org/packages/pulse-secure/) client, VPN may not work with [connman](https://www.archlinux.org/packages/?name=connman) due to conflicting routing table strategies. Check `~/.pulse_secure/pulse/pulsesvc.log` for such messages:

```
rmon.error Unauthorized new route to x.x.x.x/y.y.y.y has been added (conflicts with our route to z.z.z.z), disconnecting (routemon.cpp:598)

```

If this is the case, using [NetworkManager](/index.php/NetworkManager "NetworkManager") instead can fix the issue.