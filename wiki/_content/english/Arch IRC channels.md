Related articles

*   [ArchWiki:IRC](/index.php/ArchWiki:IRC "ArchWiki:IRC")
*   [International communities](/index.php/International_communities "International communities")
*   [phrik](/index.php/Phrik "Phrik")

**Note:** Do not edit this page unless you are a channel op in #archlinux. You are welcome to use the discussion page.

To use [Internet Relay Chat](https://en.wikipedia.org/wiki/Internet_Relay_Chat "wikipedia:Internet Relay Chat") (IRC), you need an [IRC client](/index.php/IRC_client "IRC client"). The [installation live environment](/index.php/Installation_guide "Installation guide") includes the [Irssi](/index.php/Irssi "Irssi") client.

You are expected to familiarize yourself with our [Code of conduct](/index.php/Code_of_conduct "Code of conduct") and [Code of conduct#IRC](/index.php/Code_of_conduct#IRC "Code of conduct") before joining any of the official channels. For a list of commonly used abbreviations, see [Arch terminology](/index.php/Arch_terminology "Arch terminology") and [IRC Jargon](http://www.ircbeginner.com/ircinfo/abbreviations.html).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Main channels](#Main_channels)
    *   [1.1 Registration](#Registration)
    *   [1.2 Channel operators](#Channel_operators)
*   [2 Other channels](#Other_channels)
    *   [2.1 International IRC channels](#International_IRC_channels)

## Main channels

**Note:**

*   Due to abuse various gateways and web clients may be banned at times. If you experience trouble use a "*proper*" IRC client or ask one of the operators for a ban exemption (`+e`).
*   Channel statistics are logged for [#archlinux-offtopic](https://alyp.tk/stats/aotstats.html). Speak to *jp/alyptik* if you would like to opt-out permanently.

This section is about [#archlinux](ircs://chat.freenode.net/archlinux), the main Arch Linux support [IRC](https://en.wikipedia.org/wiki/Internet_Relay_Chat "wikipedia:Internet Relay Chat") channel, and [#archlinux-offtopic](ircs://chat.freenode.net/archlinux-offtopic), the main Arch Linux social channel, both available on the [Freenode](https://freenode.net/) network.

The central topic for **#archlinux** is support and general discussion about Arch Linux.

### Registration

In order to reduce spam **#archlinux** and **#archlinux-offtopic** have the channel mode set to `+r` and `+q $~a`. This means you have to be identified via `NickServ` to be able to join these channels and send messages, respectively. If you are not registered and identified, you will be forwarded to **#archlinux-unregistered**.

To register with NickServ, follow the [freenode FAQ](https://freenode.net/kb/answer/registration), as well as `NickServ help` when connected to *chat.freenode.net*:

```
/query NickServ HELP REGISTER
/query NickServ HELP IDENTIFY

```

**Note:**

*   If `/query` happens to not work in your client you can try using either `/quote NickServ <command>` or `/msg NickServ <command>`.
*   Some IRC clients have a race-condition where they try to autojoin channels before you have been identified with NickServ, and to solve it you need to enable SASL. Either look up your IRC client's documentation or look at the freenode [SASL page](https://freenode.net/kb/answer/sasl) to find instructions for how to enable it.
*   You can get a list of people who can help you by typing `/msg ChanServ ACCESS #archlinux LIST`, or join **#freenode** and ask there.

### Channel operators

Arch operators are ops in both **#archlinux** and **#archlinux-offtopic**. See the list below, or run `/msg phrik listops` on freenode.

If you for some reason need the help of an op, do not be shy to `/query` or `/msg` us. Here is the list of ops as of 1 Nov 2018:

*   alad
*   amcrae
*   falconindy
*   gehidore / man
*   grawity
*   heftig
*   jelle
*   MrElendig / Mion
*   Namarrgon
*   pid1
*   tigrmesh / tigr
*   vodik
*   wonder / ioni

## Other channels

The size of our community led to the creation of multiple IRC channels. To get a list of all channels on **[chat.freenode.net](ircs://chat.freenode.net)** that contain `archlinux` in their name, use the command `/query alis list *archlinux*`.

| Channel | Description |
| [#archlinux-aur](ircs://chat.freenode.net/archlinux-aur) | [AUR](/index.php/AUR "AUR") general discussion |
| [#archlinux-aurweb](ircs://chat.freenode.net/archlinux-aurweb) | [aurweb](https://projects.archlinux.org/aurweb.git/) development discussion |
| [#archlinux-bugs](ircs://chat.freenode.net/archlinux-bugs) | Bug-centric discussion |
| [#archlinux-classroom](ircs://chat.freenode.net/archlinux-classroom) | A project that develops and hosts classes for the Arch Linux community. |
| [#archlinux-devops](ircs://chat.freenode.net/archlinux-devops) | Arch Linux internal infrastructure and devops discussions. |
| [#archlinux-multilib](ircs://chat.freenode.net/archlinux-multilib) | Arch Linux Multilib Project discussion and packaging |
| [#archlinux-newbie](ircs://chat.freenode.net/archlinux-newbie) | A space to learn, try new things, and ask for help without fear of ridicule. |
| [#archlinux-pacman](ircs://chat.freenode.net/archlinux-pacman) | [Pacman](/index.php/Pacman "Pacman") development and discussion |
| [#archlinux-projects](ircs://chat.freenode.net/archlinux-projects) | Projects development and discussion (mkinitcpio, abs, dbscripts, devtools, ...) |
| [#archlinux-reproducible](ircs://chat.freenode.net/archlinux-reproducible) | Discussion channel for achieving reproducible builds. |
| [#archlinux-security](ircs://chat.freenode.net/archlinux-security) | Discussion of security issues within Arch packages. |
| [#archlinux-testing](ircs://chat.freenode.net/archlinux-testing) | Discussion channel regarding the testing repositories. |
| [#archlinux-wiki](ircs://chat.freenode.net/archlinux-wiki) | Discussion about [ArchWiki](/index.php/ArchWiki "ArchWiki"), its articles and the [Arch Linux Forums](https://bbs.archlinux.org/). |
| [#archlinux-women](ircs://chat.freenode.net/archlinux-women) | Discussing gender and equality, mostly in English. |
| [#archlinux-proaudio](ircs://chat.freenode.net/archlinux-proaudio) | Discussion of [Arch Linux Pro Audio](/index.php/Professional_audio "Professional audio"). Users also in the unofficial #archaudio |

### International IRC channels

International discussions are available at the following channels, also located at the **[chat.freenode.net](ircs://chat.freenode.net)** IRC network, unless stated otherwise.

| Channel | Description |
| [#archlinux-za](ircs://chat.freenode.net/archlinux-za) | Discussion (Afrikaans, English) |
| [#archlinux-br](ircs://chat.freenode.net/archlinux-br) | Discussion (Brazilian) |
| [#archlinux-cn](ircs://chat.freenode.net/archlinux-cn) | Discussion (Chinese); also on **[irc.oftc.net#arch-cn](ircs://irc.oftc.net/arch-cn)** |
| [#archlinux-cr](ircs://chat.freenode.net/archlinux-cr) | Discussion (Costa Rica) |
| [#archlinux.cz](ircs://chat.freenode.net/archlinux.cz) | Discussion (Czech) |
| [#archlinux.dk](ircs://chat.freenode.net/archlinux.dk) | Discussion (Danish) |
| [#archlinux.fi](ircs://chat.freenode.net/archlinux.fi) | Discussion (Finnish) |
| [#archlinux-fr](ircs://chat.freenode.net/archlinux-fr) | Discussion (French) |
| [#archlinux-gaelic](ircs://chat.freenode.net/archlinux-gaelic) | Discussion (Gaelic) |
| [#archlinux.de](ircs://chat.freenode.net/archlinux.de) | Discussion (German) |
| [#archlinux-greece](ircs://chat.freenode.net/archlinux-greece) | Discussion (Greek) |
| [#archlinux-il](ircs://chat.freenode.net/archlinux-il) | Discussion (Hebrew) |
| [#archlinux.hu](ircs://chat.freenode.net/archlinux.hu) | Discussion (Hungarian) |
| [#archlinux-it](ircs://chat.freenode.net/archlinux-it) | Discussion (Italian); also on **[irc.azzurra.org#archlinux](irc://irc.azzurra.org/archlinux)** |
| [#archlinux-nordics](ircs://chat.freenode.net/archlinux-nordics) | Discussion (the nordics: Danish, Finnish, Norwegian and Swedish) |
| [#archlinux-kr](ircs://chat.freenode.net/archlinux-kr) | Discussion (Korean) |
| [#archlinux-ir](ircs://chat.freenode.net/archlinux-ir) | Discussion (Persian) |
| [#archlinux.org.pl](ircs://chat.freenode.net/archlinux.org.pl) | Discussion (Polish) |
| [#archlinux-pt](ircs://chat.freenode.net/archlinux-pt) | Discussion (Portuguese) |
| [#archlinux.ro](ircs://chat.freenode.net/archlinux.ro) | Discussion (Romanian) |
| [#archlinux-tg](ircs://chat.freenode.net/archlinux-tg) | Discussion (Russian); bridge between IRC and Telegram group [Arch Linux RU](https://t.me/ArchLinuxChatRU) |
| [#archlinux-ru](ircs://chat.freenode.net/archlinux-ru) | Discussion (Russian); also on **[irc.mibbit.net#archlinux-ru](irc://irc.mibbit.net/archlinux-ru)** |
| [#archlinux-rs](ircs://chat.freenode.net/archlinux-rs) | Discussion (Serbian) |
| [#archlinux-es](ircs://chat.freenode.net/archlinux-es) | Discussion (Spanish) |
| [#archlinux.se](ircs://chat.freenode.net/archlinux.se) | Discussion (Swedish) |
| [#archlinux-tr](ircs://chat.freenode.net/archlinux-tr) | Discussion (Turkish) |
| [#archlinux-ve](ircs://chat.freenode.net/archlinux-ve) | Discussion (Venezuela) |
| [#archlinuxvn](ircs://chat.freenode.net/archlinuxvn) | Discussion (Vietnamese, Tiếng Việt) |