This document describes how to install the CyberPower UPS daemon or alternatively the Network-UPS-Tools. The main advantage of using a CyberPower UPS is that it is cheap and it can communicate with your Linux box through either a RS-232 or USB serial connection. In the event of a prolonged power outage, should the CyberPower UPS lose most of its battery capacity, it can tell the Linux box to perform a safe shutdown.

## Contents

*   [1 Installation of Power Panel](#Installation_of_Power_Panel)
    *   [1.1 Configuration](#Configuration)
    *   [1.2 Running](#Running)
*   [2 Installation of Network UPS Tools](#Installation_of_Network_UPS_Tools)
    *   [2.1 Configuration](#Configuration_2)
        *   [2.1.1 Driver Configuration](#Driver_Configuration)
        *   [2.1.2 upsd Configuration](#upsd_Configuration)
        *   [2.1.3 upsmon Configuration](#upsmon_Configuration)

## Installation of Power Panel

[Install](/index.php/Install "Install") the [powerpanel](https://aur.archlinux.org/packages/powerpanel/) package.

### Configuration

Edit `/etc/pwrstatd.conf`

Email notifications can be accomplished by editing `/etc/powerpanel/pwrstatd-powerfail.sh` and `/etc/powerpanel/pwrstatd-lowbatt.sh`

**Warning:** Make sure the path to the email script at the bottom of these scripts is correct. It should be `/etc/powerpanel/pwrstatd-email.sh`

### Running

[Start/enable](/index.php/Start/enable "Start/enable") `pwrstatd.service`.

Then run `# pwrstat -status`. You should get something like this:

```

The UPS information shows as following:

        Properties:
                Model Name...................  Value 1500E
                Firmware Number.............. BFF7104#7N5
                Rating Voltage............... 230 V
                Rating Power................. 900 Watt

        Current UPS status:
                State........................ Normal
                Power Supply by.............. Utility Power
                Utility Voltage.............. 230 V
                Output Voltage............... 230 V
                Battery Capacity............. 100 %
                Remaining Runtime............ 61 min.
                Load......................... 126 Watt(14 %)
                Line Interaction............. None
                Test Result.................. Unknown
                Last Power Event............. None

```

## Installation of Network UPS Tools

If you do not wish to use powerpanel, the [Network UPS Tools (NUT)](http://networkupstools.org/) offers an alternative for some UPS; not all are supported. It's worth checking the [Hardware Compatibility List](http://networkupstools.org/stable-hcl.html) to see if your UPS is supported. Only one of these programs is required to monitor and shut the system down; you shouldn't use both as they might interfere with one another.

You can install network-ups-tools ([network-ups-tools](https://aur.archlinux.org/packages/network-ups-tools/)) from [AUR](/index.php/AUR "AUR").

### Configuration

NUT has 3 daemons associated with it:

*   The driver which communicates with the UPS
*   A server (upsd) which uses the driver to report out the status of the UPS
*   And a monitoring daemon (upsmon) which monitors the upsd server and takes action based on information it receives.

The idea is that if you have multiple systems connected to the UPS, one can communicate the status of the UPS over the network and the others can monitor that status by running their own upsmon services. NUT has [extensive documentation on the configuration](http://networkupstools.org/docs/user-manual.chunked/ar01s06.html#_configuring_and_using) however this is going to walk through a simple setup of a USB UPS and the associated server and monitor all in one system (common desktop configuration).

#### Driver Configuration

Edit `/etc/ups/ups.conf`

The configuration here will depend on the type of UPS you have. For a simple usb-hid compatible UPS:

```
[powerplant]                                                                
    driver = usbhid-ups                                                     
    port = auto 

```

That creates a new UPS called "powerplant". You can name the device whatever you like. If you don't have a usbhid-ups, the previously mentioned Hardware Compatibility List may help, or you can run the "nut-scanner" command which may be able to poll the system for attached UPS.

#### upsd Configuration

Optionally Edit `/etc/ups/upsd.conf`

Then Edit `/etc/ups/upsd.users`

The default upsd.conf will work. It is configured by default to only listen on localhost so if you ever wish to add network monitors, you will need to adjust this file. For our basic configuration though, this will work fine.

upsd.users however needs to be configured with a user so we can issue commands to the server and monitor it. You should populate it with a user and password.

```
[scottie]                                                                  
     password = warpspeed                                                     
     actions = SET                                                           
     instcmds = ALL                                                          

```

At this point you should be able to start up nut-server (which will automatically start nut-driver).

```
# systemctl start nut-server
# systemctl enable nut-server

```

If it has started successfully, you can run upsc <upsname> to get info from the ups. Example output would be:

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

#### upsmon Configuration

The last step is to configure upsmon to listen to upsd and take action. At least one line is needed to configure upsmon to log in with the username and password you set in upsd.users.

```
MONITOR powerplant@localhost 1 scottie warpspeed master 

```

The file also configures what alerts are sent and where they are sent and what action is taken when the battery is low so you should probably review and make your desired changes.

Then [start/enable](/index.php/Start/enable "Start/enable") `ups-monitor.service`.

Your logs should show upsmon starting and monitoring the ups.