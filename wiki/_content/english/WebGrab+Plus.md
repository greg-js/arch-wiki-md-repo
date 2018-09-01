[WebGrab+Plus](http://www.webgrabplus.com/) is a multi-site incremental [XMLTV](https://en.wikipedia.org/wiki/XMLTV "wikipedia:XMLTV") [EPG](https://en.wikipedia.org/wiki/EPG "wikipedia:EPG") grabber. It collects TV program guide data from selected TV guide sites for your favorite channels. It can later be used by [Kodi](/index.php/Kodi "Kodi") and other popular players.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Finding and adding channels](#Finding_and_adding_channels)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Different channel names](#Different_channel_names)
*   [5 See also](#See_also)

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
<channel update="i" site="tvprograma.lt" site_id="tv3/42" xmltv_id="**TV3**">**TV3**</channel>

```

and change attribute `xmltv_id` and value accordingly:

```
<channel update="i" site="tvprograma.lt" site_id="tv3/42" xmltv_id="**TV3 4K**">**TV3 4K**</channel>

```

## See also

*   [WebGrab+Plus official documentation](http://www.webgrabplus.com/documentation)