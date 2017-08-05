[Lantern](https://getlantern.org/en_US/) is a free peer-to-peer internet censorship circumvention software.

## Contents

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
    *   [2.1 Client](#Client)
    *   [2.2 Chrome](#Chrome)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [lantern-bin](https://aur.archlinux.org/packages/lantern-bin/) package.

## Setup

Now the lantern has a web client ([http://127.0.0.1:xxxx](http://127.0.0.1:xxxx)) interfaces.

### Client

The client is started with the `lantern` command.To start it using the configuration file `~/.lantern/setting.yaml`:

```
$ lantern

```

### Chrome

For Chrome users you might need to install the plugin [Proxy SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega),follow the instructions below:

	Get proxy server address and port

	In lantern set-up page,click Lantern=>Settings=>Advanced Settings,and remember the server address and port

	Edit the Proxy Profile

	In SwitchyOmega option page,edit the example file,fill in the address and port you get above

	Enable the profile

	When viewing blocked websites,run lantern and select the above proxy profile,enjoy it!

## See also

*   [Lantern website](https://getlantern.org)
*   [GitHub project](https://github.com/getlantern/lantern)