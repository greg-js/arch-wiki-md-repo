[Citrix Receiver](https://en.wikipedia.org/wiki/Citrix_Receiver "wikipedia:Citrix Receiver") is the client component of [XenDesktop](https://en.wikipedia.org/wiki/XenDesktop "wikipedia:XenDesktop") (desktop virtualization software) and [XenApp](https://en.wikipedia.org/wiki/XenApp "wikipedia:XenApp") (application virtualization software), developed by [Citrix Systems](https://en.wikipedia.org/wiki/Citrix_Systems "wikipedia:Citrix Systems").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Google Chromium](#Google_Chromium)
    *   [1.2 Manual installation](#Manual_installation)
*   [2 TLS/SSL Certificates](#TLS/SSL_Certificates)
*   [3 Audio Support](#Audio_Support)
*   [4 Troubleshooting](#Troubleshooting)

## Installation

[Install](/index.php/Install "Install") the [icaclient](https://aur.archlinux.org/packages/icaclient/) package.

SSL connections are supported by default in this packages. Also Firefox plugin will be installed by default as well as the wfica.desktop file. That way Arch knows how to open ica files.

#### Google Chromium

If you have problems launching Citrix applications with Chromium, just go to `chrome://extensions` and disable "Citrix Receiver for Linux".

Next, create `/usr/share/applications/wfica.desktop` (Exec path may vary based on package installed):

```
[Desktop Entry]
Name=Citrix ICA client
Comment="Launch Citrix applications from .ica files"
Categories=Network;
Exec=/opt/Citrix/ICAClient/wfica
Terminal=false
Type=Application
NoDisplay=true
MimeType=application/x-ica;
```

Now `xdg-open` will handle .ica extensions using `/opt/Citrix/ICAClient/wfica`.

Note: if you are running Xfce and Chromium is opening the .ica files in the wrong application (e.g. a text editor), make sure you have `xorg-xprop` installed.

#### Manual installation

*   **Step 1.** Download Citrix Receiver from [here](https://www.citrix.com/downloads/citrix-receiver/linux/receiver-for-linux-latest.html). Choose the latest version of the x86_64 tarball.

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
# cp /etc/ca-certificates/extracted/tls-ca-bundle.pem .
# awk 'BEGIN {c=0;} /BEGIN CERT/{c++} { print > "cert." c ".pem"}' < tls-ca-bundle.pem

```

	You may also need to download your CA's intermediate certificates and store them in the same directory.

	Changes to your certificate directory will likely require rehashing links for openssl to find them properly. Skipping this step might result in Citrix still giving certificate errors. To do this, use this command (borrowed from [[1]](https://help.ubuntu.com/community/CitrixICAClientHowTo#A5._Add_more_SSL_certificates))

	 `# c_rehash /opt/Citrix/ICAClient/keystore/cacerts/` 

## Audio Support

Citrix Receiver uses [ALSA](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture "wikipedia:Advanced Linux Sound Architecture"). If you use [Pulse Audio](https://en.wikipedia.org/wiki/Pulse_Audio "wikipedia:Pulse Audio"), install [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa).

To get audio input into Citrix Receiver, in `~/.ICAClient/wfclient.ini`, add `AllowAudioInput=True` anywhere in the `[WFClient]` section.

## Troubleshooting

If you have issues opening a Citrix connection under Firefox you may need to set the Citrix Receiver plugin to 'Always Activate' under the Firefox Add-ons Manager plugin settings.

If you have cursor alignment issues under Citrix and you have multiple displays connected to your machine you may need to disable all but one when using Citrix.

If you have sticky Control Ctrl key issues after logging to session you may resolve it using this [guide](http://looselytyped.blogspot.com/2014/08/fixing-sticky-control-key-issues-with.html)