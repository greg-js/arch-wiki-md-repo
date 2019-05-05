Related articles

*   [Postfix#SpamAssassin](/index.php/Postfix#SpamAssassin "Postfix")

[SpamAssassin](https://spamassassin.apache.org/) is a mail filter to identify spam.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Updating rules](#Updating_rules)
*   [3 Plugins](#Plugins)
    *   [3.1 ClamAV](#ClamAV)
    *   [3.2 Razor](#Razor)

## Installation

Install the [spamassassin](https://www.archlinux.org/packages/?name=spamassassin) package.

## Usage

Go over `/etc/mail/spamassassin/local.cf` and configure it to your needs.

### Updating rules

Update the SpamAssassin matching patterns and compile them:

```
# sa-update && sa-compile

```

You will want to run this periodically, the best way to do so is by setting up a [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

Create the following service, which will run these commands:

 `/etc/systemd/system/spamassassin-update.service` 
```
[Unit]
Description=spamassassin housekeeping stuff
After=network.target

[Service]
#User=spamd
#Group=spamd
Type=oneshot

# remove --allowplugins, if you do not want plugin updates from SA.
ExecStart=sudo -u spamd /usr/bin/vendor_perl/sa-update --allowplugins
SuccessExitStatus=1
ExecStart=sudo -u spamd /usr/bin/vendor_perl/sa-compile
ExecStart=/usr/bin/systemctl -q --no-block try-restart spamassassin.service

# uncomment the following ExecStart line to train SA's bayes filter
# and specify the path to the mailbox that contains spam email(s)
#ExecStart=/usr/bin/vendor_perl/sa-learn --spam <path_to_your_spam_mailbox>
```

Then create the timer, which will execute the previous service daily:

 `/etc/systemd/system/spamassassin-update.timer` 
```
[Unit]
Description=spamassassin house keeping

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```

Now you can [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `spamassassin-update.timer`.

## Plugins

### ClamAV

Install and setup clamd as described in [ClamAV](/index.php/ClamAV "ClamAV").

Follow one of the above instructions to call SpamAssassin from within your mail system.

[Install](/index.php/Install "Install") the [perl-cpanplus-dist-arch](https://www.archlinux.org/packages/?name=perl-cpanplus-dist-arch) package. Then install the ClamAV perl library as follows:

```
 # /usr/bin/vendor_perl/cpanp -i File::Scan::ClamAV

```

Add the 2 files from [http://wiki.apache.org/spamassassin/ClamAVPlugin](http://wiki.apache.org/spamassassin/ClamAVPlugin) into `/etc/mail/spamassassin/`. Edit `/etc/mail/spamassassin/clamav.pm` and update `$CLAM_SOCK` to point to your Clamd socket location (default is `/run/clamav/clamd.ctl`).

Finally, [restart](/index.php/Restart "Restart") `spamassassin.service`.

### Razor

**Note:** The last version was released 2008.[[1]](https://sourceforge.net/projects/razor/files/razor-agents/)

[Vipul's Razor](http://razor.sourceforge.net/) is a distributed, collaborative, spam detection and filtering network.

Make sure you have installed SpamAssassin first, then:

[Install](/index.php/Install "Install") the [razor](https://www.archlinux.org/packages/?name=razor) package.

Register with Razor.

```
 # mkdir /etc/mail/spamassassin/razor
 # chown spamd:spamd /etc/mail/spamassassin/razor
 # sudo -u spamd -s
 $ cd /etc/mail/spamassassin/razor
 $ razor-admin -home=/etc/mail/spamassassin/razor -register
 $ razor-admin -home=/etc/mail/spamassassin/razor -create
 $ razor-admin -home=/etc/mail/spamassassin/razor -discover

```

To tell SpamAssassin about Razor, add the following line to `/etc/mail/spamassassin/local.cf`:

```
 razor_config /etc/mail/spamassassin/razor/razor-agent.conf

```

To tell Razor about itself, add the following line to `/etc/mail/spamassassin/razor/razor-agent.conf`:

```
 razorhome = /etc/mail/spamassassin/razor/

```

Finally, [restart](/index.php/Restart "Restart") `spamassassin.service`.