# systemd/Timers

Related articles

*   [systemd](/index.php/Systemd "Systemd")
*   [systemd/User](/index.php/Systemd/User "Systemd/User")
*   [systemd FAQ](/index.php/Systemd_FAQ "Systemd FAQ")
*   [cron](/index.php/Cron "Cron")

Timers are [systemd](/index.php/Systemd "Systemd") unit files whose name ends in `.timer` that control `.service` files or events. Timers have the ability to be an alternative to [cron](/index.php/Cron "Cron") (read [#As a cron replacement](#As_a_cron_replacement)). Timers have built-in support for calendar time events, monotonic time events, and have the ability to run asynchronously.

## Contents

*   [1 Timer units](#Timer_units)
*   [2 Service unit](#Service_unit)
*   [3 Management](#Management)
*   [4 Example](#Example)
    *   [4.1 Monotonic timer](#Monotonic_timer)
    *   [4.2 Realtime timer](#Realtime_timer)
*   [5 As a cron replacement](#As_a_cron_replacement)
    *   [5.1 Benefits](#Benefits)
    *   [5.2 Caveats](#Caveats)
    *   [5.3 MAILTO](#MAILTO)
    *   [5.4 Using a crontab](#Using_a_crontab)
*   [6 See also](#See_also)

## Timer units

Timers are _systemd_ unit files with a suffix of `.timer`. Timers are like other [unit configuration files](/index.php/Systemd#Writing_unit_files "Systemd") and are loaded from the same paths but include a `[Timer]` section. The `[Timer]` section defines when and how the timer activates. Timers are defined as one of two types:

*   **Monotonic timers** activate after a time span relative to a varying starting point. There are number of different monotonic timers but all have the form of: `On_Type_Sec=`. `OnBootSec` and `OnActiveSec` are common monotonic timers.
*   **Realtime timers** (a.k.a. wallclock timers) activate on a calendar event (like cronjobs). The option `OnCalendar=` is used to define them.

For a full explanation of timer options, see the `systemd.timer(5)` [man page](/index.php/Man_page "Man page"). The argument syntax for calendar events and time spans is defined on the `systemd.time(7)` [man page](/index.php/Man_page "Man page").

## Service unit

For each `.timer` file, a matching `.service` file exists (e.g. `foo.timer` and `foo.service`). The `.timer` file activates and controls the `.service` file. The `.service` does not require an `[Install]` section as it is the _timer_ units that are enabled. If necessary, it is possible to control a differently-named unit using the `Unit=` option in the timer's `[Timer]` section.

## Management

To use a _timer_ unit [enable](/index.php/Enable "Enable") and start it like any other unit (remember to add the `.timer` suffix). To view all started timers, run:

 `$ systemctl list-timers` 

```
NEXT                          LEFT        LAST                          PASSED     UNIT                         ACTIVATES
Thu 2014-07-10 19:37:03 CEST  11h left    Wed 2014-07-09 19:37:03 CEST  12h ago    systemd-tmpfiles-clean.timer systemd-tmpfiles-clean.service
Fri 2014-07-11 00:00:00 CEST  15h left    Thu 2014-07-10 00:00:13 CEST  8h ago     logrotate.timer              logrotate.service

```

**Note:**

*   To list all timers (including inactive), use `systemctl list-timers --all`.
*   The status of a service started by a timer will likely be inactive unless it is currently being triggered.
*   If a timer gets out of sync, it may help to delete its `stamp-*` file in `/var/lib/systemd/timers`. These are zero length files which mark the last time each timer was run. If deleted, they will be reconstructed on the next start of their timer.

## Example

No changes to service unit files are needed to schedule them with a timer. The following example schedules `foo.service` to be run with a corresponding timer called `foo.timer`.

### Monotonic timer

A timer which will start 15 minutes after boot and again every week while the system is running.

 `/etc/systemd/system/foo.timer` 

```
[Unit]
Description=Run foo weekly and on boot

[Timer]
OnBootSec=15min
OnUnitActiveSec=1w 

[Install]
WantedBy=timers.target

```

### Realtime timer

A timer which starts once a week (at 12:00am on Monday). It starts once immediately if it missed the last start time (option `Persistent=true`), for example due to the system being powered off:

 `/etc/systemd/system/foo.timer` 

```
[Unit]
Description=Run foo weekly

[Timer]
OnCalendar=weekly
Persistent=true     

[Install]
WantedBy=timers.target
```

**Tip:** Special event expressions like `daily` and `weekly` refer to _specific start times_ and thus any timers sharing such calendar events will start simultaneously. Timers sharing start events can cause poor system performance if the timers' services compete for system resources. Consider manually staggering such timers using specific events e.g. `OnCalendar=Wed 23:15`. See [#Caveats](#Caveats).

## As a cron replacement

Although [cron](/index.php/Cron "Cron") is arguably the most well-known job scheduler, _systemd_ timers can be an alternative.

### Benefits

The main benefits of using timers come from each job having its own _systemd_ service. Some of these benefits are:

*   Jobs can be easily started independently of their timers. This simplifies debugging.
*   Each job can be configured to run in a specific environment (see the `systemd.exec(5)` [man page](/index.php/Man_page "Man page")).
*   Jobs can be attached to [cgroups](/index.php/Cgroups "Cgroups").
*   Jobs can be set up to depend on other _systemd_ units.
*   Jobs are logged in the _systemd_ journal for easy debugging.

### Caveats

Some things that are easy to do with cron are difficult or impossible to do with timer units alone.

*   Complexity: to set up a timed job with _systemd_ you create two files and run a couple `systemctl` commands. Compare that to adding a single line to a crontab.
*   Emails: there is no built-in equivalent to cron's `MAILTO` for sending emails on job failure. See the next section for an example of setting up an equivalent using `OnFailure=`.
*   Random delay: there is no built-in equivalent to cron's `RANDOM_DELAY` for randomly spreading timers out across a given interval (see [bug report](https://bugs.freedesktop.org/show_bug.cgi?id=82084), [test results](https://wiki.archlinux.org/index.php?title=Talk:Systemd/Timers&oldid=356408#Parallelization_section_is_confusing)). Services which you do not want to run concurrently must have their timers manually set to minimize overlap.

NaN

### MAILTO

You can set up systemd to send an e-mail when a unit fails - much like Cron does with `MAILTO`. First you need two files: an executable for sending the mail and a _.service_ for starting the executable. For this example, the executable is just a shell script using `sendmail`:

 `/usr/local/bin/systemd-email` 

```
#!/bin/bash

/usr/bin/sendmail -t <<ERRMAIL
To: $1
From: systemd <root@$HOSTNAME>
Subject: $2
Content-Transfer-Encoding: 8bit
Content-Type: text/plain; charset=UTF-8

$(systemctl status --full "$2")
ERRMAIL
```

Whatever executable you use, it should probably take at least two arguments as this shell script does: the address to send to and the unit file to get the status of. The _.service_ we create will pass these arguments:

 `/etc/systemd/system/status-email-user1@.service` 

```
[Unit]
Description=status email for %I to user1

[Service]
Type=oneshot
ExecStart=/usr/local/bin/systemd-email user1@mailhost %i
User=nobody
Group=systemd-journal

```

First notice that the unit to send email about is an instance parameter, so this one service can be used to send email for many other units. However the recipient is hard-coded (since unit templates can only take a single parameter) so you will need to create multiple services if you want to send emails to different sets of recipients. At this point you should test the service to verify that you can receive the emails:

 `# systemctl start status-email-user1@dbus.service` 

Then simply add `OnFailure=status-email-user1@%n.service` to the `[Unit]` section of any unit you want emails for. `%n` passes the unit's name to the template.

**Note:** If you set up SSMTP security according to [SSMTP#Security](/index.php/SSMTP#Security "SSMTP") the user `nobody` will not have access to `/etc/ssmtp/ssmtp.conf`, and the `systemctl start status-email-user1@dbus.service` command will fail. One solution is to use `root` as the User in the `status-email-user1@.service` module.

### Using a crontab

Several of the caveats can be worked around by installing a package that parses a traditional crontab to configure the timers. [systemd-crontab-generator](https://aur.archlinux.org/packages/systemd-crontab-generator/)<sup><small>AUR</small></sup> and [systemd-cron](https://aur.archlinux.org/packages/systemd-cron/)<sup><small>AUR</small></sup> are two such packages. These can provide the missing `MAILTO` and `RANDOM_DELAY` features.

If you like crontabs just because they provide a unified view of all scheduled jobs, `systemctl` can provide this. See [#Management](#Management).

## See also

*   [systemd.timer man page](http://www.freedesktop.org/software/systemd/man/systemd.timer.html) on freedesktop.org
*   [Fedora Project wiki page](https://fedoraproject.org/wiki/Features/SystemdCalendarTimers) on _systemd_ calendar timers
*   [Gentoo wiki section](https://wiki.gentoo.org/wiki/Systemd#Timer_services) on _systemd_ timer services
*   **systemd-crontab-generator** — tool to generate timers/services from crontab and anacrontab files

NaN

*   **systemd-cron** — provides systemd units to run cron scripts; using _systemd-crontab-generator_ to convert crontabs

NaN

Retrieved from "[https://wiki.archlinux.org/index.php?title=Systemd/Timers&oldid=410718](https://wiki.archlinux.org/index.php?title=Systemd/Timers&oldid=410718)"