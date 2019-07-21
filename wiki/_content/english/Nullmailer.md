Nullmailer is a small mail program that allows you (or your system) to send mails through an existing email account (using an SMTP server). Technically, this is an [MTA](https://en.wikipedia.org/wiki/Message_transfer_agent "wikipedia:Message transfer agent"). Nullmailer is particularly useful on systems that are not always online (like a travelling laptop).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Example: gmail](#Example:_gmail)
    *   [2.2 Other configurations](#Other_configurations)
*   [3 Testing](#Testing)
*   [4 References](#References)

## Installation

[Install](/index.php/Install "Install") the package [nullmailer](https://www.archlinux.org/packages/?name=nullmailer).

## Configuration

Configuration files are located in /etc/nullmailer. Each file contains one option and the possible configurations are not particularly well documented. Below we give an example of a configuration to use gmail as a relay host.

After setting the configurations, start and/or enable the [systemd](/index.php/Systemd "Systemd") service "nullmailer"

### Example: gmail

In the file /etc/nullmailer/remotes you need to set the connection to the relay host. For gmail:

```
smtp.gmail.com smtp --port=465 --auth-login --user=<gmail address> --pass=<password> --ssl

```

You can also use starttls but to the author SSL is preferable.

**Note:** You are encoding your password in this file. Make sure the permissions are set correctly so that only you can read it. The default settings are safe, but please check.

In the file /etc/nullmailer/me, you need to encode the hostname of your computer. This was set up correctly by the installation.

In the file /etc/nullmailer/defaultdomain, you need to set the gmail domain:

```
gmail.com

```

**Note:** In the configuration after installation, this file is missing. However, it is required by the systemd unit file. If you get an error message
```
Condition check resulted in Nullmailer relay-only MTA being skipped.

```
in the journal (through journalctl -u nullmailer), this might refer to this file.

### Other configurations

In the file /etc/nullmailer/pausetime you can set the minimum time to pause between successive queue runs when there are messages in the queue, in seconds. This defaults to 60, which for the author's usage (travelling laptop) is way too soon. You can set this to one hour for example:

```
3600

```

In the file /etc/nullmailer/sendtimeout you can set how long nullmailer tries to send a particular message before giving up. The default is one hour, 3 minutes might be a more reasonable cutoff:

```
180

```

## Testing

You can test the configuration by sending a test email:

```
 echo "Subject: sendmail test" | sendmail -v <recipient address>

```

## References

Information about nullmailer is a bit spread out over the internet.

*   An old blogpost, not accurate anymore, on when nullmailer was introduced in the [AUR](/index.php/AUR "AUR"): [flexion.org/posts/2013-03-nullmailer-on-arch-linux](https://flexion.org/posts/2013-03-nullmailer-on-arch-linux/).
*   Official page, only a reference to a mailing list: [untroubled.org/nullmailer](http://untroubled.org/nullmailer/).
*   A "for Dummies" style blog post with useful configuration tips: [www.troubleshooters.com/linux/nullmailer](http://www.troubleshooters.com/linux/nullmailer/).