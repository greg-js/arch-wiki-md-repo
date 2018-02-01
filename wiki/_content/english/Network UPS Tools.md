This document describes how to install the [Network UPS Tools (NUT)](http://networkupstools.org/). Network UPS Tools is compatible with thousands models of UPS. You can check the [Hardware Compatibility List](http://networkupstools.org/stable-hcl.html) to see if your UPS is supported.

## Contents

*   [1 Installation of Network UPS Tools](#Installation_of_Network_UPS_Tools)
    *   [1.1 Configuration](#Configuration)
        *   [1.1.1 Driver configuration](#Driver_configuration)
        *   [1.1.2 upsd configuration](#upsd_configuration)
        *   [1.1.3 upsmon configuration](#upsmon_configuration)

## Installation of Network UPS Tools

You can install network-ups-tools ([network-ups-tools](https://aur.archlinux.org/packages/network-ups-tools/)) from [AUR](/index.php/AUR "AUR").

### Configuration

NUT has 3 daemons associated with it:

*   The driver which communicates with the UPS.
*   A server (upsd) which uses the driver to report out the status of the UPS.
*   A monitoring daemon (upsmon) which monitors the upsd server and takes action based on information it receives.

The idea is that if you have multiple systems connected to the UPS, one can communicate the status of the UPS over the network and the others can monitor that status by running their own upsmon services. NUT has [extensive documentation on the configuration](http://networkupstools.org/docs/user-manual.chunked/ar01s06.html#_configuring_and_using) however this is going to walk through a simple setup of a USB UPS and the associated server and monitor all in one system (common desktop configuration).

#### Driver configuration

The configuration here will depend on the type of UPS you have. Consult the previously mentioned Hardware Compatibility List to find what driver will likely work for your UPS. You can run the tool [nut-scanner(8)](http://networkupstools.org/docs/man/nut-scanner.html) which will detect NUT-compatible devices attached to your system.

For many UPS connected by USB, use the [usbhid-ups(8)](http://networkupstools.org/docs/man/usbhid-ups.html) driver.

 `/etc/ups/ups.conf` 
```
...
[*upsname*]
    driver = usbhid-ups
    port = auto

```

You can name the UPS device whatever you like. [ups.conf(5)](http://networkupstools.org/docs/man/ups.conf.html)

#### upsd configuration

By default upsd listens only on localhost and this is fine for our purpose. Though it is not necessary for following this guide, you can configure upsd beyond the defaults by editing `/etc/ups/upsd.conf`. See [upsd.conf(5)](http://networkupstools.org/docs/man/upsd.conf.html).

You will need to add a user for a monitor to connect to the server and issue commands. See [upsd.users(5)](http://networkupstools.org/docs/man/upsd.users.html).

 `/etc/ups/upsd.users` 
```
...
[*upsuser*]
     password = *password*
     actions = SET
     instcmds = ALL

```

At this point you should be able to [start/enable](/index.php/Start/enable "Start/enable") `nut-server.service` which will automatically start nut-driver.

If it has started successfully, you can run `upsc <upsname>` to get information from the UPS. Example output from the command:

```
battery.charge: 100
battery.charge.low: 10
battery.charge.warning: 20
battery.mfr.date: CPS
battery.runtime: 5550
battery.runtime.low: 300
battery.type: PbAcid
battery.voltage: 13.5
battery.voltage.nominal: 12
device.mfr: CPS
device.model: UPS CP1000AVRLCD
device.type: ups
driver.name: usbhid-ups
driver.parameter.pollfreq: 30
driver.parameter.pollinterval: 2
driver.parameter.port: auto
driver.parameter.synchronous: no
driver.version: 2.7.4
driver.version.data: CyberPower HID 0.4
driver.version.internal: 0.41
input.transfer.high: 140
input.transfer.low: 90
input.voltage: 122.0
input.voltage.nominal: 120
output.voltage: 122.0
ups.beeper.status: disabled
ups.delay.shutdown: 20
ups.delay.start: 30
ups.load: 0
ups.mfr: CPS
ups.model: UPS CP1000AVRLCD
ups.productid: 0501
ups.realpower.nominal: 600
ups.status: OL
ups.test.result: Done and passed
ups.timer.shutdown: -60
ups.timer.start: 0
ups.vendorid: 0764

```

#### upsmon configuration

The last step is to configure upsmon to listen to upsd and take action on events.

Add the following line to `/etc/ups/upsmon.conf`:

```
MONITOR *upsname*@localhost 1 *upsduser* *password* master

```

Here *upsname* is the name of the UPS, and *upsduser* and *password* is the user and its password you set in `/etc/ups/upsd.user`.

You can also configure what alerts are sent, where they are sent, what action is taken when the battery is low, and more. See [upsmon.conf(5)](http://networkupstools.org/docs/man/upsmon.conf.html).

Then [start/enable](/index.php/Start/enable "Start/enable") `nut-monitor.service`.

Your logs should show upsmon starting and monitoring the UPS.