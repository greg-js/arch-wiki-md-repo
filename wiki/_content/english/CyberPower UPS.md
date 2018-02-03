This document describes how to install the CyberPower UPS daemon PowerPanel or alternatively the Network-UPS-Tools. The main advantage of using a CyberPower UPS is that it is cheap and it can communicate with your Linux box through either a RS-232 or USB serial connection. In the event of a prolonged power outage, should the CyberPower UPS lose most of its battery capacity, it can tell the Linux box to perform a safe shutdown.

## Contents

*   [1 Using PowerPanel](#Using_PowerPanel)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
    *   [1.3 Running](#Running)
*   [2 Using Network UPS Tools](#Using_Network_UPS_Tools)

## Using PowerPanel

### Installation

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

## Using Network UPS Tools

If you do not wish to use PowerPanel, the [Network UPS Tools (NUT)](http://networkupstools.org/) is an alternative. Only one of these programs (PowerPanel or NUT) is required to monitor and shut the system down. You shouldn't use both as they might interfere with one another.

Use instructions from the Wiki page of [Network UPS Tools](/index.php/Network_UPS_Tools "Network UPS Tools").