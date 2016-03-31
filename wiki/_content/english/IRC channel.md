**Warning:** Channel statistics are logged [here](https://theos.kyriasis.com/~kyrias/stats/archlinux.html). Speak to [demize](/index.php/User:Kyrias "User:Kyrias") if you would like to opt-out permanently.

This article is about **#archlinux**, the main Arch Linux support [IRC](https://en.wikipedia.org/wiki/Internet_Relay_Chat "wikipedia:Internet Relay Chat") channel, and **#archlinux-offtopic**, the main Arch Linux social channel, both available on the [Freenode](http://www.freenode.net/) network.

There are also a number of other channels dedicated to Arch Linux maintained by community members: see [IRC channels](/index.php/IRC_channels "IRC channels") for a listing.

**Note:** Do not edit this page unless you are a channel op in #archlinux. You are welcome to use the discussion page.

## Contents

*   [1 Usage](#Usage)
*   [2 #archlinux - The official support channel](#.23archlinux_-_The_official_support_channel)
    *   [2.1 #archlinux rules](#.23archlinux_rules)
    *   [2.2 #archlinux guidelines](#.23archlinux_guidelines)
    *   [2.3 #archlinux operators](#.23archlinux_operators)
*   [3 #archlinux-offtopic](#.23archlinux-offtopic)
    *   [3.1 #archlinux-offtopic rules](#.23archlinux-offtopic_rules)
    *   [3.2 #archlinux-offtopic operators](#.23archlinux-offtopic_operators)
*   [4 General information](#General_information)
    *   [4.1 Abbreviations and jargon](#Abbreviations_and_jargon)

## Usage

To join the channels, you need an IRC client. See [List of applications/Internet#IRC clients](/index.php/List_of_applications/Internet#IRC_clients "List of applications/Internet") or [Wikipedia:Comparison of Internet Relay Chat clients](https://en.wikipedia.org/wiki/Comparison_of_Internet_Relay_Chat_clients "wikipedia:Comparison of Internet Relay Chat clients") for a list. **#archlinux** and **#archlinux-offtopic** now have the channel mode set to `+r`, which means that you need to be identified with NickServ. We needed to do this to reduce spam. To register with NickServ, follow the freenode FAQ's instructions found [here](https://freenode.net/faq.shtml#nicksetup). If you are not registered and identified, you will be forwarded to **#archlinux-unregistered**, and not be able to join until you are identified. You can get a list of people who can help you by typing `/msg chanserv access #archlinux list`, or join #freenode and ask there.

Some IRC clients have a race-condition where they try to autojoin channels before you have been identified with NickServ, and to solve it you need to enable SASL. Either look up your IRC client's documentation or look at the freenode [SASL page](https://freenode.net/sasl/) to find instructions for how to enable it.

The following commands can be used inside your IRC client to quickly connect to a server and join a channel, provided that you have registered with NickServ:

```
/connect chat.freenode.net
/msg NickServ IDENTIFY `nick` `password`
/join #archlinux

```

## #archlinux - The official support channel

This is the main channel. The central topic for the channel is support and general discussion about Arch Linux.

The channel is currently `+q $~a`. This means that you have to register and identify with the NickServ service before you can talk in the channel. After you have connected to chat.freenode.net, use the following commands for help getting all set up with NickServ:

```
/query nickserv help register
/query nickserv help identify

```

If `/query` happens to not work in your client you can try using either `/quote nickserv <command>` or `/msg nickserv <command>`.

### #archlinux rules

*   **Follow the guidelines**

	[Freenode network policy](http://freenode.net/policies)

	[Freenode channel guidelines](http://freenode.net/changuide)

	[#archlinux channel guidelines](#.23archlinux_guidelines)

*   **Client settings and bots**
    *   If you want to bring a bot into the channel, then ask an operator *before* you do so.
    *   Auto-response in channel or in pm is not allowed (the only exception is 'away' responses at nick highlight in pm).
*   **Channelbot usage**
    *   There is only one official channel bot. 'phrik!~archbot@archlinux/bot/phrik'
    *   Try to limit the bot usage in channel. Remember, you can `/query phrik` when the output is not needed in-channel.
    *   No spamming of bot commands
*   **Advertising**
    *   Advertising is not allowed unless an op has given you permission to do so.
*   **Content/links**
    *   The main topic of the channel is support for and discussion about Arch Linux.
    *   Talk about general software and hardware is allowed if it does not interfere with the main topic of the channel.
    *   Anything that is not covered by the previous statements is handled on a case-by-case basis at the op's discretion.

### #archlinux guidelines

1.  The language of the channel is English. If you need help in another language, search [international arch channels](/index.php/IRC_channels#International_IRC_channels "IRC channels").
2.  Read the `/topic` on a regular basis. It often contains important information.
3.  Do not participate in [flamewars](https://en.wikipedia.org/wiki/Flaming_(Internet)#Flame_war "wikipedia:Flaming (Internet)"), instantly report violators and trolls to [channel operators](#.23archlinux_operators).
4.  Do not spam the channel, use a pastebin to share something longer than three lines. `program &> program-output.txt` in combination with [pastebin clients](/index.php/Pastebin_Clients "Pastebin Clients") can ease this step.
5.  Do not abuse phrik (the channel bot). If you want to try out commands or look through the help function, then do it in a `/query` or `/msg`. Example: `/query phrik help <command>`.
6.  Do not ask whether anyone is alive or uses your software, just state your question.
7.  [Please follow the standard litany when giving a problem report](http://www.co.kerr.tx.us/it/howtoreport.html). It is easier for us to help you when you [ask good/smart questions](http://www.catb.org/~esr/faqs/smart-questions.html).
8.  Do not demand help, ask for it. Wait for a few minutes before restating questions. Most questions get answered by 'just another user', like you.
9.  Do not be shy, feel free to help others, every user has something to contribute. The channel is a community effort to provide support, and depends on volunteers.
10.  Help yourself before you ask. Use [wiki search](/index.php/Special:Search "Special:Search"), use [forum search](https://bbs.archlinux.org/search.php), read [man pages](/index.php/Man_page "Man page") and try [Google](http://www.google.com). This method will often get you an answer faster, and will teach you more.
11.  When asking for help, always reply to people that ask you for more information, if you do not know the answer then say so.
12.  Set a good example. Each user's behavior affects all users in the channel. Be friendly and polite to maintain a pleasant and professional climate.

### #archlinux operators

If you for some reason need the help of an op, do not be shy to `/query` or `/msg` us. Here is the list of ops as of 4 Feb 2016:

*   [demize](/index.php/User:Kyrias "User:Kyrias")
*   brain0
*   escondida
*   falconindy
*   grawity
*   heftig
*   jelle
*   MrElendig / Mion
*   tigrmesh / tigr
*   vodik
*   wonder / ioni

## #archlinux-offtopic

### #archlinux-offtopic rules

*   **Follow the guidelines**

	[Freenode network policy](http://freenode.net/policy.shtml)

	[Freenode channel guidelines](http://freenode.net/channel_guidelines.shtml)

	[#archlinux channel guidelines](#.23archlinux_guidelines)

*   Ops can kick people entirely at their own discretion, do not be a moron. If you think an op acted unfairly, bring it up.

### #archlinux-offtopic operators

Arch operators are ops in both channels, see [#archlinux operators](#.23archlinux_operators) or `/msg phrik listops` for a list.

## General information

### Abbreviations and jargon

	RTFM 

	Read The Fine Manual

	RTFW 

	Read The Fine Wiki

	RTFB 

	Read The Fine BBS

	RTFN 

	Read The Fine News

	[{core,extra,testing, ...}] 

	Usually denotes a [repository](/index.php/Repository "Repository"). Example: "nvidia drivers are in [extra]"

	AUR 

	Arch User Community Repository

	ABS 

	Arch Build System

	ltt 

	less than three -> '<3' -> 'love'

	TU 

	Trusted User

	BBS 

	Bulletin Board System -> 'forum'

	AFAIK 

	As Far As I Know

	IIRC 

	If I Recall Correctly

	IMO 

	In My Opinion

	FTW 

	For The Win

	FTL 

	For The Loss

	nvm 

	never mind / forget it

	ymmv 

	your mileage may vary

	+b / B& 

	Ban / Banned