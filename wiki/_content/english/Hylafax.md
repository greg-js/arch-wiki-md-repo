From [HylaFAX home page](http://www.hylafax.org/content/Main_Page):

	HylaFAX is an enterprise-class system for sending and receiving facsimiles as well as for sending alpha-numeric pages. The software is designed around a client-server architecture. Fax modems may reside on a single machine on a network and clients can submit an outbound job from any other machine on the network. Client software is designed to be lightweight and easy to port. HylaFAX is designed to be very robust and reliable. The fax server is designed to guard against unexpected failures in the software, in the configuration, in the hardware and in general use. HylaFAX can support multiple modems and a heavy traffic load. If you expect to send more than a few facsimiles a day, then HylaFAX is the fax package for you!

## Contents

*   [1 Setup](#Setup)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 FaxDispatch](#FaxDispatch)
    *   [2.2 Pagesize](#Pagesize)
    *   [2.3 No dialtone error or if you are a laptop user](#No_dialtone_error_or_if_you_are_a_laptop_user)
    *   [2.4 For laptop users it might be helpfull to deactivate the dialtone check](#For_laptop_users_it_might_be_helpfull_to_deactivate_the_dialtone_check)
    *   [2.5 Automatic fax printing](#Automatic_fax_printing)
    *   [2.6 Disabling MTA actions](#Disabling_MTA_actions)
    *   [2.7 Enable automatic printing of notifications](#Enable_automatic_printing_of_notifications)
    *   [2.8 Useful commands](#Useful_commands)
*   [3 Frontends for HylaFAX](#Frontends_for_HylaFAX)

## Setup

[Install](/index.php/Install "Install") the [hylafax](https://www.archlinux.org/packages/?name=hylafax) package.

It could be that you need a MTA installed like [Postfix](/index.php/Postfix "Postfix"):

*   After installation please run `# faxsetup`. Answer the questions and modify to your needs.

*   Run `# faxaddmodem`. It asks you for the device, leave out the `/dev` prefix; only enter eg. modem, ttyS0 or such things.

*   Answer the other questions, important ones could be the ringtones, max pages, permissions on files or your the name that should be shown.

*   [Enable](/index.php/Enable "Enable") the service for the daemon. Assuming your modem is on ttyS0, the service would be `faxgetty@ttyS0.service`.

*   The package contains further services and [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") to [start/enable](/index.php/Start/enable "Start/enable") for your usage. For example, `hfaxd.service` and `faxq.service`.

Your received faxes will be saved in `/var/spool/hylafax/rcvq/` and deleted after 30 days. Your sent faxes will be saved in `/var/spool/hylafax/sendq/`.

## Tips and tricks

### FaxDispatch

You can create a FaxDispatch file that will allow you to convert incoming faxes to pdf or other and direct where these are sent. Examples are all over the Internet, but be aware that FaxDispatch does **not** go into `/etc`, but rather into `/var/spool/hylafax/etc`.

A simple FaxDispatch that converts to pdf and sends the fax to a particular address would be:

```
FILETYPE=pdf
SENDTO=myaddress@myemail.whatever

```

### Pagesize

HylaFAX defaults are made for North America settings. Pagesize of send faxes can be adjusted in `/usr/lib/fax/pagesizes` for A4 default setup please change the file to that:

```
---snip
Japanese Legal          JP-LEG  12141   17196   11200    15300  900     400
#
#default        NA-LET  10200   13200    9240    12400  472     345
default         A4      9920    14030   9240    13200   472     345
---snap

```

### No dialtone error or if you are a laptop user

If you need a special number to get the Dialtone add this to:

```
/var/spool/hylafax/etc/config.*yourdevicename*

```

Uncomment the `ModemDialCmd` line, and change `ATDT%s` to `ATDT*yournumber*%s`

### For laptop users it might be helpfull to deactivate the dialtone check

Uncomment the `ModemDialCmd` line, and change `ATDT%s` to `ATX3DT%s`

### Automatic fax printing

Add this to `/var/spool/hylafax/bin/faxrcvd` at the end:

```
/usr/bin/tiff2ps -a -h 11.1082 -w 7.8543 $FILE | /usr/bin/lpr -P *yourprintername*

```

This setup is for A4 pagesize, adjust -h and -w to your needs if you need an other size.

### Disabling MTA actions

Normally HylaFAX uses a MTA to receive faxes, if you do not need that change, your `/var/spool/hylafax/bin/faxrcvd`.

Change `NOTIFY_FAXMASTER=always` to `never`

### Enable automatic printing of notifications

If you want notifications to be printed out and not mailed, change your `/var/spool/hylafax/bin/notify`

1.  Change `NOTIFY_FAXMASTER=never` to `always` and at the end of that file.
2.  Comment this line: `) || 2>&1 $SENDMAIL -f$FROMADDR -oi -t` 
3.  Add this as next line: `) || 2>&1 lpr -P ''yourprinter'' -p` 

Remember to add your changed file to pacmans NoUpgrade list else your changes might get lost on update.

### Useful commands

```
faxstat (shows you the status of HylaFAX)
faxstat -s (shows you the send status)
faxstat -r (shows received faxes)
faxalter -a now *jobid* (forces send retry now)
faxrm *jobid* (deletes fax from sendqueue)

```

For more options please read the manpages of each program.

## Frontends for HylaFAX

GNU/Linux Apps:

*   Avantfax is a PHP56, MySQL enterprise class frontend to HylaFAX (by one of the HylaFAX developers David Mimms). Get it here: [http://www.avantfax.com/download.php](http://www.avantfax.com/download.php)
*   kfax is a nice app to view the received tiff files.
*   KDE has a printer to send your document to fax, change it to use the HylaFAX backend.

Windows Apps:

*   WFHC is a nice HylaFAX client for Windows. Get it here: [http://www.uli-eckhardt.de/whfc/](http://www.uli-eckhardt.de/whfc/).
*   SuSEfax is also a nice client for Windows. Get it here: [ftp://ftp.suse.com/pub/suse/discontinued/i386/SuSEFax_WIN32](ftp://ftp.suse.com/pub/suse/discontinued/i386/SuSEFax_WIN32).