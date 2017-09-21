*EVE Online* is a space-based, persistent world [massively multiplayer online role-playing game](https://en.wikipedia.org/wiki/Massively_multiplayer_online_role-playing_game "wikipedia:Massively multiplayer online role-playing game") (MMORPG) that is renound for its scale and complexity. It features free-to-play and pay-to-play versions--the pay-to-play version unlocking additional ships, skills, and training bonuses. Both versions access the same characters and assets belonging to the player.

There is no Linux client program for EVE Online. The game is installed with the *EVE Launcher Setup* (a Windows program) run under [Wine](/index.php/Wine "Wine"), the *win*dows *e*mulator. The *EVE Launcher*, once installed (also a Windows program, under Wine), authenticates the player then starts the game proper. An internet connection to the EVE Online servers is maintained throughout play. The purpose of Wine is to translate the Windows API calls made by the install and game programs into compatible Linux API calls, on-the-fly as the programs run.

## Contents

*   [1 Requirements](#Requirements)
    *   [1.1 Installing](#Installing)
    *   [1.2 Playing](#Playing)
*   [2 Installation](#Installation)
    *   [2.1 Install packages](#Install_packages)
    *   [2.2 Prepare the Wine configuration](#Prepare_the_Wine_configuration)
        *   [2.2.1 Set environment variables](#Set_environment_variables)
        *   [2.2.2 Create the minimal configuration](#Create_the_minimal_configuration)
        *   [2.2.3 Add supplementary components](#Add_supplementary_components)
    *   [2.3 Install EVE Online](#Install_EVE_Online)
*   [3 Play the game](#Play_the_game)
*   [4 Tips and tricks](#Tips_and_tricks)
*   [5 Known issues](#Known_issues)
    *   [5.1 Game freezes during play](#Game_freezes_during_play)
        *   [5.1.1 Symptoms](#Symptoms)
        *   [5.1.2 Resolution](#Resolution)
    *   [5.2 Firejail incompatibility](#Firejail_incompatibility)
        *   [5.2.1 Symptoms](#Symptoms_2)
        *   [5.2.2 Resolution](#Resolution_2)
*   [6 See also](#See_also)

## Requirements

### Installing

*   Internet connectivity
*   Familiarity with [Wine](/index.php/Wine "Wine")
*   A [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   The 32-bit version of your graphics driver, as listed in the *OpenGL (Multilib)* column in [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg").

### Playing

*   Internet connectivity
*   Patience; be prepared for a steep learning curve if you are a new pilot.

## Installation

### Install packages

1.  [Install](/index.php/Install "Install") the [wine-staging](https://www.archlinux.org/packages/?name=wine-staging), [winetricks](https://www.archlinux.org/packages/?name=winetricks), and [samba](https://www.archlinux.org/packages/?name=samba) packages.
2.  [Install](/index.php/Install "Install") the [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins), [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls), [lib32-gst-plugins-base-libs](https://www.archlinux.org/packages/?name=lib32-gst-plugins-base-libs), [lib32-libldap](https://www.archlinux.org/packages/?name=lib32-libldap), [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse), [lib32-libva](https://www.archlinux.org/packages/?name=lib32-libva), [lib32-libxml2](https://www.archlinux.org/packages/?name=lib32-libxml2), [lib32-mpg123](https://www.archlinux.org/packages/?name=lib32-mpg123), [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal), and [lib32-v4l-utils](https://www.archlinux.org/packages/?name=lib32-v4l-utils) packages from the official [multilib](/index.php/Multilib "Multilib") repository.

**Note:** You do *not* need to [start](/index.php/Start "Start") or [enable](/index.php/Enable "Enable") the `samba.service` file installed from the [samba](https://www.archlinux.org/packages/?name=samba) package; no further configuration of [Samba](/index.php/Samba "Samba") is required. Wine requires the `/usr/bin/ntlm_auth` program which is provided by the [samba](https://www.archlinux.org/packages/?name=samba) package.

### Prepare the Wine configuration

In this section, you will prepare a fresh *Wine configuration* suitable for installing the EVE Launcher *into* (as described in the next section).

	Wine configuration

	Background: An arbitrary Windows program running under Wine needs routine access to a minimum of files, such as Windows support programs, native and emulated .dll's, registry entries, and so forth. On the first invocation of Wine, these files are copied into a "working" directory (typically at `~/.wine`) in an arrangement that mimics a native Windows filesystem. An *application* such as the EVE Launcher is then installed into this minimal Windows filesystem by its setup program also run under Wine. At this point Wine can run the EVE Launcher in its proper filesystem context. Together, all this data comprises a single *Wine configuration*, particular to zero, one, (or more) Windows applications installed and runnable therein.

#### Set environment variables

**If you have no other Wine configurations** (i.e. this is a clean install), the environment variables `WINEPREFIX` and `WINEARCH` will not be defined--their defaults being `~/.wine` and `win64` respectively, and you can **skip to step 4**. Otherwise **read on**.

1.  Select a location in your filesystem to store the Wine configuration: a location that you have access to, is persistant, and doesn't contain any files. It should be a directory, but it doesn't have to exist yet--Wine will create it if it doesn't exist. Note the *path* of this location.

**Warning:** It would be unwise to select an *existing* Wine configuration and attempt to install the EVE Launcher into it unless you know what you're doing; better to start with a "clean slate".

	2\. Set the [WINEPREFIX](/index.php/Wine#WINEPREFIX "Wine") environment variable to the *path* you noted in the previous step.

	 `export WINEPREFIX=*path*` 

	The value of `WINEPREFIX` is the path to the configuration that Wine will use at runtime. If `WINEPREFIX` is not defined `~/.wine` will be used by default. A generic Wine configuration will be generated automatically at this path if it is empty, or updated if it contains files.

**Tip:** If you periodically redefine `WINEPREFIX` to run other Wine configurations, you would be wise to verify that `WINEPREFIX` is correctly set to the EVE Online Wine configuration path prior to starting the game.

**If you have no win32 Wine configurations** the environment variable `WINEARCH` will not be defined, the default being `win64`, and you can **skip to step 4**. Otherwise **read on**.

	3\. Ensure the [WINEARCH](/index.php/Wine#WINEARCH "Wine") environment variable is not defined (or is set to `win64`).

**Note:** EVE Online requires a 64-bit Wine configuration.

**Tip:** If you periodically set `WINEARCH=win32` to run Windows programs in 32-bit Wine configurations you would be wise to verify that `WINEARCH` is correctly set to `win64` (or undefined) prior to starting the game.

#### Create the minimal configuration

	4\. Generate the minimal Wine configuration.

	 `$ winecfg` 

	Generation will take place followed by the appearance of the `Wine configuration` window.

**Tip:** Wine writes *alot* of diagnostic messages to `stdout` which you can safely ignore unless you experience problems.

**Tip:** If you have [Firejail](/index.php/Firejail "Firejail") installed and the `Wine configuration` window does not appear, see [EVE Online#Firejail](/index.php/EVE_Online#Firejail "EVE Online") for a resolution.

	5\. On the `Applications` tab, click the `Windows Version` drop-down box and select `Windows 10`.

	6\. Click `OK` to accept changes and close the window.

	`winecfg` will exit.

#### Add supplementary components

	7\. Download and install the suplementary runtime components needed by EVE Online into the configuration using `winetricks`.

	 `$ winetricks corefonts vcrun2005 vcrun2008 vcrun2010` 

	The components will be downloaded and you will see a series of dialogs asking you to confirm each installation.

	8\. Confirm each.

	The components will be installed into the Wine configuration, then `winetricks` will exit.

### Install EVE Online

Download the [EVE Launcher Setup program](https://community.eveonline.com/support/download/).

**Note:** The setup program's filename will in the format `EveLauncher-*nnnnnnnn*.exe`, where *nnnnnnnnn* is the release number.

Run the EVE Launcher setup under Wine.

```
$ wine EveLauncher-*nnnnnnnnn*.exe

```

You will be presented with a series of dialogs where you can customize the installation of EVE Online. Accept the defaults or customize. Click `Finish` and the EVE Launcher setup will exit.

## Play the game

Ensure that `WINEPREFIX` and `WINEARCH` are not defined, or defined appropriately.

Start the EVE Launcher:

```
$ wine start 'C:\EVE\eve.exe'

```

Login with your EVE username and password, or create an account. Accounts are [free as in beer](https://en.wiktionary.org/wiki/free_as_in_beer "wiktionary:free as in beer").

**Note:** Everytime you start the EVE Launcher, it will verify that your EVE game software is up-to-date. If it needs updating, it will download and install file "bundles" automatically with no action necessary on your part. Game updates happen frequently (several times a week on average).

**Note:** The *first time* you start the EVE Launcher, it will download and install a large number of "bundles" taking 1-5 minutes depending on your network bandwidth.

## Tips and tricks

*   If you experience "stuttering" in the graphics during scenes with many redrawings, try lowering the rendering quality to better suit your hardware and drivers. Pressing `Esc` at any time during the game will display a panel where you can adjust these settings.

## Known issues

### Game freezes during play

#### Symptoms

*   Multi-second game "freezes" on a multi-core processor.

#### Resolution

When starting the EVE Launcher, prefix the `wine` command as in the following:

 `$ taskset -c0 wine 'C:\EVE\eve.exe'` 

This will force the EVE process to stay on one processor core only, preventing slow migration from core to core.

**Warning:** This will decrease game performance and is not recommended unless you are experiencing freezes.

### Firejail incompatibility

As of September 2017, the default [Firejail](/index.php/Firejail "Firejail") *profile* for Wine is incompatible with EVE Online. If you install [firejail](https://www.archlinux.org/packages/?name=firejail) subsequent to installing [wine-staging](https://www.archlinux.org/packages/?name=wine-staging), the Firejail configuration process may create a symlink `/usr/local/bin/wine -> /usr/bin/firejail` that automatically "sandboxes" Wine with this profile. From this point forward, EVE Online will no longer run.

#### Symptoms

*   `winecfg`, `winetricks`, and `wine` produce messages to `stdout` then halt, with no game or configuration windows appearing.

#### Resolution

1.  Delete or rename the `/usr/local/bin/wine` symlink so `$ wine` correctly runs `/usr/bin/wine`, bypassing Firejail entirely.

## See also

*   [Official site](http://www.eveonline.com)
*   [EVE Online](https://en.wikipedia.org/wiki/EVE_Online "wikipedia:EVE Online") at Wikipedia