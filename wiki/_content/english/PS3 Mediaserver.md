[PS3 Media Server](https://github.com/ps3mediaserver/ps3mediaserver) is a cross-platform DLNA-compliant UPnP Media Server, written in [Java](/index.php/Java "Java").

**Warning:** The project is unmaintained since 2016.

Has very good default transcoding profiles for several clients, but lacks good information for headless servers.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Running](#Running)
*   [4 Indexing](#Indexing)

## Installation

**Note:** Because of the dependency [tsmuxer](https://aur.archlinux.org/packages/tsmuxer/) having extra 32-bit dependencies, you will need to enable the [multilib](/index.php/Multilib "Multilib") repository if you have a 64-bit system.

[Install](/index.php/Install "Install") the [pms](https://aur.archlinux.org/packages/pms/) package.

## Configuration

The default install location is `/opt/pms` and the config file is at `/opt/pms/PMS.conf`, there are comments describing what each option is for.

If running headless on a server

 `Operating Mode`  `minimized = true` 

If you do not want your entire filesystem to be shown

 `Media Locations` 
```
folders = /directory.you.want.shared/,/another.directory

```

If you run into issues with the wrong audio track playing (example: English desired)

 `Audio language priority` 
```
mencoder_audiolangs = eng,und

```

Example of english subtitles desired, no subtitles by default on English programs

 `Subtitle language priority` 
```
mencoder_sublangs = loc,eng,und

```

A list with all options can be found [here](http://ps3mediaserver.org/forum/viewtopic.php?f=3&t=254&hilit=pms.conf#p15283).

## Running

[Start](/index.php/Start "Start") `pms@**user**.service`, replacing `**user**` with the user you want PMS to run under.

## Indexing

This should be done automagically upon starting the service, but if it does not, this is how to do it manually:

*   Browse the logs to see at what ip-address and port pms has started the built-in webservice
*   Use your web browser to go to: http://<ip-address-of-your-server>:5001/console/home and click on 'index files and folders'
*   After the indexing has ended, you are done.