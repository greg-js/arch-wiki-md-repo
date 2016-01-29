# Evolution

Evolution is a [GNOME](/index.php/GNOME "GNOME") mail client it supports IMAP, Microsoft Exchange Server and Novell GroupWise. It also has a calender function that supports vcal, csv, google calendar and many more. You can also organise your contacts, tasks and memos with Evolution. The beautiful thing about Evolution is that it's easy to use and integrates with the GNOME environment. You can see your calendar, tasks and location in the GNOME panel along with the weather and date. Just add the clock to your GNOME panel.

## Contents

*   [1 Installation](#Installation)
*   [2 IMAP Setup](#IMAP_Setup)
*   [3 Alternative IMAP Setup](#Alternative_IMAP_Setup)
    *   [3.1 Offlineimap setup](#Offlineimap_setup)
    *   [3.2 First offlineimap sync and automated sync-ing](#First_offlineimap_sync_and_automated_sync-ing)
    *   [3.3 Evolution setup for offlineimap's maildir](#Evolution_setup_for_offlineimap.27s_maildir)
*   [4 GMAIL Setup](#GMAIL_Setup)
    *   [4.1 Receiving Mail](#Receiving_Mail)
    *   [4.2 Sending Mail](#Sending_Mail)
*   [5 Gmail Calendar](#Gmail_Calendar)
*   [6 Google Contacts](#Google_Contacts)
*   [7 Tudelft webmail (Exchange)](#Tudelft_webmail_.28Exchange.29)
*   [8 Using Evolution Outside Of Gnome](#Using_Evolution_Outside_Of_Gnome)
*   [9 Spell Check](#Spell_Check)
*   [10 Tips and tricks](#Tips_and_tricks)
    *   [10.1 Changing cipher settings](#Changing_cipher_settings)
*   [11 Troubleshooting](#Troubleshooting)
    *   [11.1 Failing to Synchronize with Server](#Failing_to_Synchronize_with_Server)
*   [12 References](#References)

## Installation

[Install](/index.php/Install "Install") the [evolution](https://www.archlinux.org/packages/?name=evolution) package.

Exchange servers are supported by [evolution-ews](https://www.archlinux.org/packages/?name=evolution-ews) and web calendars (like Google calendar) by [evolution-data-server](https://www.archlinux.org/packages/?name=evolution-data-server).

## IMAP Setup

This is the setup for a standard IMAP mail address. Go to Edit -> Preferences -> Mail Accounts. Add a mail account insert your Name and real email adress. Then click 'forward' here you are going to select the server type, this is IMAP. Now fill in the textbox server, for the server adress and username. For the rest of the options just follow the wizard. It is very easy, if you get stuck read this guide [[1]](http://library.gnome.org/users/evolution/stable/).

## Alternative IMAP Setup

An alternative to letting Evolution connect directly to the IMAP server is to sync the IMAP server to your PC. This costs as much hard-disc space as you have mail, though it is possible to limit the folders synced in this manner (see below). An additional benefit (primary inspiration for this app) is that you have a full copy of your email, including attachments, on your PC for retrieval, even if on the move without an internet connection.

To set this up, you will need to [install](/index.php/Install "Install") the [offlineimap](https://www.archlinux.org/packages/?name=offlineimap) package (see also [[2]](http://offlineimap.org/)).

### Offlineimap setup

offlineimap takes its settings from the file ~/.offlineimaprc, which you will need to create. Most users will be able to use the .offlineimaprc below, for the most common case of a Gmail account. The settings for a general account are identical, except remotehost, ssl, and remoteport need to be set appropriately (see the comments below). See the [official README](https://github.com/nicolas33/offlineimap) for more information.

```
[general]
accounts = MyAccount
# Set this to the number of accounts you have.
maxsyncaccounts = 1
# You can set ui = TTY.TTYUI for interactive password entry if needed.
# Setting it within this file (see below) is easier.
ui = Noninteractive.Basic

[Account MyAccount]
# Each account should have a local and remote repository
localrepository = MyLocal
remoterepository = MyGmail
# Specifies how often to do a repeated sync (if running without crond)
autorefresh = 10

[Repository MyLocal]
type = Maildir
localfolders = /home/path/to/your/maildir
# This needs to be specified so the MailDir uses a folder structure
# suitable to Evolution
sep = /

[Repository MyGmail]
# Example for a gmail account
type = Gmail
# If using some other IMAP server, uncomment and set the following:-
#remotehost = imap.gmail.com
#ssl = yes
#remoteport = 993
# Specify the Gmail user name and password.
remoteuser = yourname@gmail.com
remotepass = yourpassword
# realdelete is Gmail specific, setting to no ensures that deleting
# a message sends it to 'All Mail' instead of the trash.
realdelete = no
# Use 1 here first, increase it if your connection (and the server's)
# supports it.
maxconnections = 1
# This translates folder names such that everything (including your Inbox)
# appears in the same folder (named root).
nametrans = lambda foldername: re.sub('^Sent$', 'root/Sent',
 re.sub('^(\[G.*ail\]|INBOX)', 'root', foldername))
# This excludes some folders from being synced. You will almost
# certainly want to exclude 'All Mail', 'Trash', and 'Starred', at
# least. Note that offlineimap does NOT honor subscription details.
folderfilter = lambda foldername: foldername not in ['[Gmail]/All Mail',
 '[Gmail]/Trash','[Gmail]/Spam','[Gmail]/Starred']

```

WARNING: Please note that any space indenting a line of code in .offlineimaprc would be considered as appending that line to the previous line. In other words, always make sure there is no space before any lines in your config file.

Acknowledgement: This config file was done by referring both to the official example as well as to the config file in an article on [http://www.linux.com](http://www.linux.com) (no longer available).

### First offlineimap sync and automated sync-ing

Once you have completed your offlineimap setup, you should perform your first sync by running with your normal user account

```
$ offlineimap

```

Assuming you've set your password and all other settings correctly, offlineimap will begin to sync the requested repositories. This may take a long while, depending on connection speed and size of your mail account, so you should preferably find a fast connection to do this. You can run offlineimap using another interface by specifying

```
$ offlineimap -u TTY.TTYUI

```

This allows interactive entry of passwords.

Once you've completed your first sync, you'll want to set up automatic syncing. This can be done using crond, or just by running offlineimap on startup. The disadvantage of running offlineimap on startup (with autorefresh set) is that if for any reason an error appears, your mail will just stop syncing from that point onwards. So, running through crond requires you to add the following line to your crontab.

```
*/10 * * * * /path/to/scripts/runofflineimap >/dev/null 2>&1

```

For those unfamiliar with crontab and/or vi, just run

```
$ crontab -e

```

Press 'i' to start input, type in the line above, press Esc to escape back to the prompt, and type ':wq' to save and quit. /path/to/scripts/runofflineimap should run offlineimap itself (with -o for a single run). Here is an example script for that:-

```
#!/bin/sh
# Run offlineimap through cron to fetch email periodically
ps aux | grep "\/usr\/bin\/offlineimap"
if [ $? -eq "0" ]; then
        logger -i -t offlineimap "Another instance of offlineimap running. Exiting."
        exit 0;
else
        logger -i -t offlineimap "Starting offlineimap..."
        offlineimap -u Noninteractive.Quiet -o
        logger -i -t offlineimap "Done offlineimap..."
	exit 0;
fi

```

You should now have an automatically synced local copy of your IMAP server. Error messages (if any) will be shown in /var/log/cron.d or one of its variants.

### Evolution setup for offlineimap's maildir

This is really quite simple, use Evolution's Account Assistant and select the Server Type "Maildir-format mail directories", under the Receiving Email section. Select also the path to your maildir (the 'root' folder if you're using a modified version of the .offlineimaprc above). You can change your 'Checking for New Mail' option to something very short, even 1 minute, since this only checks your local copy and not the server-side copy. SMTP settings are according to normal usage (does not go through offlineimap).

## GMAIL Setup

To setup a GMail account, go to Edit -> Preferences -> Mail Accounts and enter your mail account details.

### Receiving Mail

*   Server Type: POP
*   Server: pop.gmail.com
*   Username: <username>@gmail.com
*   Use Secure Connecetion: SSL encryption
*   Authenthication Type: Password

Optionally fill in automatically check for new mail every ** minutes. The rest is user specific.

### Sending Mail

*   Server type: SMTP
*   Server: smtp.gmail.com
*   Port: 587
*   Server requires authentication: Checked
*   Use Secure Connection: TSL
*   Fill in Username: <username>@gmail.com
*   Authentication: PLAIN or Login

You are now finished with configuring evolution for gmail. Just hit Send/ Receive in the main screen and wait for new mail. If it still didn't work, go to this link [[3]](http://tuxicity.wordpress.com/2007/03/08/howto-set-up-gmail-in-evolution-gnomes-mail-client-and-organizer/)

## Gmail Calendar

You can use your gmail calendar in evolution here's how:

Go to your calendar in your browser. Click on manage calendars -> the click on the calendar you want to add -> In the Private URL section copy the URL of ICAL (green button).

Now go to Evolution. Click on file -> new -> calendar . In the 'new calendar dialog box' select type: On The Web. You can fill in your own calendar name Then Copy the URL to the URL field

Now you will see your google calendar in your calendar view in Evolution by the name you gave it in the Name field.

**Variant2 (with evolution-webcal):**

From Evolution click on -> new -> calendar . In the 'new calendar dialog box' select type: Google. You can fill in your own calendar name. Insert your username (not the email). Click the button "Get List" and choose the calendar you want to use.

## Google Contacts

Simarly with the calendar, you can sync your Google contacts in evolution.

On Evolution, click on File > New > Address Book . Choose Google as type and add your Google account email as the User.

**Note:** The above does not work since Google has turned off the old developer APIs which Evolution uses. You will need to create a Gnome online account (GOA) for your google account. Install [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) to be able to create a GOA and select what you would like to sync. You can delete/disable any google addressbooks created in evolution directly, else you will see two addressbooks

## Tudelft webmail (Exchange)

This is the setup for your tudelft webmail for evolution. It might also work for other webmail based email accounts.

Go to Edit -> Preferences -> Mail Accounts and make a mail account. For your Email Adress: <netid>@gmail.com . Be carefull your <netid>@student.tudelft.nl must be like this example: E.M.devries@student.tudelft.nl

Receiving mail: Server type: Microsoft Exchange Username: <netid> this is just your netid like this example: edevries OWA URL: [https://webmail.tudelft.nl](https://webmail.tudelft.nl) -> now click 'Authenticate' and fill in your password. The mailbox will be filled in automaticlly

Click Forward: The receiving options are already correct, you can select the option to automaticlly receive email every x minutes.

Click Forward: Now just fill in the name of the mailbox and you are done.

## Using Evolution Outside Of Gnome

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** This setup script has changed. See [GNOME Keyring#Use without GNOME, but with a display manager](/index.php/GNOME_Keyring#Use_without_GNOME.2C_but_with_a_display_manager "GNOME Keyring") for the new version. (Discuss in [Talk:Evolution#](https://wiki.archlinux.org/index.php/Talk:Evolution))

In order to use Evolution outside of Gnome desktop you must export [gnome-keyring](/index.php/Gnome-keyring "Gnome-keyring"):

```
#!/bin/bash
eval \`gnome-keyring-daemon\`
export GNOME_KEYRING_PID
export GNOME_KEYRING_SOCKET
exit

```

Run the above script before starting Evolution. Reboot or remove the appropriate files in your /tmp directory prior to running.

## Spell Check

Make sure you have a local dictionary installed. You can run `pacman -Ss aspell` for a list of dictionaries.

## Tips and tricks

### Changing cipher settings

It is possible to change the advertised ciphers used to secure the connetion to the server. Evolution does not provide a switch to change the settings for the used ciphers, however since evolution uses GnuTLS it is possible to change the settings using environment variables.

One way to change the settings is to set the variable in /usr/share/applications/evolution.desktop

change the line:

```
Exec=evolution %U

```

to something like this (in case you do not like to use ECC ciphers with NIST/NSA curves):

```
Exec=env G_TLS_GNUTLS_PRIORITY=${G_TLS_GNUTLS_PRIORITY:-NORMAL:-ECDHE-ECDSA:-ECDHE-RSA} evolution %U

```

The available cipher settings are documented here: [http://gnutls.org/manual/html_node/Priority-Strings.html](http://gnutls.org/manual/html_node/Priority-Strings.html)

A different way to archive this would be some kind of start script:

```
#!/bin/sh

export G_TLS_GNUTLS_PRIORITY=${G_TLS_GNUTLS_PRIORITY:-NORMAL:%COMPAT:\!VERS-SSL3.0}

exec /usr/bin/evolution
```

See also: [https://bugzilla.gnome.org/show_bug.cgi?id=738633#c4](https://bugzilla.gnome.org/show_bug.cgi?id=738633#c4)

## Troubleshooting

If after some system upgrade one gets no accounts in Evolution then all is not lost. First, we can see if we got our account files in ~/.evolution/, if so, then the only solution is to just make a new account in Evolution with the same parameters. (I only lost the signatures

### Failing to Synchronize with Server

If you change internet connections, such as switching VPN or restart X, Evolution may have problems connecting to the mail servers. You would see it endlessly trying to connect in the status bar at the bottom.

A possible solution is to switch to "Work Offline" select "Don't Synchronize” in the pop-up. Then after a minute has passed, go back to On-line mode. It should now have no problem fetching from the mail servers.

## References

[Gnome Evolution Guide](http://library.gnome.org/users/evolution/stable/)

[Tudelft Evolution 2.24 Setup](http://www.tudelft.nl/live/pagina.jsp?id=babae0a3-1479-4501-9ec4-e308153735dc&lang=nl)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Evolution&oldid=415372](https://wiki.archlinux.org/index.php?title=Evolution&oldid=415372)"