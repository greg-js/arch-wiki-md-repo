[FireHOL](http://firehol.org) is a language (and a program to run it) which builds secure, stateful firewalls from easy to understand, human-readable configurations. The configurations stay readable even for very complex setups.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Try, Run and Enable](#Try.2C_Run_and_Enable)
*   [4 Related](#Related)

## Installation

Install [Firehol](http://aur.archlinux.org/packages/firehol/) or [Firehol-git](http://aur.archlinux.org/pkgbase/firehol-git/) from AUR.

## Configuration

Configuration file is at `/etc/firehol/firehol.conf`

Copy example config from [Firehol example](http://firehol.org/#firehol)

The configuration file is bash file and has 3 parts

*   helper
*   interface
*   router

## Try, Run and Enable

You can try the config file is correct or not by

```
   sudo firehol try

```

or

```
   sudo firehol nofast try

```

If the config is working, run the Firehol by

```
   systemctl start firehol

```

Enable Firehol to run at boot time by

```
   systemctl enable firehol

```

## Related

You may configure Fireqos for QoS and NetData for monitoring