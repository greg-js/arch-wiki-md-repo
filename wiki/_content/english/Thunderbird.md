Mozilla [Thunderbird](https://www.mozilla.org/thunderbird/) is an open source email, news, and chat client developed by the [Mozilla Foundation](https://www.mozilla.org/).

## Contents

*   [1 Installation](#Installation)
*   [2 Securing](#Securing)
    *   [2.1 Considerations](#Considerations)
*   [3 Extensions](#Extensions)
    *   [3.1 EnigMail - Encryption](#EnigMail_-_Encryption)
        *   [3.1.1 Sharing the public key](#Sharing_the_public_key)
        *   [3.1.2 Encrypting emails](#Encrypting_emails)
        *   [3.1.3 Decrypting emails](#Decrypting_emails)
        *   [3.1.4 Blank draft messages](#Blank_draft_messages)
    *   [3.2 TorBirdy - Anonymity](#TorBirdy_-_Anonymity)
    *   [3.3 FireTray - Tray icon](#FireTray_-_Tray_icon)
    *   [3.4 Lightning - Calendar](#Lightning_-_Calendar)
    *   [3.5 SOGo Connector (CardDAV)](#SOGo_Connector_.28CardDAV.29)
    *   [3.6 Cardbook (CardDAV)](#Cardbook_.28CardDAV.29)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Setting the default browser](#Setting_the_default_browser)
    *   [4.2 Plain Text mode and font uniformity](#Plain_Text_mode_and_font_uniformity)
    *   [4.3 Webmail with Thunderbird](#Webmail_with_Thunderbird)
    *   [4.4 Migrate profile to another system](#Migrate_profile_to_another_system)
    *   [4.5 Export + Import](#Export_.2B_Import)
    *   [4.6 Changing the default sorting order](#Changing_the_default_sorting_order)
    *   [4.7 Maildir support](#Maildir_support)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 LDAP Segfault](#LDAP_Segfault)
    *   [5.2 Error: Incoming server already exists](#Error:_Incoming_server_already_exists)

## Installation

[Install](/index.php/Install "Install") the [thunderbird](https://www.archlinux.org/packages/?name=thunderbird) package, with a [language pack](https://www.archlinux.org/packages/?q=thunderbird-i18n) if required.

Other versions include:

*   **Thunderbird Beta** — Cutting edge features with relatively-good stability.

	[http://www.mozilla.org/en-US/thunderbird/channel/](http://www.mozilla.org/en-US/thunderbird/channel/) || [thunderbird-beta-bin](https://aur.archlinux.org/packages/thunderbird-beta-bin/)

*   **Thunderbird Earlybird** — Experience the newest innovations as they're developed (equivalent to an alpha and Firefox Aurora releases).

	[http://www.mozilla.org/en-US/thunderbird/channel/](http://www.mozilla.org/en-US/thunderbird/channel/) || [thunderbird-earlybird](https://aur.archlinux.org/packages/thunderbird-earlybird/)

*   **Thunderbird Nightly** — Experience the newest innovations with nightly releases (for those that want to work with breakages).

	[https://ftp.mozilla.org/pub/mozilla.org/thunderbird/nightly/latest-comm-central/](https://ftp.mozilla.org/pub/mozilla.org/thunderbird/nightly/latest-comm-central/) || [thunderbird-nightly](https://aur.archlinux.org/packages/thunderbird-nightly/)

A version overview, both past and future, can be read on the [Mozilla wiki](https://wiki.mozilla.org/Releases).

## Securing

### Considerations

Under some circumstances Thunderbird may send your system's (internal) IP address as reply to HELO/ELHO requesting SMTP servers. If you have concerns, please read [this](http://kb.mozillazine.org/Replace_IP_address_with_name_in_headers) article. You might change this for Firefox, too.

If you want to hide Thunderbird for sending your system's [User Agent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Gecko_user_agent_string_reference#Linux) string, then you can override the default string with an empty one:

1.  go to `Edit > Preferences > Advanced > General > Config Editor`.(*)
2.  right-click and create new string entry `general.useragent.override` and leave the second dialog entry empty.

While Thunderbird disables email images by default, it enables HTML rendering which may expose IP address and location. Choose `View > Message Body As > Plain Text` to disable this.

JavaScript is disabled for message content but not RSS news feeds. To disable JavaScript for RSS:

1.  go to `Edit > Preferences > Advanced > General > Config Editor`.
2.  search `javascript.enabled` and double-click the value to false.

## Extensions

### EnigMail - Encryption

[EnigMail](https://www.enigmail.net) is an [extension](https://addons.mozilla.org/thunderbird/addon/enigmail/) that allows writing and receiving email signed and/or encrypted with the OpenPGP standard. It relies on the [GnuPG](/index.php/GnuPG "GnuPG").

Common packages include: [thunderbird-enigmail](https://aur.archlinux.org/packages/thunderbird-enigmail/) and [thunderbird-enigmail-bin](https://aur.archlinux.org/packages/thunderbird-enigmail-bin/).

#### Sharing the public key

To distribute the public key one may upload it to a [keyserver](https://en.wikipedia.org/wiki/Key_server_(cryptographic) "wikipedia:Key server (cryptographic)").

#### Encrypting emails

Encryption does not always work properly with emails containing HTML. It is best to use plain text by choosing *Options > Delivery Format > Plain Text Only* in the new email window.

Once the email is finished it can be signed through the *OpenPGP* menu.

#### Decrypting emails

Assuming that the email was encrypted properly, just trying to open it should result in a pop-up asking to type in the keyphrase.

#### Blank draft messages

If after upgrading to [gnupg](https://www.archlinux.org/packages/?name=gnupg) v2.1 your saved draft emails have gone "blank" and show a pink bar displaying:

```
Enigmail Error - no matching private/secret key found to decrypt message; click on 'Details' button for more information

```

or, when you have a "Write" window open you repeatedly see a popup window with:

```
The email address or key ID 0x*key_id* cannot be matched to a valid, not expired OpenPGP key.
Please ensure that you have a valid OpenPGP key, and that your account settings point to that key.

```

and `gpg --list-keys` fails to show some keys that used to be there, see [GnuPG invalid packet workaround](http://jo-ke.name/wp/?p=111).

### TorBirdy - Anonymity

TorBirdy is an [extension](https://addons.mozilla.org/en-us/thunderbird/addon/torbirdy/) that configures Thunderbird to make connections over the [Tor](/index.php/Tor "Tor") anonymity network.

### FireTray - Tray icon

FireTray is an [extension](https://addons.mozilla.org/thunderbird/addon/firetray/) that adds a customizable system tray icon for Thunderbird. It is available in the AUR as [thunderbird-firetray](https://aur.archlinux.org/packages/thunderbird-firetray/).

### Lightning - Calendar

[Lightning](https://www.mozilla.org/projects/calendar/lightning/) is a calendar [extension](https://addons.mozilla.org/thunderbird/addon/lightning/) that brings [Sunbird](https://en.wikipedia.org/wiki/Mozilla_Sunbird "wikipedia:Mozilla Sunbird")'s functionality to Thunderbird, including CalDAV support.

It is available in the AUR as [thunderbird-lightning-bin](https://aur.archlinux.org/packages/thunderbird-lightning-bin/).

In case you are migrating a user profile (with Lightning installed there) from another platform (e.g. Windows), you may have to reinstall the Lightning addon from the mozilla addon page because Lightning is platform-dependent.

### SOGo Connector (CardDAV)

[SOGo Connector](http://www.sogo.nu/english/downloads/frontends.html) allows to sync addressbooks via CardDAV.

It is available in the AUR as [thunderbird-sogo-connector-bin](https://aur.archlinux.org/packages/thunderbird-sogo-connector-bin/).

### Cardbook (CardDAV)

[Cardbook](https://addons.mozilla.org/en-US/thunderbird/addon/cardbook/) (VCard Addressbook): a new addressbook for Thunderbird based on the CARDDav and VCARD standards.

## Tips and tricks

### Setting the default browser

**Note:** Since version 24 the `network.protocol-handler.app.*` keys have no effect and will not be able to set the default browser.

Recent versions of Thunderbird use the default browser as defined by the [system MIME settings](/index.php/Default_applications "Default applications"). This is commonly modified by the Gnome Control Center (*Gnome Control Center > Details > Default Applications > Web*) (available in: [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center)).

This can be overridden in Thunderbird through *Edit > Preferences > Advanced > General > Config Editor* by searching for `network.protocol-handler.warn-external`.

If the following three are all set to **false** (default), turn them to **true**, and Thunderbird will ask you when clicking on links which application to use (remember to also check *"Remember my choice for .. links"*).

```
network.protocol-handler.warn-external.ftp
network.protocol-handler.warn-external.http
network.protocol-handler.warn-external.https

```

### Plain Text mode and font uniformity

Plain Text mode lets you view all your emails without HTML rendering and is available in *View > Message Body As*. This defaults to the [Monospace](https://en.wikipedia.org/wiki/Monospace_(Unicode) font but the size is still inherited from original system fontconfig settings. The following example will overwrite this with Ubuntu Mono of 10 pixels (available in: [ttf-ubuntu-font-family](https://www.archlinux.org/packages/?name=ttf-ubuntu-font-family)).

Remember to run `fc-cache -fv` to update system font cache. See [Font configuration](/index.php/Font_configuration "Font configuration") for more information.

 `~/.config/fontconfig/fonts.conf` 
```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="pattern">
    <test qual="any" name="family"><string>monospace</string></test>
    <edit name="family" mode="assign" binding="same"><string>Ubuntu Mono</string></edit>
    <!-- For Thunderbird, lowering default font size to 10 for uniformity -->
    <edit name="pixelsize" mode="assign"><int>10</int></edit>
  </match>
</fontconfig>

```

### Webmail with Thunderbird

	*See upstream Wiki: [Using webmail with your email client](http://kb.mozillazine.org/Using_webmail_with_your_email_client).*

### Migrate profile to another system

**Tip:** The [ImportExportTools](https://addons.mozilla.org/en-US/thunderbird/addon/importexporttools) addon offers an option to export and import a profile folder.

Before you start with Importing or Exporting tasks, backup your complete `~/.thunderbird` profile:

```
$ cp -R ~/.thunderbird /to/backup/folder/

```

With migration you just copy your current Thunderbird profile to another PC or a new Thunderbird installation:

1\. Install Thunderbird on the target PC

2\. Start Thunderbird without doing anything and quit it.

3\. Go to your Backup folder of your old Thunderbird installation

4\. Enter the backup profile folder:

```
$ cd /to/backup/folder/.thunderbird/<oldrandomnumber>.default/

```

5\. Copy its content into the target profile folder `~/.thunderbird/<newrandomnumber>.default/`

```
$ cp -R /to/backup/folder/.thunderbird/<oldrandomnumber>.default/* ~/.thunderbird/<newrandomnumber>.default/

```

### Export + Import

Before you start with Importing or Exporting tasks, backup your complete `~/.thunderbird` profile:

```
$ cp -R ~/.thunderbird /to/backup/folder/

```

If your accounts are broken or you want to join two different Thunderbird installations, you better install one Import and Export AddOn (eg. [ImportExportTools AddOn](https://addons.mozilla.org/en-US/thunderbird/addon/importexporttools)) to both Thunderbird installations and following this just export and import all your data to the new installation.

### Changing the default sorting order

Thunderbird (up to at least 31.4.0-1) sorts mail by date with the oldest on top without any threading. While this can be changed per folder, it is easier to set a sane default instead as described in [this Superuser.com post](https://superuser.com/questions/13518/change-the-default-sorting-order-in-thunderbird).

Go to Edit -> Preferences -> Advanced -> General -> Config Editor and set these keys:

```
mailnews.default_sort_order = 2 (descending)
mailnews.default_view_flags = 1 (Threaded view)

```

### Maildir support

The default message store format is mbox. To enable the use of Maildir, see [Mozilla wiki: Thunderbird/Maildir](https://wiki.mozilla.org/Thunderbird/Maildir). You basically have to set this preference through (Edit -> Preferences -> Advanced -> General -> Config Editor):

```
mail.serverDefaultStoreContractID = @mozilla.org/msgstore/maildirstore;1

```

Some limitations up to at least 31.4.0-1: only the "tmp" and "cur" directories are supported. The "new" directory is completely ignored. The read state of mails are stored in a separate ".msf" file, so initially all local mail using Maildir will be marked as unread even when located in the "cur" directory.

## Troubleshooting

### LDAP Segfault

An [LDAP clash (Bugzilla#292127)](https://bugzilla.mozilla.org/show_bug.cgi?id=292127) arises on systems configured to use it to fetch user information. A possible [workaround](https://bugzilla.mozilla.org/show_bug.cgi?id=292127#c7) consists of renaming the conflicting bundled LDAP library.

### Error: Incoming server already exists

It seems Thunderbird (v24) still has that bug which pops up with "Incoming server already exists" if you want to reinstall a previously deleted account with the same account data afterwards. Unfortunately, if you get this error you can now only clean reinstall Thunderbird:

1\. Make a backup of your current profile:

```
$ cp -R ~/.thunderbird /to/backup/folder/

```

2\. Export all you Accounts, Calendar and Feeds via an AddOn like it's written in *Export section* of this Wiki. 3\. Uninstall your current Thunderbird installation

```
$ pacman -R thunderbird

```

4\. Remove all your data by deleting your current Thunderbird folder `rm -R ~/.thunderbird/`.

5\. Install Thunderbird again:

```
$ pacman -S thunderbird

```

6.Create your mail accounts, feeds and calenders (empty).

7\. Install the [ImportExportTools](https://addons.mozilla.org/en-US/thunderbird/addon/importexporttools/) AddOn

8\. Import all your data.