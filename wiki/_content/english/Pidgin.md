From the project [home page](http://www.pidgin.im/): "Pidgin is an easy to use and free chat client used by millions. Connect to AIM, MSN, Yahoo, and more chat networks all at once."

## Contents

*   [1 Installation](#Installation)
*   [2 Spellcheck](#Spellcheck)
*   [3 Sound fix](#Sound_fix)
*   [4 Browser error](#Browser_error)
*   [5 QIP encoding bug](#QIP_encoding_bug)
*   [6 ICQ](#ICQ)
*   [7 IRC](#IRC)
*   [8 Xfire](#Xfire)
*   [9 Web QQ](#Web_QQ)
*   [10 Facebook XMPP](#Facebook_XMPP)
*   [11 Security](#Security)
*   [12 Privacy](#Privacy)
    *   [12.1 Pidgin-OTR](#Pidgin-OTR)
    *   [12.2 Pidgin-Encryption](#Pidgin-Encryption)
    *   [12.3 Pidgin-GPG](#Pidgin-GPG)
*   [13 Sametime protocol](#Sametime_protocol)
*   [14 SIP/Simple protocol for Live Communications Server 2003/2005/2007](#SIP.2FSimple_protocol_for_Live_Communications_Server_2003.2F2005.2F2007)
*   [15 Other packages](#Other_packages)
*   [16 Skype plugin](#Skype_plugin)
*   [17 Auto logout on suspend](#Auto_logout_on_suspend)
*   [18 Troubleshooting](#Troubleshooting)
    *   [18.1 Installing Pidgin after a Carrier installation](#Installing_Pidgin_after_a_Carrier_installation)
*   [19 History import Kopete to Pidgin](#History_import_Kopete_to_Pidgin)
*   [20 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [pidgin](https://www.archlinux.org/packages/?name=pidgin) package. Notable variants are:

*   **Pidgin Light** — Light Pidgin version without GStreamer, Tcl/Tk, XScreenSaver, video/voice support.

	[http://pidgin.im/](http://pidgin.im/) || [pidgin-light](https://aur.archlinux.org/packages/pidgin-light/)

You may also want to install additional plugins from the [purple-plugin-pack](https://www.archlinux.org/packages/?name=purple-plugin-pack).

## Spellcheck

The [aspell](https://www.archlinux.org/packages/?name=aspell) package will be installed as a dependency, but to prevent all of your text from showing up as incorrect you will need to install an aspell dictionary. See the [aspell](/index.php/Aspell "Aspell") article.

**Note:** The **switch spell** plugin is included in the [purple-plugin-pack](https://www.archlinux.org/packages/?name=purple-plugin-pack). It allows you to switch between multiple languages.

## Sound fix

To have event sounds working, install the [gstreamer0.10-good](https://www.archlinux.org/packages/?name=gstreamer0.10-good) package. Alternatively, in the "Sounds" preferences tab, the method can be set to 'command' and one of the following sound commands used.

After configuring [ALSA](/index.php/ALSA "ALSA"):

```
$ aplay %s

```

If using [OSS](/index.php/OSS "OSS"):

```
$ ossplay %s

```

And for [PulseAudio](/index.php/PulseAudio "PulseAudio"):

```
$ paplay %s

```

## Browser error

If clicking a link within Pidgin creates an error message about trying to use 'sensible-browser' to open a link, try editing `~/.purple/prefs.xml`. Find the line referencing 'sensible-browser' and change it to this:

```
<pref name='command' type='path' value='firefox'/>

```

This example assumes you use [Firefox](/index.php/Firefox "Firefox").

## QIP encoding bug

There is another bug in character encoding when communicating between Pidgin and QIP, which especially affects Czech language, but there are also other languages affected. There are two possible solutions. The better one is to upgrade from QIP to QIP 2012 or QIP Infium, second solution is to install and enable plugin from [pidgin-qip-decoder](https://aur.archlinux.org/packages/pidgin-qip-decoder/) package currently available from [AUR](/index.php/AUR "AUR").

## ICQ

You can change encoding for ICQ account if encoding in Buddy Information is not correct:

```
Account > *your ICQ account* > Edit account > Advanced tab

```

Select `Encoding: CP1251` (for Cyrillic).

## IRC

This is a small tutorial for connecting to Freenode. It should work for other IRC networks as long as you substitute the port numbers and other specific settings.

Go to *Accounts > Manage Accounts > Add*. Fill/select the following options:

```
Protocol: IRC
Username: *your username*

```

Now go to *Buddies > New instant message* (or hit `Ctrl+m`), fill 'freenode.net' in the textbox and *username*@irc.freenode.net, then click 'Ok'. Type:

```
/join #archlinux

```

The channel is irrelevant.

In order to register your nick, type:

```
/msg nickserv register *password* *email-addres*

```

Follow the instructions from the registration mail. For further help type:

```
/msg nickserv help
/msg nickserv help *command*

```

This final step will add your channel to 'Buddies': go to *Buddies > Add chat*, fill the correct channel in the textbox named channel (#archlinux).

## Xfire

Simply install [pidgin-gfire](https://www.archlinux.org/packages/?name=pidgin-gfire) and then add a new account, selecting xfire as protocol.

## Web QQ

Simply install [pidgin-lwqq](https://www.archlinux.org/packages/?name=pidgin-lwqq) and then add a new account, selecting webQQ as the protocol. QQ is a proprietary chat protocol/IM service mainly used in Asia, particularly China.

## Facebook XMPP

Facebook XMPP is not working since April 30th, 2015\. See [[1]](https://developers.facebook.com/docs/chat?_fb_noscript=1)

An alternative is to use a ThirdPartyPlugin that uses Facebook IM, see [[2]](https://github.com/jgeboski/purple-facebook)

You can get the plugin from either [purple-facebook](https://aur.archlinux.org/packages/purple-facebook/) or [purple-facebook-git](https://aur.archlinux.org/packages/purple-facebook-git/)

Then add a new account, select Facebook as the protocol, enter your [Facebook username](https://www.facebook.com/help/211813265517027) and password and login.

## Security

Pidgin uses Libpurple 2 which stores passwords unencrypted (in plaintext) in $HOME/.purple/account.xml, see [[3]](https://developer.pidgin.im/wiki/PlainTextPasswords). You can store them in a keyring by using a plugin like:

*   [purple-gnome-keyring](https://aur.archlinux.org/packages/purple-gnome-keyring/)
*   [pidgin-kwallet](https://www.archlinux.org/packages/?name=pidgin-kwallet)

## Privacy

Pidgin has some privacy rules set by default. Namely, the whole world cannot send you messages; only your contacts or people selected from a list. Adjust this, and other settings through:

```
Tools > Privacy

```

### Pidgin-OTR

This is a plugin that brings Off-The-Record (OTR) messaging to Pidgin. OTR is a cryptographic protocol that will encrypt your instant messages.

First you need to install [pidgin-otr](https://www.archlinux.org/packages/?name=pidgin-otr) from the official repositories. Once this has been done, OTR has been added to Pidgin.

1.  To enable OTR, start Pidgin and go to *Tools > Plugins* or press `Ctrl+u`. Scroll down to the entry entitled "Off-The-Record Messaging". If the checkbox beside it is not checked, check it.
2.  Next, click on the plugin entry and select "Configure plugin" at the bottom. Select which account you wish to generate a key for, then click "Generate". You will have now generated a private key. If you are not sure what the other options do, leave them, the default options will work fine.
3.  The next step is to contact a buddy who also has OTR installed. In the chat window, a new icon should appear to the top right of your text input box. Click on it, and select "Start private conversation". This will start an 'Unverified' session. Unverified sessions are encrypted, but not verified - that is, you have started a private conversation with someone using your buddy's account who has OTR, but who might not be your buddy. The steps for verification of a buddy are beyond the scope of this section; however, they might be added in the future.

### Pidgin-Encryption

[pidgin-encryption](https://www.archlinux.org/packages/?name=pidgin-encryption) transparently encrypts your instant messages with RSA encryption. Easy-to-use, but very secure.

You can enable it the same way as Pidgin-OTR.

Now you can open conversation window and new icon should appear beside menu. Press it to enable or disable encryption. Also if you want to make encryption enabled by default right-click on a buddy's name (in your buddy list), and select Turn Auto-Encrypt On. Now, whenever a new conversation window for that buddy is opened, encryption will start out as enabled.

### Pidgin-GPG

Pidgin-GPG transparently encrypt conversations using GPG, and taking advantage of all the features of a pre-existing WoT.

The plugin is available on AUR as [pidgin-gpg](https://aur.archlinux.org/packages/pidgin-gpg/). It can be enabled the same way as the previously mentioned ones.

## Sametime protocol

Sametime support is available by installing two packages from [AUR](/index.php/AUR "AUR"):

*   [meanwhile](https://aur.archlinux.org/packages/meanwhile/)
*   [libpurple-meanwhile](https://aur.archlinux.org/packages/libpurple-meanwhile/)

Previously it was required to rebuild Pidgin to remove the `--disable-meanwhile` flag from compilation, this is no longer needed. Once these two packages are installed the 'Sametime' protocol will be available when creating an account.

## SIP/Simple protocol for Live Communications Server 2003/2005/2007

The [pidgin-sipe](https://www.archlinux.org/packages/?name=pidgin-sipe) plugin is available in [official repositories](/index.php/Official_repositories "Official repositories").

## Other packages

Arch has other Pidgin-related packages. Here are the most popular (for a thorough list, search the AUR):

*   [pidgin-libnotify](https://www.archlinux.org/packages/?name=pidgin-libnotify) - Libnotify support, for theme-consistent notifications
*   [guifications](https://www.archlinux.org/packages/?name=guifications) - Toaster-style popup notifications
*   [microblog-purple](https://aur.archlinux.org/packages/microblog-purple/) - Libpurple plug-in supporting microblog services like Twitter
*   [pidgin-latex](https://aur.archlinux.org/packages/pidgin-latex/) - A small latex plugin for pidgin. Put math between $$ and have it rendered (recepient also needs to have this installed)

## Skype plugin

Install the [purple-skypeweb](https://www.archlinux.org/packages/?name=purple-skypeweb) or [skype4pidgin-git](https://aur.archlinux.org/packages/skype4pidgin-git/) package.

## Auto logout on suspend

If you suspend your computer pidgin seems to stay connected for about 15 minutes. To prevent message loss, it is needed to set your status offline before suspending or hibernating. The status message won't be changed.

Therefore create a new systemd unit `pidgin-suspend` in `/etc/systemd/system` Take the following snippet and replace *myuser* with your user.

```
[Unit]
Description=Suspend Pidgin
Before=sleep.target
StopWhenUnneeded=yes

[Service]
Type=oneshot
User=*myuser*
RemainAfterExit=yes
Environment=DISPLAY=:0
ExecStart=-/usr/bin/purple-remote setstatus?status=offline
ExecStop=-/usr/bin/purple-remote setstatus?status=available

[Install]
WantedBy=sleep.target

```

If you are using [pm-utils](/index.php/Pm-utils "Pm-utils"), you could create a `00pidgin` file in `/etc/pm/sleep.d/` instead.

```
#!/bin/sh
#
# 00pidgin: set offline/online status

case "$1" in
    hibernate|suspend)
        DISPLAY=:0 su -c 'purple-remote setstatus?status=offline' ''%myuser''
    ;;
    thaw|resume)
        DISPLAY=:0 su -c 'purple-remote setstatus?status=available' ''%myuser''
    ;;
    *) exit $NA
    ;;
esac

```

## Troubleshooting

### Installing Pidgin after a Carrier installation

If you previously installed [carrier](https://aur.archlinux.org/packages/carrier/) (aka [FunPidgin](http://funpidgin.sourceforge.net/)), follow these steps *before* installing Pidgin:

*   Quit Carrier
*   Delete your `~/.purple` directory.

**Warning:** This will remove all your user settings for any programs that use libpurple, i.e. Pidgin, Carrier, etc.

```
rm -r ~/.purple

```

*   Uninstall **carrier** and **libpurple**.
*   Install **pidgin** and **libpurple**.

## History import Kopete to Pidgin

*   Install [xalan-c](https://www.archlinux.org/packages/?name=xalan-c) and create `~/bin/history_import_kopete2pidgin.sh` with this code:

```
#!/bin/sh

KOPETE_DIR=~/.kde4/share/apps/kopete/logs
PIDGIN_DIR=~/.purple/logs
CURRENT_DIR=~/bin

cd

if [ ! -d $KOPETE_DIR ];then
    echo "Kopete log directory not found"
    exit 1;
fi

if [ ! -d $PIDGIN_DIR ];then
    echo "Pidgin log directory not found"
    exit 2;
fi

for KOPETE_PROTODIR in $(ls $KOPETE_DIR); do
    PIDGIN_PROTODIR=$(echo $KOPETE_PROTODIR | sed 's/Protocol//' | tr [:upper:] [:lower:])
    for accnum in $(ls $KOPETE_DIR/$KOPETE_PROTODIR); do
        echo "Account number: $accnum"
        for num in $(ls $KOPETE_DIR/$KOPETE_PROTODIR/$accnum); do
            FILENAME=$(Xalan $KOPETE_DIR/$KOPETE_PROTODIR/$accnum/$num $CURRENT_DIR/history_import_kopete2pidgin_filename.xslt)
            if [ $? = 0 ]; then
                echo "$KOPETE_DIR/$KOPETE_PROTODIR/$accnum/$num"
                echo " -> $PIDGIN_DIR/$PIDGIN_PROTODIR/$FILENAME"
                mkdir -p $(dirname $PIDGIN_DIR/$PIDGIN_PROTODIR/$FILENAME)
                Xalan -o $PIDGIN_DIR/$PIDGIN_PROTODIR/$FILENAME $KOPETE_DIR/$KOPETE_PROTODIR/$accnum/$num $CURRENT_DIR/history_import_kopete2pidgin.xslt
            fi
        done
    done
done

```

*   Make `~/bin/history_import_kopete2pidgin.sh` executable:

```
chmod +x ~/bin/history_import_kopete2pidgin.sh

```

*   Create `~/bin/history_import_kopete2pidgin.xslt` with this code:

```
<?xml version="1.0"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:output method="text" indent="no" />

    <xsl:template match="kopete-history">
        <xsl:apply-templates select="msg"/>
    </xsl:template>

    <xsl:template match="msg">
        <xsl:text>(</xsl:text>
        <xsl:value-of select="translate(substring-after(@time,' '),':',',')"/>
        <xsl:text>) </xsl:text>
        <xsl:value-of select="@nick"/>
        <xsl:if test="not(@nick) or @nick = *">*
            <xsl:value-of select="@from"/>
        </xsl:if>
        <xsl:text>: </xsl:text>
        <xsl:value-of select="."/>
		<xsl:text>
</xsl:text>
    </xsl:template>
</xsl:stylesheet>
</nowiki>
```

*   Create `~/bin/history_import_kopete2pidgin_filename.xslt` with this code:

```
<?xml version="1.0"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:output method="text" indent="no" />

    <xsl:template match="kopete-history">
        <xsl:value-of select="head/contact[@type = 'myself']/@contactId"/>
        <xsl:text>/</xsl:text>
        <xsl:value-of select="head/contact[not(@type)]/@contactId"/>
        <xsl:text>/</xsl:text>
        <xsl:value-of select="head/date/@year"/>
        <xsl:text>-</xsl:text>
        <xsl:if test="head/date/@month &lt; 10">0</xsl:if>
        <xsl:value-of select="head/date/@month"/>
        <xsl:text>-</xsl:text>
        <xsl:if test="string-length(substring-before(msg[1]/@time,' ')) &lt; 2">0</xsl:if>
        <xsl:value-of select="translate(msg[1]/@time,' :','.')"/>
        <xsl:text>+0200EET.txt</xsl:text>
    </xsl:template>
</xsl:stylesheet>
```

*   Execute the command in the shell:

```
~/bin/history_import_kopete2pidgin.sh

```

## See also

*   [Pidgin homepage](http://pidgin.im)
*   [History import Kopete to Pidgin](http://lukav.com/wordpress/2008/03/30/history-import-kopete-to-pidgin)