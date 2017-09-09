From the project [home page](http://www.pidgin.im/): "Pidgin is an easy to use and free chat client used by millions. Connect to AIM, Google Talk, ICQ, IRC, XMPP, and more chat networks all at once."

## Contents

*   [1 Installation](#Installation)
*   [2 Spellcheck](#Spellcheck)
*   [3 Services](#Services)
    *   [3.1 Facebook](#Facebook)
    *   [3.2 IRC](#IRC)
    *   [3.3 Sametime protocol](#Sametime_protocol)
    *   [3.4 SIP/Simple protocol for Live Communications Server 2003/2005/2007](#SIP.2FSimple_protocol_for_Live_Communications_Server_2003.2F2005.2F2007)
    *   [3.5 Skype plugin](#Skype_plugin)
    *   [3.6 Rocket.Chat plugin](#Rocket.Chat_plugin)
*   [4 Security](#Security)
*   [5 Privacy](#Privacy)
    *   [5.1 Pidgin-OTR](#Pidgin-OTR)
    *   [5.2 Pidgin-Encryption](#Pidgin-Encryption)
    *   [5.3 Pidgin-GPG](#Pidgin-GPG)
*   [6 Other packages](#Other_packages)
*   [7 Auto logout on suspend](#Auto_logout_on_suspend)
*   [8 Minimize to tray](#Minimize_to_tray)
*   [9 History import Kopete to Pidgin](#History_import_Kopete_to_Pidgin)
*   [10 Backup](#Backup)
*   [11 Troubleshooting](#Troubleshooting)
    *   [11.1 Version Match for Sametime](#Version_Match_for_Sametime)
    *   [11.2 Browser error](#Browser_error)
    *   [11.3 ICQ Buddy Information encoding fix](#ICQ_Buddy_Information_encoding_fix)
*   [12 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [pidgin](https://www.archlinux.org/packages/?name=pidgin) package. Notable variants are:

*   **Pidgin Light** — Light Pidgin version without GStreamer, Tcl/Tk, XScreenSaver, video/voice support.

	[http://pidgin.im/](http://pidgin.im/) || [pidgin-light](https://aur.archlinux.org/packages/pidgin-light/)

You may also want to install additional plugins from the [purple-plugin-pack](https://www.archlinux.org/packages/?name=purple-plugin-pack).

## Spellcheck

The [aspell](https://www.archlinux.org/packages/?name=aspell) package will be installed as a dependency, but to prevent all of your text from showing up as incorrect you will need to install an aspell dictionary. See the [aspell](/index.php/Aspell "Aspell") article.

**Note:** The **switch spell** plugin is included in the [purple-plugin-pack](https://www.archlinux.org/packages/?name=purple-plugin-pack). It allows you to switch between multiple languages.

## Services

### Facebook

[Install](/index.php/Install "Install") the [purple-facebook](https://www.archlinux.org/packages/?name=purple-facebook) package. (or [purple-facebook-git](https://aur.archlinux.org/packages/purple-facebook-git/))

Then add a new account, select Facebook as the protocol, enter your [Facebook username](https://www.facebook.com/help/211813265517027) and password and login.

### IRC

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

### Sametime protocol

[Install](/index.php/Install "Install") the [libpurple-meanwhile](https://aur.archlinux.org/packages/libpurple-meanwhile/) package. The 'Sametime' protocol will be available when creating an account.

### SIP/Simple protocol for Live Communications Server 2003/2005/2007

[Install](/index.php/Install "Install") the [pidgin-sipe](https://www.archlinux.org/packages/?name=pidgin-sipe) package.

### Skype plugin

Install the [purple-skypeweb](https://www.archlinux.org/packages/?name=purple-skypeweb) or [skype4pidgin-git](https://aur.archlinux.org/packages/skype4pidgin-git/) package.

### Rocket.Chat plugin

Install [mercurial](https://www.archlinux.org/packages/?name=mercurial) and [discount](https://aur.archlinux.org/packages/discount/) packages.

Type:

```
hg clone [https://bitbucket.org/EionRobb/purple-rocketchat/](https://bitbucket.org/EionRobb/purple-rocketchat/)
cd purple-rocketchat
make
sudo make install

```

Following files will be installed:

```
/usr/lib/purple-2/librocketchat.so
/usr/share/pixmaps/pidgin/protocols/16/rocketchat.png
/usr/share/pixmaps/pidgin/protocols/48/rocketchat.png
/usr/share/pixmaps/pidgin/protocols/22/rocketchat.png
```

The 'Rocket.Chat' protocol should be now available when creating an account.

## Security

Pidgin uses Libpurple 2 which stores passwords unencrypted (in plaintext) in $HOME/.purple/account.xml, see [[1]](https://developer.pidgin.im/wiki/PlainTextPasswords). You can store them in a keyring by using a plugin like:

*   [purple-gnome-keyring](https://aur.archlinux.org/packages/purple-gnome-keyring/)
*   [pidgin-kwallet](https://www.archlinux.org/packages/?name=pidgin-kwallet)

## Privacy

Pidgin has some privacy rules set by default. Namely, the whole world cannot send you messages; only your contacts or people selected from a list. Adjust this, and other settings in *Tools > Privacy*.

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

The plugin is available on AUR as [pidgin-gpg-git](https://aur.archlinux.org/packages/pidgin-gpg-git/). It can be enabled the same way as the previously mentioned ones.

## Other packages

Arch has other Pidgin-related packages. Here are the most popular (for a thorough list, search the AUR):

*   [pidgin-libnotify](https://www.archlinux.org/packages/?name=pidgin-libnotify) - Libnotify support, for theme-consistent notifications
*   [purple-libnotify-plus](https://aur.archlinux.org/packages/purple-libnotify-plus/) - Notifications with Libnotify which does work with notify-osd. It might matter for WMs without DE, like i3, the original pidgin-libnotify instead uses plain messagebox there.
*   [guifications](https://www.archlinux.org/packages/?name=guifications) - Toaster-style popup notifications
*   [microblog-purple](https://aur.archlinux.org/packages/microblog-purple/) - Libpurple plug-in supporting microblog services like Twitter
*   [pidgin-latex](https://aur.archlinux.org/packages/pidgin-latex/) - A small latex plugin for pidgin. Put math between $$ and have it rendered (recepient also needs to have this installed)

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

## Minimize to tray

To make use of the [Xfce](/index.php/Xfce "Xfce") system tray go to preferences and enable the system tray in the section "Interface". You can now close the main window and run pidgin minimized. You will also be able to see message notifications in the tray.

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

## Backup

Save `~/.purple` to backup all message logs, accounts and other application data.

## Troubleshooting

### Version Match for Sametime

There was an issue if you would connect to the Sametime via Pidgin, it prompt "Version Match". A potential solution on the client side is to fake the version in accounts.xml. Insert/change the lines:

```
<setting name='fake_client_id' type='bool'>1</setting>
<setting name='client_minor' type='int'>8511</setting>

```

in the <settings> section of Sametime account in accounts.xml which is located in $HOME/.purple/ folder.

### Browser error

If clicking a link within Pidgin creates an error message about trying to use 'sensible-browser' to open a link, try editing `~/.purple/prefs.xml`. Find the line referencing 'sensible-browser' and change it to this:

```
<pref name='command' type='path' value='firefox'/>

```

This example assumes you use [Firefox](/index.php/Firefox "Firefox").

As an alternative if the method above does not work you can set the desired browser in the pidgin preferences in the section "Browser".

### ICQ Buddy Information encoding fix

You can change encoding for ICQ account if encoding in Buddy Information is not correct:

```
Account > *your ICQ account* > Edit account > Advanced tab

```

Select `Encoding: CP1251` (for Cyrillic).

## See also

*   [Pidgin How To](https://developer.pidgin.im/wiki/Using%20Pidgin)
*   [Pidgin homepage](http://pidgin.im)
*   [History import Kopete to Pidgin](http://lukav.com/wordpress/2008/03/30/history-import-kopete-to-pidgin)
*   [Connecting to HipChat using Pidgin](https://confluence.atlassian.com/hipchatkb/connecting-to-hipchat-using-pidgin-751436267.html)