[Evolution](https://wiki.gnome.org/Apps/Evolution/) is an application for managing email, calendars, contacts, tasks, and notes. It is the default mail client in [GNOME](/index.php/GNOME "GNOME"). It includes support for IMAP, Microsoft Exchange Server 2007 and 2010, Novell GroupWise, [Kolab](/index.php/Kolab "Kolab"), LDAP, WebDAV, CalDAV, and many other services and protocols.

## Contents

*   [1 Installation](#Installation)
*   [2 IMAP Setup](#IMAP_Setup)
*   [3 Alternative IMAP Setup](#Alternative_IMAP_Setup)
    *   [3.1 OfflineIMAP setup](#OfflineIMAP_setup)
    *   [3.2 Evolution setup for offlineimap's maildir](#Evolution_setup_for_offlineimap.27s_maildir)
*   [4 Gmail Setup](#Gmail_Setup)
    *   [4.1 Receiving Mail](#Receiving_Mail)
    *   [4.2 Sending Mail](#Sending_Mail)
*   [5 Gmail Calendar](#Gmail_Calendar)
*   [6 Google Contacts](#Google_Contacts)
*   [7 Tudelft webmail (Exchange)](#Tudelft_webmail_.28Exchange.29)
*   [8 Using Evolution Outside Of GNOME](#Using_Evolution_Outside_Of_GNOME)
*   [9 Spell Check](#Spell_Check)
*   [10 Tips and tricks](#Tips_and_tricks)
    *   [10.1 Changing cipher settings](#Changing_cipher_settings)
*   [11 Troubleshooting](#Troubleshooting)
    *   [11.1 Failing to Synchronize with Server](#Failing_to_Synchronize_with_Server)
    *   [11.2 Stuck at 'saving user interface' on startup](#Stuck_at_.27saving_user_interface.27_on_startup)
*   [12 References](#References)

## Installation

[Install](/index.php/Install "Install") the [evolution](https://www.archlinux.org/packages/?name=evolution) package.

Additional plugins:

*   **Bogofilter Plugin** — Spam filtering for Evolution, using Bogofilter.

	[https://wiki.gnome.org/Apps/Evolution](https://wiki.gnome.org/Apps/Evolution) || [evolution-bogofilter](https://www.archlinux.org/packages/?name=evolution-bogofilter)

*   **EWS Plugin** — MS Exchange integration through Exchange Web Services.

	[https://wiki.gnome.org/Apps/Evolution](https://wiki.gnome.org/Apps/Evolution) || [evolution-ews](https://www.archlinux.org/packages/?name=evolution-ews)

*   **MAPI Plugin** — MS Exchange integration through OpenChange. (deprecated)

	[https://wiki.gnome.org/Apps/Evolution](https://wiki.gnome.org/Apps/Evolution) || [evolution-mapi](https://aur.archlinux.org/packages/evolution-mapi/)

*   **RSS Plugin** — Enables reading of RSS/RDF/ATOM feeds.

	[http://gnome.eu.org/index.php/Evolution_RSS_Reader_Plugin](http://gnome.eu.org/index.php/Evolution_RSS_Reader_Plugin) || [evolution-rss](https://www.archlinux.org/packages/?name=evolution-rss)

*   **SpamAssassin Plugin** — Spam filtering for Evolution, using SpamAssassin.

	[https://wiki.gnome.org/Apps/Evolution](https://wiki.gnome.org/Apps/Evolution) || [evolution-spamassassin](https://www.archlinux.org/packages/?name=evolution-spamassassin)

## IMAP Setup

This is the setup for a standard IMAP mail address. Go to Edit -> Preferences -> Mail Accounts. Add a mail account insert your Name and real email adress. Then click 'forward' here you are going to select the server type, this is IMAP. Now fill in the textbox server, for the server adress and username. For the rest of the options just follow the wizard. It is very easy, if you get stuck read [this guide](https://help.gnome.org/users/evolution/stable/).

## Alternative IMAP Setup

An alternative to letting Evolution connect directly to the IMAP server is to sync the IMAP server to your PC. This costs as much hard-disk space as you have mail, though it is possible to limit the folders synced in this manner (see below). An additional benefit (primary inspiration for this app) is that you have a full copy of your email, including attachments, on your PC for retrieval, even if on the move without an internet connection.

To set this up, you will need to [install](/index.php/Install "Install") the [offlineimap](https://www.archlinux.org/packages/?name=offlineimap) package (see also [[1]](http://offlineimap.org/)).

### OfflineIMAP setup

OfflineIMAP takes its settings from the file `~/.offlineimaprc`, which you will need to create. For standard IMAP server, most users will be able to use the template file below. See the [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP") for more information.

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
remoterepository = MyMailserver
# Specifies how often to do a repeated sync (if running without crond)
autorefresh = 10

[Repository MyLocal]
type = Maildir
localfolders = /home/path/to/your/maildir
# This needs to be specified so offlineimap does not complain during resync 
sep = .
nametrans = lambda folder: re.sub('^.', *,*
                       re.sub('^$', '.INBOX', folder))

[Repository MyMailserver]
# Example for a gmail account
type = IMAP
remotehost = your.imap.server.com
remoteuser = yourname
remotepass = yourpassword
remoteport = 143
# You need to configure some CA certificates
sslcacertfile = /etc/ssl/certs/ca-certificates.crt
# Translate your INBOX to be the root directory.
# All other directories need a dot before the actual name.
nametrans = lambda folder: re.sub('^.INBOX$', *,*
                       re.sub('^', '.', folder))

```

In case of Gmail instead of standard IMAP server, you will most likely need to add additional translations ( [source](https://medvid.tk/post/2015/02/08/sync-evolution-mail-with-offlineimap/) ).

For remote Mailserver Repository:

```
nametrans = lambda folder: re.sub('^.INBOX$', *,*
                          re.sub('^', '.',
                          re.sub('\.', '_2E',
                          re.sub('^\[Gmail\].Drafts$', 'Drafts',
                          re.sub('^\[Gmail\].Sent Mail$', 'Sent', folder)))))

```

and for local Repository:

```
nametrans = lambda folder: re.sub('^Sent$',   '[Gmail].Sent Mail',
                          re.sub('^Drafts$', '[Gmail].Drafts',
                          re.sub('_2E', '.',
                          re.sub('^.', *,*
                          re.sub('^$', '.INBOX', folder)))))

```

**Warning:** Please note that any space indenting a line of code in `~/.offlineimaprc` would be considered as appending that line to the previous line. In other words, always make sure there is no space before any lines in your config file.

See [OfflineIMAP#Running_offlineimap_in_the_background](/index.php/OfflineIMAP#Running_offlineimap_in_the_background "OfflineIMAP") to configure OfflineIMAP for work in the background.

### Evolution setup for offlineimap's maildir

This is really quite simple, use Evolution's Account Assistant and select the Server Type "Maildir-format mail directories", under the Receiving Email section. Select also the path to your maildir (the 'root' folder if you're using a modified version of the .offlineimaprc above). You can change your 'Checking for New Mail' option to something very short, even 1 minute, since this only checks your local copy and not the server-side copy. SMTP settings are according to normal usage (does not go through offlineimap).

## Gmail Setup

**Note:** Evolution automatically configures your settings in order to receive and send mails via Gmail if you enter your address during the initial setup.

To setup a Gmail account, go to `Edit > Preferences > Mail Accounts` and enter your mail account details.

**Tip:** In [GNOME](/index.php/GNOME "GNOME") you can add a Google account in *GNOME Settings > Online Account* instead.

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

You are now finished with configuring Evolution for Gmail. Just hit Send/Receive in the main screen and wait for new mail. If it still didn't work, go [here](http://tuxicity.wordpress.com/2007/03/08/howto-set-up-gmail-in-evolution-gnomes-mail-client-and-organizer/).

## Gmail Calendar

You can use your Gmail calendar in Evolution here's how:

Go to your calendar in your browser. Click on manage calendars -> the click on the calendar you want to add -> In the Private URL section copy the URL of ICAL (green button).

Now go to Evolution. Click on file -> new -> calendar . In the 'new calendar dialog box' select type: On The Web. You can fill in your own calendar name Then Copy the URL to the URL field

Now you will see your Google calendar in your calendar view in Evolution by the name you gave it in the Name field.

**Variant2 (with evolution-webcal):**

From Evolution click on -> new -> calendar . In the 'new calendar dialog box' select type: Google. You can fill in your own calendar name. Insert your username (not the email). Click the button "Get List" and choose the calendar you want to use.

## Google Contacts

Simarly with the calendar, you can sync your Google contacts in Evolution.

On Evolution, click on File > New > Address Book . Choose Google as type and add your Google account email as the User.

**Note:** The above does not work since Google has turned off the old developer APIs which Evolution uses. You will need to create a GNOME online account (GOA) for your Google account. Install [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) to be able to create a GOA and select what you would like to sync. You can delete/disable any Google addressbooks created in Evolution directly, else you will see two addressbooks

## Tudelft webmail (Exchange)

This is the setup for your tudelft webmail for Evolution. It might also work for other webmail based email accounts.

Go to Edit -> Preferences -> Mail Accounts and make a mail account. For your Email Adress: <netid>@gmail.com . Be carefull your <netid>@student.tudelft.nl must be like this example: E.M.devries@student.tudelft.nl

Receiving mail: Server type: Microsoft Exchange Username: <netid> this is just your netid like this example: edevries OWA URL: [https://webmail.tudelft.nl](https://webmail.tudelft.nl) -> now click 'Authenticate' and fill in your password. The mailbox will be filled in automaticlly

Click Forward: The receiving options are already correct, you can select the option to automaticlly receive email every x minutes.

Click Forward: Now just fill in the name of the mailbox and you are done.

## Using Evolution Outside Of GNOME

In order to use Evolution outside of GNOME desktop you must export [gnome-keyring#Using the keyring outside GNOME](/index.php/Gnome-keyring#Using_the_keyring_outside_GNOME "Gnome-keyring") first.

## Spell Check

You need a local dictionary installed. See the [aspell](/index.php/Aspell "Aspell") article.

## Tips and tricks

### Changing cipher settings

It is possible to change the advertised ciphers used to secure the connetion to the server. Evolution does not provide a switch to change the settings for the used ciphers, however since Evolution uses GnuTLS it is possible to change the settings using environment variables.

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

If after some system upgrade one gets no accounts in Evolution then all is not lost. First, we can see if we got our account files in `~/.evolution/`, if so, then the only solution is to just make a new account in Evolution with the same parameters. (I only lost the signatures

### Failing to Synchronize with Server

If you change internet connections, such as switching VPN or restart X, Evolution may have problems connecting to the mail servers. You would see it endlessly trying to connect in the status bar at the bottom.

A possible solution is to switch to "Work Offline" select "Don't Synchronize” in the pop-up. Then after a minute has passed, go back to On-line mode. It should now have no problem fetching from the mail servers.

### Stuck at 'saving user interface' on startup

This is a known problem and relates to glibc not Evolution hence cannot be fixed. To workaround the problem, before Evolution is closed put the application in 'offline mode' either by clicking on plug and socket icon (in bottom left) or from *File > Work offline*. Next time Evolution is run, put it to online mode to sync all emails. Problem of being stuck at 'saving user interface' will not repeat.

## References

[GNOME Evolution Guide](http://library.gnome.org/users/evolution/stable/)

[Tudelft Evolution 2.24 Setup](http://www.tudelft.nl/live/pagina.jsp?id=babae0a3-1479-4501-9ec4-e308153735dc&lang=nl)