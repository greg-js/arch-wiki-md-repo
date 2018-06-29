**Note:** DansGuardian is no longer maintained. An actively developed fork is [e2guardian](https://aur.archlinux.org/packages/e2guardian/).

From the project [home page](http://dansguardian.org):

	DansGuardian is an award winning Open Source web content filter which currently runs on Linux, FreeBSD, OpenBSD, NetBSD, Mac OS X, HP-UX, and Solaris. It filters the actual content of pages based on many methods including phrase matching, PICS filtering and URL filtering. It does not purely filter based on a banned list of sites like lesser totally commercial filters.

	DansGuardian is designed to be completely flexible and allows you to tailor the filtering to your exact needs. It can be as draconian or as unobstructive as you want. The default settings are geared towards what a primary school might want but DansGuardian puts you in control of what you want to block.

	DansGuardian is a true web content filter.

DansGuardian is excellent at filtering pages from the Internet as it examines both the URL and the content of the page, and it has many options to allow you to fine tune the process. To run DansGuardian, you will first need a proxy in place. DansGuardian will work with many proxy servers, such as [Polipo](/index.php/Polipo "Polipo") or [tinyproxy](https://www.archlinux.org/packages/?name=tinyproxy), but [Squid](/index.php/Squid "Squid") is the recommended one.

The original author of this article runs Squid and DansGuardian content filters at several schools in the UK, successfully blocking inappropriate content.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Configuration files](#Configuration_files)
    *   [2.2 Blacklists](#Blacklists)
    *   [2.3 "Access Denied" template](#.22Access_Denied.22_template)
    *   [2.4 Web frontend](#Web_frontend)

## Installation

[Install](/index.php/Install "Install") the [dansguardian](https://aur.archlinux.org/packages/dansguardian/) package.

After [#Configuration](#Configuration), [start/enable](/index.php/Start/enable "Start/enable") the `dansguardian.service` systemd service.

## Configuration

### Configuration files

Configuration files, blocking templates, blacklists, etc are stored in `/etc/dansguardian`.

DansGuardian has the concept of groups, which are groups of users or machines that have certain blocks applied to them. The following sets up one group for everyone---the idea being that anyone who wants unfiltered access could just hit Squid directly. (This is not ideal.)

Edit `/etc/dansguardian/dansguardian.conf`. The defaults are suitable for most users, and the file is well-commented. Be sure to check the options under Network Settings for `filterip`, `filterport`, `proxyip` and `proxyport`. You may also want to examine `weightedphrasemode` and `phrasefiltermode`. The filter mode is especially important if you are running this setup on older hardware.

Next edit the options for the first, and only, group in this setup. Edit the file `/etc/dansguardian/dansguardianf1.conf`, which is well-commented. Pay attention to the `naughtynesslimit`.

DansGuardian examines the content on a page and adds up the naughty words based on a weighting scheme, with worse words getting more points. If this total exceeds the `naughtnesslimit`, the page will be blocked. 50 is a good limit for young children, whereas 160 is good for young adults. In a corporate environment, you'd want this set around 200.

### Blacklists

Adding websites to the block lists are done in the same directory, in the almost self-explanatory configuration files. DansGuardian provides a powerful regular expression URL and content filter, as well as ordinary URL blocklists. Some of the important files are:

*   bannedsitelist - The domains for your banned sites, e.g. "human-horse-love.com"
*   bannedurllist - If you just want to block part of a website, e.g. "bbc.co.uk/games"
*   exception* - This is where your domain/URL exceptions go. Sites in this list will not be checked and allowed straight through.
*   bannedregexpurllist - Very powerful. This is where you can put regular expressions to block certain URLs, e.g. "(.*q=.*xxx.*)" to stop searching for the word "xxx".

Whenever you add or remove a URL from the list, you must tell DansGuardian you have done so. This can be done with:

```
# dansguardian -r

```

Which will force DansGuardian to reload it's configuration. Doing it this way, rather than restarting the daemon, will mean that for the most part your users won't notice reloading. (I've noticed that straight after the reload, users may have trouble accessing web pages for about 5-10 seconds - if this is a problem you can always run a cronjob at 12am to run `dansguardian -r`).

You can download a blacklist collection from [URLBlacklist](http://urlblacklist.com), but be sure to read the [FAQ](http://urlblacklist.com/?sec=faq) first, as you will, paradoxically, want to unsort the collection to enable DansGuardian to start faster. Optionally, you can find blacklists at [Squidblacklist.org](http://www.squidblacklist.org), Once you have installed a blacklist under `/etc/dansguardian` you can add them to your DansGuardian configuration by opening the appropriate configuration file and adding:

```
.Include</etc/dansguardian/blacklists/ads/domains>
.Include</etc/dansguardian/blacklists/drugs/domains>
.Include</etc/dansguardian/blacklists/porn/dg-porn
etc...

```

To the bottom of the file. Take a look around the blacklist collection to see what is available.

### "Access Denied" template

If you wish to change the page that gets displayed to users when a website is blocked, you need to edit the file:

```
/usr/share/dansguardian/languages/*LANGUAGE*/template.html.

```

### Web frontend

If you would like a web-based frontend to manage DansGuardian, you could use [Webmin](/index.php/Webmin "Webmin") with the DansGuardian [Webmin Module](http://sourceforge.net/projects/dgwebminmodule/).