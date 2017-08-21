**Alpine** is based on pine, a text-based E-mail and newsclient that was originally released by the University of Washington in 1991\. It is an easier to use alternative to [mutt](/index.php/Mutt "Mutt"), a more lightweight approach to the mail reader concept.

Right now, this article is just a quick and dirty guide for configuring Alpine to use a remote mailserver with IMAP.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration for use with IMAP](#Configuration_for_use_with_IMAP)
*   [3 Setting up other IMAP folders](#Setting_up_other_IMAP_folders)
*   [4 Setting up a proper return address](#Setting_up_a_proper_return_address)
*   [5 Built in help](#Built_in_help)
*   [6 What else can you configure?](#What_else_can_you_configure.3F)
*   [7 Printing from alpine](#Printing_from_alpine)
*   [8 Tips and Tricks](#Tips_and_Tricks)
*   [9 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [alpine](https://aur.archlinux.org/packages/alpine/). Optionally a spellchecker may be installed. Alpine supports both [aspell](https://www.archlinux.org/packages/?name=aspell) and [hunspell](https://www.archlinux.org/packages/?name=hunspell).

## Configuration for use with IMAP

Alpine can be configured directly from the config file in your home folder; `~/.pinerc` but it's usually easier to use the in-program configuration tools (which are pretty comprehensive anyway). You can also create a system wide pinerc file if you want to, but that's beyond the scope of this page.

To start alpine call up a console or a terminal emulator and type:

```
$ alpine

```

You will see the main menu for alpine, you can select various sub-menus by moving your cursor with the arrow keys. If you have used [nano](/index.php/Nano "Nano") before, this should be very trivial. You should also note that a list of handy commands is given at the bottom of the screen including `?` for built in help (see below).

To get to the configuration options we want to type `S` for "setup" and then `C` for "config" (or select these by using the arrow keys and return). At the top of the screen, there will see various lines you can edit by pressing `C`, for "change value". You'll probably want to fill in your name, the name of your mailserver in "User Domain", your SMTP server for sending mail and, if you want to, the location of things like your saved message folder and postponed message folder.

When specifying your SMTP server, you also need to specify your username on that server (probably your e-mail address) and if you are using some method of encryption SSL or TLS (which is common), note the format:

```
mailserver.org:portnumber/user=username/ssl (or tls)

```

Also note the format for where Alpine is configured to keep saved and postponed messages. This keeps the messages on the mailserver, instead of saving them locally.

```
{mailserver.org:portnumber/user=username/ssl}/path/to/folder

```

You need to put the full entry you've specified for your SMTP Server into "{}" before the path name to the folder on the mailserver.

```
Personal Name                     = Jim Bob
User Domain                       = mailserver.org
SMTP Server (for sending)         = mailserver.org:465/user=jimbob123/ssl
NNTP Server (for news)            = <No Value Set>
Inbox Path                        = <No Value Set: using "inbox">
Incoming Archive Folders          = <No Value Set>
Pruned Folders                    = <No Value Set>
Default Fcc (File carbon copy)    = {mailserver.org:465/user=jimbob123/ssl}~/mail/sent-mail
Default Saved Message Folder      = <No Value Set: using "saved-messages">
Postponed Folder                  = {mailserver.org:465/user=jimbob123/ssl}~/mail/drafts
Read Message Folder               = <No Value Set>
Form Letter Folder                = <No Value Set>
Trash Folder                      = <No Value Set: using "Trash">
Literal Signature                 = <No Value Set>
Signature File                    = <No Value Set: using ".signature">
Feature List                      =

```

To setup Alpine for receiving e-mail from another server using IMAP or POP, check the boxes in the section "Folder Preferences" for "Enable Incoming Folders Collection" and "Enable Incoming Folders Checking". There's a bunch of other stuff to configure, but you can come back to that later. At this point you must restart Alpine for these changes to take effect.

Now from the main menu type `L` to open "Folder List", then select "Incoming Folders". Now you'll probably see your default inbox. You may want to leave this alone in case you receive local mail. To add another folder to receive mail from a remote server type `A` to add a folder.

Alpine prompts you for "name of server to contain folder", enter your mailserver with the format:

```
"mailserver.org:993/user=jimbob123/ssl"

```

where mailserver.org should be replaced by the domain name or IP address of your mailserver, 993 should be replaced by the proper port to connect to, jimbob123 should be replaced by your username (probably your e-mail address) and SSL should be replaced by TLS if you are using TLS instead of SSL.

Now it will prompt you for the name of the folder on your mailserver to use, it's probably "INBOX" and if it isn't hopefully you can find out from your mail provider what it is.

Then it will ask you for a nickname, type whatever you want to call the folder. At this point you might get prompted for your password on the mailserver. Enter it and you should be able to read your e-mail.

## Setting up other IMAP folders

Great, now you can read your INBOX, but what about the rest of your IMAP folders? We'll fix that know:

Type `E` to exit setup and make sure that you save the changes. This should put you back at the main menu type `S` again to bring up the setup menu, but this time pick `L` for collectionLists.

Enter your mailserver info below using the format you should be getting used to by now:

```
Nickname  : My Mailserver
Server    : mailserver.org:993/user=jimbob123/ssl
Path      : ~/mail/
View      :

```

```
   Fill in the fields above to add a Folder Collection to your
   COLLECTION LIST screen.
   Use the "^G" command to get help specific to each item, and
   use "^X" when finished.

```

Note that "Path" is the path on the remote server and you don't have to write:

```
{mailserver.org:993/user=jimbob123/ssl}~/mail/

```

You only need to give the local path on the mailserver (in this case ~/mail/)

## Setting up a proper return address

if you've followed the steps above you can read and write e-mails, but you're probably not specifying your return address correctly, in fact, you will specify you return address properly if and only if the user name on the host computer which is run alpine is the same as your e-mail address on the mail server. In order to fix this we edit the configuration again (type `M` for main menu, type `S` for setup, and `C` for configuration). Then find "Customized Headers" (either use the "Whereis" command to search, or page down a few pages to find this) and change the value to

```
From:  Jim Bob <jimbob123@mailserver.org>

```

Of course, replace Jim Bob with your name and put your proper e-mail address in the <>. While this works, the behavior of alpine with respect to this field is somewhat complex.

## Built in help

Alpine has an extensive built-in help system that is context sensitive, it can be reached by pressing `?`, if you have an item highlighted, this will give you help on that item.

## What else can you configure?

Almost anything, in particular you can specify which colors to use, (from the main menu press `S` for set up, then `K` for colors), a browser to open external links (this is in the "Config" setup that we've previously been modifying"), an alternate text editor to use, different folder views, etc.

Pressing `W` allows you to quickly search for options. Messages can be listed in localtime by enabling the option "Convert Dates to Localtime". Toggling options can be done using the enter key.

## Printing from alpine

[Printing](/index.php/Printing "Printing") from Alpine directly to `lpr` does not work with special characters like Germanic umlauts in the Mail to be printed. The [a2ps](https://www.archlinux.org/packages/?name=a2ps) program does help. You can then edit `~/.pinerc`:

```
# Your default printer selection
printer=*YOURPRINTER* [] a2ps -q --center-title --footer -P*YOURPRINTER*

# List of special print commands
personal-print-command=*YOURPRINTER* [] a2ps -q --center-title --footer -P*YOURPRINTER*

# Which category default print command is in
personal-print-category=3

```

Replace *YOURPRINTER* with the name of your printer. Note that these settings can also be applied in the setup UI of Alpine. See the manpage of `a2ps` for more configuration options.

## Tips and Tricks

There is no direct, or immediately apparent command for arbitrarily invoking an update of the inbox, however, as indirectly referenced in the manual;

```
New mail checking and notification occurs automatically every 2.5 minutes and after certain commands, e.g. refresh-screen (Ctrl-L).

```

## See also

*   [http://www.washington.edu/alpine/](http://www.washington.edu/alpine/) - Official Alpine Page. This page includes links to unofficial Alpine pages that have some handy tutorials (arguably better than the one provided here), hit `C` to open the config menu.