Phrik is the villainous IRC bot in Arch Linux's [IRC channels](/index.php/IRC_channel "IRC channel"). He is a [supybot](http://sourceforge.net/projects/supybot/) with loads of handy factoids and utilities for things like searching Google, the ArchWiki, and the [AUR](/index.php/AUR "AUR"), which is useful for quickly giving people links to what they need. Custom commands can be edited or added once registered (not to be confused with NickServ registration.)

## Contents

*   [1 Account](#Account)
    *   [1.1 Registering](#Registering)
    *   [1.2 Identifying](#Identifying)
    *   [1.3 Identify with hostname](#Identify_with_hostname)
        *   [1.3.1 Adding a new hostmask](#Adding_a_new_hostmask)
        *   [1.3.2 Removing a hostmask](#Removing_a_hostmask)
        *   [1.3.3 Listing hostmasks](#Listing_hostmasks)
*   [2 Factoids](#Factoids)
    *   [2.1 Searching factoids](#Searching_factoids)
    *   [2.2 Finding out info about factoids](#Finding_out_info_about_factoids)
    *   [2.3 Creating new factoids](#Creating_new_factoids)
    *   [2.4 Factoid locking](#Factoid_locking)
    *   [2.5 Modifying factoids](#Modifying_factoids)
        *   [2.5.1 Regex substitute](#Regex_substitute)
        *   [2.5.2 Replacing a factoid](#Replacing_a_factoid)
    *   [2.6 Deleting factoids](#Deleting_factoids)
*   [3 Quotes](#Quotes)
    *   [3.1 Grab](#Grab)
    *   [3.2 Quote](#Quote)
    *   [3.3 Random](#Random)
    *   [3.4 Search](#Search)
    *   [3.5 List](#List)
    *   [3.6 Say](#Say)
    *   [3.7 Get](#Get)

## Account

**Warning:** Remember to query phrik in a private message with `/msg phrik` for operations related to your account. Prefixing commands with `!` is not required in this case.

### Registering

To make new or change already existing factoids you need to have a phrik account, which doesn't have to be named the same as your IRC nick.

```
register <name> <password>

```

Example: `register demize stuff` to register an account named `demize` with the password `stuff`

### Identifying

To identify with phrik for the current session, or until you `unidentify`, you need to run the following command:

```
identify <name> <password>

```

Example: `identify demize stuff`

### Identify with hostname

If you don't want to have to identify with phrik every time you connect you can add a hostmask to your phrik account which will make him identify you automatically everytime you connect from that host. They are in the form of `nick!ident@host`.

Be careful what hostmask you add tho, since anyone connecting with that hostmask will be identified as you so you don't want to add the host from your ISP since that will likely change a lot. To be autoidentified with a hostmask you'll want to either IRC from a server or have a cloak, otherwise the host will likely change a lot and thus others might get identified as you. If you are going to get identified with a host you might also want to run an ident server so that others connecting from the same server wont be able to fake being you.

Two good examples are `demize!kyrias@theos.kyriasis.com` or `*!*@archlinux/op/demize`.

#### Adding a new hostmask

To add a hostmask send the following command to phrik in private:

```
hostmask add <hostmask>

```

Example: `!hostmask add demize!kyrias@theos.kyriasis.com`

#### Removing a hostmask

```
hostmask remove <name> <hostmask>

```

```
hostmask remove demize demize!kyrias@theos.kyriasis.com

```

#### Listing hostmasks

```
hostmask list

```

## Factoids

Phrik has the MoobotFactoids plugins means that users can create, recall and give others factoids, which are small messages.

To make phrik recall a factoid you can either send the key of the factoid prefixed with an exclamation mark either to a channel where he is in or in private, like this:

 `!welcome` 

### Searching factoids

To search existing factoids, you can use the listkeys and listvalues commands:

 `!listkeys welcome` 

or

 `!listvalues welcome` 

### Finding out info about factoids

If you want to find out who and when a factoid was created you can use the factinfo command:

 `!factinfo welcome` 

### Creating new factoids

Creating a new factoid is as easy as typing the key you want the factoid to be recalled by, `is` and then the message. Often you want to prepend the message with `<reply>` so that phrik will just write the message exactly as you give it, instead of printing `<key> is <value>`.

Making a factoid like this:

 `!example is "<reply>This is an example factoid"` 

Will make phrik send `This is an example factoid` to the channel or pm whenever someone says `!example` in the channel. If the `<reply>` is omitted phrik will instead say `example is This is an example factoid`.

### Factoid locking

Factoid can be locked to prevent other people from removing or overwriting a factoid, but there's generally no need for that as it's just in the way if there ends up being a good reason for the factoid being changed. Normally locking and unlocking would be done by calling the commands from the `MoobotFactoids` plugin, but `!fact` is aliased to `!MoobotFactoids` for convenience.

If a factoid you think should be changed is locked, firstly contact the person who locked it (`!factinfo` will tell you), and if the person is either unavailable or refuses to change it but you still think it should be, due to breaking the rules or similar, feel free to contact the ops. (To get a list of ops send `!listops` to phrik in a pm.)

 `!fact lock *<factoid key>*` 

or

 `!fact unlock *<factoid key>*` 

### Modifying factoids

For modifying a factoid there are two alternatives, the first is using a regex substitute and the second is replacing it completely. Regex replaces have the good property of keeping the original creator info and who last modified it.

#### Regex substitute

To replace the word "This" in the example factoid with the word "That" you can use regex replace like this:

 `!example =~ s/This/That/` 

#### Replacing a factoid

Completely replacing a factoid with something new can be done with the no command like this:

 `!no example is "<reply>a really bad example factoid"` 

### Deleting factoids

Removing a factoid is done with `!MoobotFactoids remove *<factoid key>*`, but since that is to long there exists an alias for convenience called `!rmfact`. Don't delete others factoids without a good reason, and do ask first if you're unsure.

 `!rmfact *<factoid key>*` 

## Quotes

Phrik uses the QuoteGrabs plugin to provide an easy to use system for storing and retrieving things users say. You do not need to be identified with phrik to grab/retrieve quotes. All the QuoteGrabs commands can be listed using the command `!list QuoteGrabs`.

(The `*<channel>*` argument does not seem to make any difference to the result of any of the commands listed below.)

### Grab

The `!grab *<nickname>*` command is used to "grab" a quote. This means that the last thing `*<nickname>*` said will be stored in phrik's internal database. Example:

 `!grab Arch-TK` 

`!grab` is synonymous to `!QuoteGrabs grab`.

### Quote

The `!quote *<nickname>*` command is used to view the last grabbed quote.

`!quote` is synonymous to `!QuoteGrabs quote`, and so is `!q`

### Random

The `!QuoteGrabs random *[<nickname>]*` command is used to view a random selection of quotes. Given a `*<nickname>*` the selection is narrowed to just one user.

The alias `!rq` can be used in place of `!QuoteGrabs random` and the alias `!multirq` gives a selection of 5 random quotes instead of just 1.

### Search

The `!QuoteGrabs search *[<channel>]* *<text>*` command is used to search phrik's quote database for a quote containing a given string. This command does a literal search, this means that searching for "Arch-TK broken" will not return any search results unless that literal result is found. For example:

 `!QuoteGrabs search "Arch-TK Windows"` 

Will not return `#35732: Windows ME, best windows.`.

The alias `!qfind` can be used in place of `!QuoteGrabs search`.

### List

The `!QuoteGrabs list *[<channel>]* *<nickname>*` command is used to list all the quotes for a given user.

The alias `!qlist` can be used in place of `!QuoteGrabs list`.

### Say

The `!QuoteGrabs say *[<channel>]* *<id>*` command is used to view the full quote text using an ID returned by the search and list functions.

For example:

 `!QuoteGrabs say 34656` 

Will return: `<sudokode> ew you might as well be using windows`

The alias `!qsay` can be used in place of `!QuoteGrabs say`.

### Get

The `!QuoteGrabs get *[<channel>]* *<id>*` command is very similar to the *Say* command. It returns the full text of the quote along with additional information.

For example:

 `!QuoteGrabs get 34656` 

Will return:

 `<sudokode> ew you might as well be using windows (Said by: sudokode!~ponies@unaffiliated/sudokode; grabbed by quantum-mechanic!~neutrino@unaffiliated/electron/x-8286743 at 11:21 AM, November 12, 2014` 

The alias `!qget` can be used in place of `!QuoteGrabs get` but does not permit using a `*<channel>*` argument.