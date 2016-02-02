# Citrix

## Contents

*   [1 Install from AUR](#Install_from_AUR)
    *   [1.1 Install Package](#Install_Package)
    *   [1.2 Google Chromium](#Google_Chromium)
*   [2 Manual Install](#Manual_Install)
    *   [2.1 Citrix Receiver (icaclient) Installation](#Citrix_Receiver_.28icaclient.29_Installation)
*   [3 TLS/SSL Certificates](#TLS.2FSSL_Certificates)

## Install from AUR

#### Install Package

[icaclient](https://aur.archlinux.org/packages/icaclient/) x86_64

SSL connections are supported by default in this packages. Also Firefox plugin will be installed by default as well as the wfica.desktop file. That way Arch knows how to open ica files.

#### Google Chromium

If you have problems launching Citrix applications with Chromium, just go to `about:plugins` and disable "Citrix Receiver for Linux".

Next, create `/usr/share/applications/wfica.desktop` (Exec path may vary based on package installed):

```
[Desktop Entry]
Name=Citrix ICA client
Comment="Launch Citrix applications from .ica files"
Categories=Network;
Exec=/usr/bin/wfica
Terminal=false
Type=Application
NoDisplay=true
MimeType=application/x-ica;
```

Now `xdg-open` will handle .ica extensions using `/usr/bin/wfica`.

Note: if you are running Xfce and Chromium is opening the .ica files in the wrong application (e.g. a text editor), make sure you have `xorg-xprop` installed.

## Manual Install

#### Citrix Receiver (icaclient) Installation

*   **Step 0\. 64-bit Arch systems only - install 32-bit libs:**

from Arch repositories: openmotif, lib32-libxmu, printproto, nspluginwrapper, lib32-alsa-lib, lib32-gcc-libs, lib32-libxft, lib32-gtk2, lib32-libxdamage, lib32-libpng12\. From AUR: lib32-libxp, lib32-libxpm, lib32-libxaw, lib32-openmotif

Citrix has released a 64-bit version of the Citrix Receiver. You might try this version first (Navigate to [[1]](http://www.citrix.com/downloads/citrix-receiver/linux.html), select the newest version, go to section "For 64-bit Systems")

*   **Step 1.** Download Citrix Receiver It can be found [here](http://www.citrix.com/downloads/citrix-receiver/linux.html). Choose the latest version of the x86 client in the .tar.gz format.

*   **Step 2.** Unpack the archive:

```
# tar zxvf en.linuxx86.tar.gz
./
./PkgId
./install.txt
./eula.txt
./readme.txt
./setupwfc
./linuxx86/
./linuxx86/hinst
./linuxx86/linuxx86.cor/
./linuxx86/linuxx86.cor/nls/
./linuxx86/linuxx86.cor/nls/en/
./linuxx86/linuxx86.cor/nls/en/UTF-8/
./linuxx86/linuxx86.cor/nls/en/UTF-8/Wfica
./linuxx86/linuxx86.cor/nls/en/UTF-8/Wfcmgr
... many more files ...

```

*   **Step 3.** Run setupwfc: `# ./setupwfc` (Follow all instructions prompted by setupwfc.)
*   **Step 4.** (Applies only for Firefox integration:)

The setup program should have made appropriate links to the "Citrix Receiver for Linux" plugin. You can check this as such:

```
# find / -name npica.so
/opt/Citrix/ICAClient/npica.so

```

Or you can check if your browser loads the plugin, in Firefox this can be done by typing "about:plugins" in the address bar. If you have a 64-bit version of Firefox, the plugin will not be loaded. You can check below what to do.

Create missing links as such:

 `# ln -s /opt/Citrix/ICAClient/npica.so /usr/lib/mozilla/plugins/` 

*   **Step 6.** Restart your browser

At this point, everything should work, including wfcmgr. In the case of Opera, integration should be automatic. The ICAClient will automatically be launched whenever you try to access a citrix-based application from either Firefox or Opera.

**Note:** If for some reason firefox prompts you for which application to use when opening a citrix-based application, use `/opt/Citrix/ICAClient/wfica`

## TLS/SSL Certificates

Because ICAClient uses SSL you may need a security certificate to connect to the server, check with the server administrator. If there is a certificate download and place it in `/usr/lib/ICAClient/keystore/cacerts/`.

You may then receive the error `You have not chosen to trust the issuer of the server's security certificate. (SSL Error 61)`.

There may be several reasons for this:

	You do not have the root Certificate Authority (CA) certificates.

	These are already installed on most systems, they are part of the core package [ca-certificates](https://www.archlinux.org/packages/?name=ca-certificates), but they are not where ICAClient looks for them. Copy the certificates from `/etc/ssl/certs/` to `/usr/lib/ICAClient/keystore/cacerts/`. For Citrix versions before 13.1, run the following command as root:

	 `# ln -sf /etc/ssl/certs/* /opt/Citrix/ICAClient/keystore/cacerts/` 

	Since versions 13.1, Citrix needs the certificates in separate files. You need to run the following commands as root:

```
# cd /opt/Citrix/ICAClient/keystore/cacerts/
# cp /etc/ssl/certs/ca-certificates.crt .
# awk 'BEGIN {c=0;} /BEGIN CERT/{c++} { print > "cert." c ".pem"}' < ca-certificates.crt

```

	You may also need to download your CA's intermediate certificates and store them in the same directory.

	Changes to your certificate directory will likely require rehashing links for openssl to find them properly. Skipping this step might result in Citrix still giving certificate errors. To do this, use this command (borrowed from [[2]](https://help.ubuntu.com/community/CitrixICAClientHowTo#A5._Add_more_SSL_certificates))

	 `# c_rehash /opt/Citrix/ICAClient/keystore/cacerts/` 

	Your server is using a certificate with a SHA-2 hash for the Signature Algorithm.

	Microsoft has mandated that any certificates with an expiry date of 2017 or later must use a SHA-2 hash[[3]](http://www.p2vme.com/2014/02/sha2-certificates-and-citrix-receiver.html). You may either:

1.  Upgrade your client to 13.1 or later. Citrix now supports SHA-2 hashes in the ICA client version 13.1.0.285639.
2.  Contact your CA and have your certificate re-keyed with a SHA-1 hash.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Citrix&oldid=409499](https://wiki.archlinux.org/index.php?title=Citrix&oldid=409499)"