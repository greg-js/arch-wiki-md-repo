This article is intended to show users how to install Arch remotely via an [SSH](/index.php/SSH "SSH") connection. Consider this approach when the host is located remotely or you wish to use the copy/paste ability of an SSH client to do the Arch install.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 On the remote (target) machine](#On_the_remote_(target)_machine)
*   [2 On the local machine](#On_the_local_machine)
*   [3 Install Arch Linux on a Headless Server (SSH over WiFi)](#Install_Arch_Linux_on_a_Headless_Server_(SSH_over_WiFi))

## On the remote (target) machine

**Note:** These steps require physical access to the machine. If the host is physically located elsewhere, this may need to be coordinated with another person.

Boot the target machine into a live Arch environment via the [Live CD/USB image](/index.php/Getting_and_installing_Arch "Getting and installing Arch"): this will log the user in as root.

At this point, setup the network on the target machine as for example suggested in [Installation guide#Connect to the internet](/index.php/Installation_guide#Connect_to_the_internet "Installation guide").

Secondly, setup a root password which is needed for an SSH connection, since the default Arch password for root is empty:

```
# passwd

```

Now check that `PermitRootLogin yes` is present (and uncommented) in `/etc/ssh/sshd_config`. This setting allows root login with password authentication on the SSH server.

Finally, [start](/index.php/Start "Start") the openssh daemon with `sshd.service`, which is included by default on the live CD.

**Note:** Unless required, after installation it is recommended to remove `PermitRootLogin yes` from `/etc/ssh/sshd_config`.

**Tip:** If the target machine is behind a NAT router, and you require external access, the SSH port (22 by default) will need to be forwarded to the target machine's LAN IP address.

## On the local machine

On the local machine, connect to the target machine via SSH with the following command:

```
$ ssh root@*ip.address.of.target*

```

From here one is presented with the live environment's welcome message and is able to administer the target machine as if sitting at the physical keyboard. At this point, if the intent is to simply install Arch from the live media, follow the guide at [Installation guide](/index.php/Installation_guide "Installation guide"). If the intent is to edit an existing Linux install that got broken, follow the [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux") wiki article.

**Tip:** Consider installing a [terminal multiplexer](/index.php/List_of_applications#Terminal_multiplexers "List of applications") on the target machine's live (in memory) system, so that if you are disconnected you can reattach to your multiplexer's session.

## Install Arch Linux on a Headless Server (SSH over WiFi)

**Note:** These steps require physical access to the USB port of the headless machine. Somebody has to insert the bootable USB stick and power up the headless server.

This section describes installation of Arch Linux on a headless server (in my case an Intel NUC box) without a keyboard, mouse or display. It involves three steps:

1.  Create a modified Arch Linux live image using [Archiso](/index.php/Archiso "Archiso"). The modification is designed to do three things:
    1.  Automatically connect to the (possibly password protected) WiFi network at boot time.
    2.  Run the SSH daemon at boot time
    3.  Create an `/root/.ssh/authorized_keys` file for root containing your public key. The default `/etc/ssh/sshd_config` allows root to log in over SSH using public key authentication.
2.  Boot the headless machine into a live Arch environment by inserting the installation medium containing the above modified boot image and powering it up.
3.  Wait for a minute or so to allow the headless machine time to boot up and connect to the WiFi network. From your existing machine (with keyboard and display) SSH into the live Arch environment on the headless server and complete the installation as described in the [Installation guide](/index.php/Installation_guide "Installation guide").

**Note:** To belabor the obvious, all the WiFi and SSH configuration that was carried out in the boot image needs to be done again in the actual Arch Linux installation to allow WiFi SSH access to the headless machine after installation.

The rest of this section describes the first step of creating a modified live image. All of this done on a machine with an existing Arch Linux installation which will typically also be the machine from which you plan to SSH into the headless machine.

*   Install [Archiso](/index.php/Archiso "Archiso") and then as explained in [Archiso#Setup](/index.php/Archiso#Setup "Archiso") copy the *releng* profile to a suitable folder:

```
cp -r /usr/share/archiso/configs/releng/ /root/archlive

```

*   Create a file defining your network SSID, password and public key file. This can be merged into the script file described below, but I prefer to keep some separation between code and data.

 `/root/archlive/my-build-config.sh` 
```
SSID=your_wifi_network_ssid
PASSWORD=your_wifi_network_password
PUBLIC_KEY=/path/to/your/public/key
```

*   Create a customized build script that installs requisite packages, enables desired services and copies the public key file to the boot image. This script does several modifications in the boot image:
    *   It copies the public key into root's `.ssh/authorized_keys`. As explained in [Archiso#Adding_files_to_image](/index.php/Archiso#Adding_files_to_image "Archiso"), this has to be done by creating a `skel` directory within `airootfs/` and copy the files there. SSH is very particular about file permissions and we must set these permissions as well.
    *   It sets up the boot image to connect to the WiFi network at boot using [NetworkManager](/index.php/NetworkManager "NetworkManager") and its command line interface [nmcli](/index.php/NetworkManager#nmcli_examples "NetworkManager"). There are several steps involved in this:
        *   Install [networkmanager](/index.php/Networkmanager "Networkmanager") as well as the [Wireless drivers and firmware](/index.php/Wireless#Troubleshooting_drivers_and_firmware "Wireless") which in my case is [[linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware)]. As explained in [Archiso#Installing_packages](/index.php/Archiso#Installing_packages "Archiso"), installation of additional packages is accomplished by adding these packages to the lists of packages in `packages.x86_64`.
        *   Start the `NetworkManager.service` at boot by adding the requisite `systemctl enable` command to `customize_airootfs.sh` as explained in [Archiso#Configure_the_live_medium](/index.php/Archiso#Configure_the_live_medium "Archiso")
        *   Ensure that the requisite `nmcli dev wifi connect` command is executed automatically on booting. The boot image is by default set up to auto login to root at boot. When root (or any other user logs in), the scripts in `/etc/profile.d` are executed. So all that we need to do is to create an executable script in `/etc/profile.d` with the requisite `nmcli dev wifi connect` command. In the script below, the password is enclosed in an arcane set of quotes; this quoting is necessary only if the password is actually a passphrase (with embedded spaces).
    *   Start the `sshd.service` at boot by adding the requisite `systemctl enable` command to `customize_airootfs.sh` as explained in [Archiso#Configure_the_live_medium](/index.php/Archiso#Configure_the_live_medium "Archiso")
    *   Finally, the customized build script must run the original build script (`./build.sh`) to create the boot image.

 `/root/archlive/my-build.sh` 
```
# source values of SSID PASSWORD PUBLIC_KEY
source my-build-config.sh

# copy PUBLIC_KEY to authorized_keys 
mkdir -p airootfs/etc/skel/.ssh
cp $PUBLIC_KEY airootfs/etc/skel/.ssh/authorized_keys
chmod 700 airootfs/etc/skel/.ssh
chmod 600 airootfs/etc/skel/.ssh/authorized_keys

# install networkmanager
echo networkmanager >> packages.x86_64
# install linux-firmware (required for the Intel NUC)
echo linux-firmware >> packages.x86_64

# enable sshd and NetworkManager
echo systemctl enable sshd.service NetworkManager.service \
     >> airootfs/root/customize_airootfs.sh
# connect to WiFi network at login
mkdir -p airootfs/etc/profile.d
echo nmcli dev wifi connect "$SSID" password '"'"$PASSWORD"'"' \
     >> airootfs/etc/profile.d/connect-wifi.sh
chmod +x airootfs/etc/profile.d/connect-wifi.sh

# run the original build script
./build.sh
```

Make the script executable and run it

```
cd /root/archlive
chmod +x my-build.sh
./my-build.sh

```

The modified boot image is now ready (in the `/root/archlive/out/` folder) and can be copied to an installation medium (USB drive) using `dd`:

 `dd bs=4M if=out/archlinux_xxxxxx of=/dev/sdxx status=progress oflag=sync`