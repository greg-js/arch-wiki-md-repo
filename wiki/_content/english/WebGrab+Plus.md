[WebGrab+Plus](http://www.webgrabplus.com/) is a multi-site incremental [XMLTV](https://en.wikipedia.org/wiki/XMLTV "wikipedia:XMLTV") [EPG](https://en.wikipedia.org/wiki/EPG "wikipedia:EPG") grabber. It collects TV program guide data from selected TV guide sites for your favorite channels. It can later be used by [Kodi](/index.php/Kodi "Kodi") and other popular players.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Finding and adding channels](#Finding_and_adding_channels)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Different channel names](#Different_channel_names)
    *   [4.2 Same channels under different names](#Same_channels_under_different_names)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Alternative configuration directory](#Alternative_configuration_directory)
    *   [5.2 Update channels list](#Update_channels_list)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [wg++](https://aur.archlinux.org/packages/wg%2B%2B/) package.

## Usage

Copy the default configuration directory:

```
$ cp -R /usr/share/wg++ ~/wg++

```

To generate EPG guide, run:

```
$ wg++

```

And your EPG guide will be stored in the location, which is defined in configuration file `~/wg++/WebGrab++.config.xml`.

## Configuration

All configuration files will be placed in `~/wg++` directory. The main configuration file is `~/wg++/WebGrab++.config.xml`. See [the upstream documentation](http://www.webgrabplus.com/documentation/configuration/webgrabconfigxml) for the available options.

**Tip:** You might want to set up [web server](/index.php/Web_server "Web server") on the same machine, set up read-write access for your user and generate `guide.xml` directly to it. For example `<filename>/srv/http/public/guide.xml</filename>`.

#### Finding and adding channels

Channel entries defines what TV programs needs to be included in EPG guide.

To list all possible TV programs, use this command:

```
$ grep site_id ~/wg++/siteini.pack/*/*channels.xml

```

To list all possible TV programs by country:

```
$ grep site_id ~/wg++/siteini.pack/*Country*/*channels.xml

```

To filter TV programs by keyword:

```
$ grep site_id ~/wg++/siteini.pack/*/*channels.xml | grep -i "*keyword*"

```

And paste as many <channel> entries as you want into the configuration file.

## Troubleshooting

### Different channel names

Your IPTV provider might use different channel names from what WebGrabber+Plus offers. For example - **TV3** channel exists in WebGrabber+Plus channels list, but your IPTV provider uses **TV3 4K**, which refers to the same channel, but cannot be found in WebGrabber+Plus channels list. If the channel name is not changed, then it will not be picked up by IPTV player either.

To resolve this, take the actual WebGrabber+Plus channel element:

```
<channel update="i" site="tvprograma.lt" site_id="tv3/42" xmltv_id="TV3">**TV3**</channel>

```

and change value accordingly:

```
<channel update="i" site="tvprograma.lt" site_id="tv3/42" xmltv_id="TV3">**TV3 4K**</channel>

```

### Same channels under different names

Your IPTV provider might provide backup channels or channels with different quality, therefore ending up with duplicating channels under different names. In order to generate EPG guide efficiently, modify configuration file as per below example:

```
<channel update="i" site="sporttv.pt" site_id="727" xmltv_id="**SPORT.TV1**">SPORT TV 1</channel>
<channel offset="0" same_as="**SPORT.TV1**" xmltv_id="SPORT TV 1 HD">SPORT TV 1 HD</channel>
<channel offset="0" same_as="**SPORT.TV1**" xmltv_id="SPORT TV 1 FHD">SPORT TV 1 FHD</channel>
<channel offset="0" same_as="**SPORT.TV1**" xmltv_id="SPORT TV 1 XXX">SPORT TV 1 XXX</channel>

```

**Note:** Attribute `xmltv_id` must be unique in your configuration file. You might consider changing it to new channel's name as well.

## Tips and tricks

### Alternative configuration directory

You can specify and use alternative configuration directory. Copy default configuration directory to your desired destination:

```
$ cp -R /usr/share/wg++ /path/to/*<configuration_directory>*

```

To generate EPG guide, run:

```
$ wg++ /path/to/*<configuration_directory>*

```

### Update channels list

[wg++](https://aur.archlinux.org/packages/wg%2B%2B/) already contains channels lists, but they might not be up to date. To update them, you have 2 choices:

*   Download latest upstream channels (sites) lists from [GitHub repository](https://github.com/SilentButeo2/webgrabplus-siteinipack).
*   Update yourself for specific TV guide providers. See [Site.channels.xml | WebGrab+Plus](http://webgrabplus.com/documentation/configuration/sitechannelsxml)

## See also

*   [WebGrab+Plus official documentation](http://www.webgrabplus.com/documentation)