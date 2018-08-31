[WebGrab+Plus](http://www.webgrabplus.com/) is a multi-site incremental XMLTV EPG grabber. It collects TV program guide data from selected TV guide sites for your favorite channels. It can later be used by [Kodi](/index.php/Kodi "Kodi") and other popular players.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Generate configuration](#Generate_configuration)
    *   [2.2 Customize configuration](#Customize_configuration)
        *   [2.2.1 <filename>](#.3Cfilename.3E)
        *   [2.2.2 <mode>](#.3Cmode.3E)
        *   [2.2.3 <channel>](#.3Cchannel.3E)
    *   [2.3 Generate EPG](#Generate_EPG)
        *   [2.3.1 One time](#One_time)
        *   [2.3.2 Scheduled](#Scheduled)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Different channel names](#Different_channel_names)
*   [4 See also](#See_also)

## Installation

Install as a [wg++](https://aur.archlinux.org/packages/wg%2B%2B/) package.

## Configuration

The default configuration file looks like this:

 `~/wg++/WebGrab++.config.xml` 
```
<?xml version="1.0"?>
<settings>

  <filename>guide.xml</filename>
  <mode></mode>
  <postprocess grab="y" run="n">mdb</postprocess>
  <user-agent>Mozilla/5.0 (Windows NT 6.1; WOW64; rv:29.0) Gecko/20100101 Firefox/29.0</user-agent>
  <logging>on</logging>
  <retry time-out="5">4</retry>
  <timespan>0</timespan>
  <update>f</update>

  <channel site="dummy" site_id="xx" update="i" xmltv_id="Example">Example</channel>

</settings>

```

### Generate configuration

Run `wg++` as regular user once:

```
$ wg++

```

and directory `~/wg++` will be created. Alternatively, you can copy all configuration files manually:

```
$ mkdir ~/wg++
$ cp -R /usr/share/wg++ ~/wg++

```

**Note:** Because of application design, it is impossible to create any [Systemd](/index.php/Systemd "Systemd") service or timer. You will need to rely on configuration files stored in your home directory, where your user can read, write and permanently store files.

### Customize configuration

All configuration files will be placed in `~/wg++` directory. The main configuration file is `~/wg++/WebGrab++.config.xml`.

#### <filename>

Filename is generated EPG guide's full path. The location must have read-write permissions for your user. For example:

```
<filename>/home/jan/wg++/guide.xml</filename>

```

**Tip:** You might want to set up [web server](/index.php/Web_server "Web server") on the same machine, set up read-write access for your user and generate `guide.xml` directly to it. for example `<filename>/srv/http/public/guide.xml</filename>`.

#### <mode>

Mode defines how EPG guide will be generated.

| Short | Long | Description |
| d | debug | Saves the output XMLTV file in a file with -debug addition in the file name. The original XMLTV file will be kept. |
| m | measure | Measures the time for each updated show or new show added. |
| n | nomark | Disables the update-type marking (n) (c) (g) (r) at the end of the description. |
| v | verify | Verifies the result following a channel update. |
| w | wget | Use wget as grab engine (might improve site recognition in rare cases). |

Both short and long can be mixed, separated by comma's and/or spaces. For example:

```
<mode>d,nomark verify</mode>

```

#### <channel>

Channel entries defines what TV programs needs to be included in EPG guide.

To list all possible TV programs, use this command:

```
$ cat ~/wg++/siteini.pack/*/*channels.xml | grep "site_id"

```

To list all possible TV programs by country:

```
$ cat ~/wg++/siteini.pack/*Country*/*channels.xml | grep "site_id"

```

To filter TV programs by keyword:

```
$ cat ~/wg++/siteini.pack/*/*channels.xml | grep "site_id" | grep -i "*keyword*"

```

And paste as many <channel> entries as you want into the configuration file. Example:

 `~/wg++/WebGrab++.config.xml` 
```

  ...

  <channel update="i" site="toptv.co.za" site_id="euro-sport-news" xmltv_id="Euro Sport News">Euro Sport News</channel>
  <channel update="i" site="toptv.co.za" site_id="discovery-science" xmltv_id="Discovery Science">Discovery Science</channel>
  <channel update="i" site="tvprograma.lt" site_id="lietuvos-ryto-tv/34" xmltv_id="Lietuvos ryto TV">Lietuvos ryto TV</channel>

  ...

```

### Generate EPG

#### One time

To generate EPG guide, run:

```
$ wg++

```

And your EPG guide will be stored in the location, which is defined in configuration file `~/wg++/WebGrab++.config.xml`.

#### Scheduled

In order to create a scheduled job (e.g. every day or every week), you might want to set up [Cron job](/index.php/Cron "Cron") for this type of task. For example, run `wg++` command every night at 3AM:

 `$ crontab -e` 
```
0 3 * * * wg++

```

## Troubleshooting

### Different channel names

Your IPTV provider might use different channel names from what WebGrabber+Plus offers. For example - **TV3** channel exists in WebGrabber+Plus channels list, but your IPTV provider uses **TV3 4K**, which refers to the same channel, but cannot be found in WebGrabber+Plus channels list.

To resolve this, take the actual WebGrabber+Plus channel element:

```
<channel update="i" site="tvprograma.lt" site_id="tv3/42" xmltv_id="**TV3**">**TV3**</channel>

```

and change attribute `xmltv_id` and value accordingly:

```
<channel update="i" site="tvprograma.lt" site_id="tv3/42" xmltv_id="**TV3 4K**">**TV3 4K**</channel>

```

## See also

*   [WebGrab+Plus official documentation](http://www.webgrabplus.com/documentation%7COfficial)