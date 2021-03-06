Related articles

*   [CUPS](/index.php/CUPS "CUPS")
*   [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems")

**Note:** See [CUPS](/index.php/CUPS "CUPS") for the main article, and [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems") for information on non-CAPT Canon printers

CAPT (*Canon Advanced Printing Technology*) is Canon's proprietary driver, supporting the **Canon i-Sensys** series of laser printers. For more information, see [Setting up CAPT printers on Ubuntu](https://help.ubuntu.com/community/CanonCaptDrv190).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 CAPT status monitor](#CAPT_status_monitor)
    *   [3.1 Local CUPS](#Local_CUPS)
    *   [3.2 Remote CUPS](#Remote_CUPS)
        *   [3.2.1 Client configuration](#Client_configuration)
        *   [3.2.2 Server configuration](#Server_configuration)

## Installation

[Install](/index.php/Install "Install") the [capt-src](https://aur.archlinux.org/packages/capt-src/) package. It depends on 32-bit library packages and requires [enabling multilib](/index.php/Official_repositories#Enabling_multilib "Official repositories").

There is also an open source CAPT driver in *early alpha stage* not described here, available as [captdriver-git](https://aur.archlinux.org/packages/captdriver-git/).

## Configuration

Canon's driver uses a local daemon to communicate with the printer, and wraps that using a CUPS driver.

To configure the printer, follow the [CUPS](/index.php/CUPS "CUPS") article, adding a *CAPT printer* and using a [Printer URI](/index.php/CUPS#Printer_URI "CUPS") of `ccp://localhost:59787`. Find the right model using `lpinfo -m`, or check the table provided on the [Ubuntu help page](https://help.ubuntu.com/community/CanonCaptDrv190), which matches each supported printer with its corresponding PPD.

**Note:**

*   Installing CAPT printers via the [CUPS](/index.php/CUPS "CUPS") web interface may not work [[1]](http://askubuntu.com/a/464334). Instead, use the [CLI tools](/index.php/CUPS#CLI_tools "CUPS").
*   If port `59787` doesn't work, try port `59**6**87`.
*   Some models have multiple PPDs, where the last letter indicates the regional model (J = Japan, K = United Kingdom, S = United States)

Next, register the printer with the CAPT driver itself via *ccpdadmin*. Replace `*queue_name*` with the queue descriptive name and `*printer_address*` with either the USB port (e.g. `/dev/usb/lp0`) in case of a local printer or the IP address, prefixed by `net:` (e.g. `net:192.168.1.100`), in case of a network printer:

```
# ccpdadmin -p *queue_name* -o *printer_address*

```

For example, for a USB printer:

```
# ccpdadmin -p LBP6310 -o /dev/usb/lp0

```

Or for a network printer:

```
# ccpdadmin -p LBP6310 -o net:192.168.1.100

```

[Start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") the CAPT daemon with `ccpd.service`.

To remove a printer:

```
# ccpdadmin -x *queue_name*

```

## CAPT status monitor

### Local CUPS

The driver includes a status monitor which can be launched with

```
$ captstatusui -P *printer_model*

```

e.g.

```
$ captstatusui -P LBP6310

```

If you only want the status monitor to pop up when a problem occurs, simply append the `-e` switch:

```
$ captstatusui -P LBP6310 -e

```

### Remote CUPS

Unfortunately, a local installation of *captstatusui* will not detect CAPT printers on a remote CUPS server.

Remote print monitoring can be achieved, however, using [SSH](/index.php/SSH "SSH") and [X11 forwarding](/index.php/X11_forwarding "X11 forwarding").

**Warning:** X11 forwarding has important security implications, especially when using the `-Y` switch (*ForwardX11Trusted*, required for the CAPT status monitor to work via X11 Forwarding). See [X11 forwarding](/index.php/X11_forwarding "X11 forwarding") for further information.

**Note:** There are many ways to set up X11 forwarding. For security reasons, this example is based on public key authentication, a dedicated SSH user account, and SSH running on the CUPS server. Adapt these instructions to your specific configuration.

#### Client configuration

*   create a new [SSH key](/index.php/SSH_key "SSH key") `~/.ssh/capt` and [copy the public key to the remote server](/index.php/SSH_keys#Copying_the_public_key_to_the_remote_server "SSH keys")
*   create a file `captstatusui.sh` with the following content, make it executable and place it in your [autostart](/index.php/Autostart "Autostart") folder:

```
#!/bin/sh
ssh -T -Y -i ~/.ssh/capt *remote_server_hostname_or_IP_address* < /dev/null

```

#### Server configuration

*   create a new user `capt`
*   append the following section to `/etc/ssh/sshd_config` and [restart](/index.php/Restart "Restart") the SSH daemon or socket

```
...
Match User capt
       X11Forwarding yes
       PermitTTY no
       ForceCommand captstatusui -P *printer_model* -e
       AuthenticationMethods publickey

```

e.g.

```
...
Match User capt
       X11Forwarding yes
       PermitTTY no
       ForceCommand captstatusui -P LBP6310 -e
       AuthenticationMethods publickey

```

This can be extended to include multiple users (using a single, shared SSH key or each with a unique SSH key) by adding each user to a `capt` group, then using a Match Group rule:

```
...
Match Group capt
       X11Forwarding yes
       PermitTTY no
       ForceCommand captstatusui -P LBP6310 -e
       AuthenticationMethods publickey

```