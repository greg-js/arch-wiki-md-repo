[Postgrey](http://postgrey.schweikert.ch/) can be used to enable greylisting for a Postfix mail server.

## Installation

[Install](/index.php/Install "Install") the [postgrey](https://www.archlinux.org/packages/?name=postgrey) package. To get it running quickly edit the Postfix configuration file and add these lines:

 `/etc/postfix/main.cf` 

```
smtpd_recipient_restrictions =
  check_policy_service inet:127.0.0.1:10030

```

Then [start/enable](/index.php/Start/enable "Start/enable") the `postgrey` service. Afterwards, reload the `postfix` service. Now greylisting should be enabled.

## Configuration

Configuration is done via editing the `greylist.service` file. First copy it over to edit it.

```
# cp /usr/lib/systemd/system/postgrey.service /etc/systemd/system/

```

Now you can edit it. For example, to add automatic whitelisting (successful deliveries are whitelisted and don't have to wait any more), you could add the `--auto-whitelist-clients=N` option and replace `N` by a suitably small number (or leave it at its default of 5).

For a full documentation of possible options see `perldoc postgrey`.