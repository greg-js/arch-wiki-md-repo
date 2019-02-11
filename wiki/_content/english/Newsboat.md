[Newsboat](https://newsboat.org/) is an open source news aggregator licensed under the MIT License.

From the [documentation](https://newsboat.org/releases/2.12/docs/newsboat.html#_introduction):

	Newsboat is an RSS/Atom feedreader. RSS and Atom are a number of widely-used XML formats to transmit, publish and syndicate articles, for example news or blog articles. Newsboat is designed to be used on text terminals on Unix or Unix-like systems such as GNU/Linux, FreeBSD or macOS.

Newsboat is a [fork](https://groups.google.com/forum/#!topic/newsbeuter/RPtlWX8CPGU) of Newsbeuter. The only difference is that Newsboat is actively maintained while Newsbeuter isn't.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Managing feeds](#Managing_feeds)
    *   [3.1 Adding/Removing feeds](#Adding/Removing_feeds)
    *   [3.2 Tagging feeds](#Tagging_feeds)
        *   [3.2.1 Special tags](#Special_tags)
            *   [3.2.1.1 Custom feed names](#Custom_feed_names)
            *   [3.2.1.2 Hidden feeds](#Hidden_feeds)
*   [4 Configuration](#Configuration)
*   [5 Tips](#Tips)
    *   [5.1 Automatic feed reloads](#Automatic_feed_reloads)
    *   [5.2 Pass article URL to external command](#Pass_article_URL_to_external_command)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Newsboat won't start](#Newsboat_won't_start)
*   [7 See Also](#See_Also)

## Installation

Install the [newsboat](https://www.archlinux.org/packages/?name=newsboat) package. For the development version, install the [newsboat-git](https://aur.archlinux.org/packages/newsboat-git/) package.

## Usage

Newsboat can't start without any configured feeds. Feeds can be configured in `~/.config/newsboat/urls`.

Newsboat can be started from the command line with

```
newsboat

```

Press the `?` key to see a list of all keybindings. Keybindings can be rebound, see [#Configuration](#Configuration).

## Managing feeds

Adding, removing, and tagging feeds is done by editing the urls file. By default that is `~/.config/newsboat/urls`.

### Adding/Removing feeds

To add URLs, open `~/.config/newsboat/urls` with your favorite text editor and add the URLs, one per line:

```
http://rss.cnn.com/rss/cnn_topstories.rss
http://newsrss.bbc.co.uk/rss/newsonline_world_edition/front_page/rss.xml

```

If you need to add URLs that have restricted access via username/password, simply provide the username/password in the following way:

```
http://username:password@hostname.domain.tld/feed.rss

```

In order to protect username and password, make sure that `~/.config/newsboat/urls` has the appropriate permissions.

Newsboat also makes sure that usernames and passwords within URLs aren’t displayed in its user interface. In case there is a @ in the username, you need to write it as %40 instead so that it can be distinguished from the @ that separates the username/password part from the hostname part.

You can also configure local files as feeds, by prefixing the local path with `file://` and adding it to the `~/.config/newsboat/urls` file:

```
file:///var/log/rss_eventlog.xml

```

To **remove** a feed, simply delete the line from your urls file

### Tagging feeds

Every feed can be assigned 0 or more tags. This makes it easy to categorize your feeds as well as the ability to easily apply commands to multiple feeds at once.

Usually, the `~/.config/newsboat/urls` file contains one RSS feed URL per line. To assign a tag to an RSS feed, simply attach it as a single word, separated by blanks such as space or tab. If the tag needs to contain spaces, you must use quotes (") around the tag (see example below). An example may look like this:

```
http://blog.fefe.de/rss.xml?html interesting conspiracy news "cool stuff"                                       
http://rss.orf.at/news.xml news orf                                                                             
http://www.heise.de/newsticker/heise.rdf news interesting                                                       

```

When you now start Newsboat with this configuration, you can press `t` to select a tag. When you select the tag "news", you will see all three RSS feeds. Pressing `t` again and e.g. selecting the "conspiracy" tag, you will only see the `http://blog.fefe.de/rss.xml?html` RSS feed. Pressing `Ctrl-T` clears the current tag, and again shows all RSS feeds, regardless of their assigned tags.

**Note:** If the tag name contains spaces, the tag must be bounded by `"`

#### Special tags

##### Custom feed names

The name of a feed can be defined with a special tag in your urls file. Simply **prefix** the tag name with the `~` character and the tag name will become the feed name.

For example:

```
http://rss.cnn.com/rss/cnn_topstories.rss "~CNN Top stories"

```

will define the feed with feed-name "CNN Top stories"

##### Hidden feeds

A feed can be **hidden** from the regular list of feeds by **prefixing** the tag name with an `!`.

For example:

```
http://rss.orf.at/news.xml "!ORF News (hidden)"                                                                 

```

The content of a **hidden** feed can only be found through a query feed.

## Configuration

Several aspects of Newsboat’s behaviour can be configured via a configuration file which is located, by default, in `~/.newsboat/config`. This configuration file contains lines of the form:

```
<config-command> <arg1> ...

```

The configuration file can also contain comments, which start with the `#` character and go as far as the end of line. If you need to enter a configuration argument that contains spaces, use quotes `"` around the whole argument. It’s even possible to integrate the output of external commands into the configuration. The text between two backticks ``` is evaluated as shell command, and its output is put on its place instead. This works like backtick evaluation in Bourne-compatible shells and allows users to use external information from the system within the configuration.

See [[1]](https://gist.github.com/anonymous/42d2f5956e7bc8ee1ebc) and [[2]](http://moparx.com/configs/newsbeuter/) for example configurations.

**Note:** To see a complete list of configuration command, consult the man page

## Tips

### Automatic feed reloads

You can set Newsboat to automatically reload all of your feeds at startup with the following configuration:

```
auto-reload yes

```

With this setting, Newsboat also runs periodic auto-reloads -- by default, every 60 minutes. The number of minutes between automatic reloads can be configured like so:

```
reload-time <desired number of minutes>

```

Alternatively, you can use [cron](/index.php/Cron "Cron") or [systemd](/index.php/Systemd "Systemd") to automatically reload your feeds. Just add a line in your crontab, or create a systemd service/timer unit combo that issues the following command:

```
/usr/bin/newsboat -x reload

```

### Pass article URL to external command

A clever little hack allows you to pass the url of an article to an external command. The idea is to use a macro to set the browser that Newsboat opens the article with to the path of some other command and then change it back afterwords.

For example, if you subscribe to a youtube channel and you would like to open the video with [mpv](/index.php/Mpv "Mpv"), do the following:

```
macro y set browser "mpv %u"; open-in-browser ; set browser "elinks %u"

```

**Note:** to use a macro, you must first press the `,` key, followed by the keybind. In the example above, you would type `,` + `y`

## Troubleshooting

### Newsboat won't start

Newsboat cannot start without any configured feeds! If you try to do this you will get the following error:

```
Error: no URLs configured. Please fill the file ~/.config/newsboat/urls with RSS feed URLs or import an OPML file.

```

To add urls, see [#Managing feeds](#Managing_feeds)

If that is not the problem, then you probably have another instance of Newsboat running. Newsboat issues a lock on its database so that only one instance can access it at a time; thus, attempting to open a second instance will fail.

## See Also

*   [Official web site](https://newsboat.org/)
*   [Full documentation](https://newsboat.org/releases/2.12/docs/newsboat.html)
*   [Arabesque: RSS with Newsboat](https://sanctum.geek.nz/arabesque/rss-with-newsboat/)