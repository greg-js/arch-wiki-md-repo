[Freenet](http://freenetproject.org/) is a free and open source software that aims to provide anonymity and freedom of speech through a decentralized peer-to-peer network. Freenet enables its users to share files anonymously, publish freesites without fear of censorship and more. Data is encrypted and routed through multiple nodes making almost impossible to identify who requested the information and what its content is. Keep in mind any files you choose to upload may contain meta data.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Wizard](#Wizard)
    *   [2.2 Manual](#Manual)

## Installation

[Install](/index.php/Install "Install") the [freenet](https://aur.archlinux.org/packages/freenet/) package.

## Configuration

[Start/enable](/index.php/Start/enable "Start/enable") the `freenet.service`.

You can either let the wizard guide you through the configuration or get your hands dirty by configuring freenet manually. You might want to read about [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") or [EncFS](/index.php/EncFS "EncFS") to protect the data you will be sharing before continuing.

### Wizard

You need to visit freenet's web interface at [http://127.0.0.1:8888/](http://127.0.0.1:8888/) and make sure you carefully follow the instructions. Using the private mode of your browser while accessing freenet is a good habit to take.

### Manual

The [Freenet wiki](https://github.com/freenet/wiki/wiki) will be useful if you decide to configure things by hand. Manual configuration is done by editing `/opt/freenet/freenet.ini` and `/opt/freenet/wrapper.conf`.