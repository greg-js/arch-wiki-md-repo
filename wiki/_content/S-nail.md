# S-nail

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

S-nail is a mail processing system with a command syntax reminiscent of ed with lines replaced by messages. It is intended to provide the functionality of the POSIX mailx command and offers (mostly optional) extensions for line editing, IDNA, MIME, S/MIME, SMTP and POP3 (and IMAP). It is usable as a mail batch language.

This overview page was updated for version **v14.8.5** of S-nail. Excerpt of latest _NEWS_: _-d_ / _debug_ finally offers real dry-run tests, extended **@** message specification, new **source_if** command, many bug fixes. _NEWS_ of older **v14.8.x** releases: [RFC 2231](//tools.ietf.org/html/rfc2231) support, mailing-list support (_followup-to_, _followup-to-honour_, _reply-to-honour_, **Lreply**, **mlist**, **mlsubscribe**), simple builtin HTML viewer, freely configurable spam-checker hooks, command line and addressee hardening (new **-.** option, _expandargv_ and _expandaddr_ variables), improved -t support, _expandaddr_ fine-tuning, new _smime-sign-message-digest_ variable, and many small improvements.

S-nail is a direct descendant of the BSD Mail program that was introduced in 1978 (itself superseding the simpler UNIX mail program) and used to introduce itself (in the Mail reference manual) as follows:

_Mail provides a simple and friendly environment for sending and receiving mail._

_It divides incoming mail into its constituent messages and allows the user to deal with them in any order._

_In addition, it provides a set of ed‐like commands for manipulating messages and sending mail._

_Mail offers the user simple editing capabilities to ease the composition of outgoing messages, as well as providing the ability to define and send to names which address groups of users._

S-nail is thus the _user side_ of the Unix mail system, whereas the _system side_ was traditionally taken by [sendmail](/index.php/Sendmail "Sendmail"). In Arch Linux S-nail supports direct mail delivery via SMTP, so that messages can be send directly to external SMTP servers: In this very mode of operation no local mail-transfer-agent (MTA) is necessary on the _system side_. (Note however that S-nail does not (yet) include a mail-queue mechanism and thus simply tries to send the message over SMTP, directly and immediately.)

## Contents

*   [1 Quick shot](#Quick_shot)
*   [2 First configuration adjustments](#First_configuration_adjustments)
*   [3 Sending mail with an external SMTP server](#Sending_mail_with_an_external_SMTP_server)
*   [4 Interactive usage](#Interactive_usage)
    *   [4.1 I'm in!](#I.27m_in.21)
    *   [4.2 Message composition](#Message_composition)
*   [5 Using S/MIME](#Using_S.2FMIME)
*   [6 Workaround missing OpenPGP support](#Workaround_missing_OpenPGP_support)
*   [7 Using an IMAP mailbox](#Using_an_IMAP_mailbox)

## Quick shot

Because the systemwide Arch Linux configuration file (`/etc/mail.rc`) brings in some useful standard settings, sending mail over a local mail-transfer-agent (MTA), such as [sendmail](/index.php/Sendmail "Sendmail") or [postfix](/index.php/Postfix "Postfix"), can be as easy as follows:

```
# echo 'Message body' | mailx -d -s 'A subject' -a an_attachment.txt foo1@bar.example 'Foo2 <foo2@bar.example>'

```

Using the _-d_ebug flag results in a dry-run that doesn't perform any action for real (including ignorance of the current _save_ and _record_ settings). You can adjust the program which is used as a MTA by setting the variable _sendmail_ (fine-tuning via _sendmail-arguments_, _sendmail-no-default-arguments_, _sendmail-progname_, please see the manual, "Sending mail"):

```
# < /etc/passwd mailx -Ssendmail=/usr/bin/sendmail -Ssendwait -s 'My password file content!' public-foo@bar.example
# echo Message was passed successfully: $?

```

By default message delivery is asynchronous, and S-nail will exit as soon as the prepared message has been passed over to the delivery mechanism (the MTA or the builtin SMTP MTA), stating only wether message preparation was successful (or not). If the _sendwait_ option is set, however, S-nail will wait for the started (builtin) MTA instance to exit and (instead) use the MTA exit status as its message delivery "success" or "failure" status.

Sending messages to file and command "addresses" (not over the MTA) is possible if the _expandaddr_ option is set:

```
# echo bla | mailx -Sexpandaddr -s test ./mbox.mbox
# echo bla | mailx -Sexpandaddr -s test '|cat >> ./mbox.mbox'

```

To avoid environmental noise scripts can (and should) "detach" from configuration files and use the _-S_ and _-X_ command line flags to create their own setup and run necessary commands, respectively. Also _expandaddr_ can be given a value and be used for address verification (the following for example allows _only_ network addressees), and the _-._ command line option will terminate option processing and turn on message send mode: together these form active barriers to prevent misinterpretation of address arguments as command line options and other injection attacks. E.g., the following example can be used "as is" (except for _-d_), provided that you have a **somefile.pdf**, somewhere; it sets the _record_ variable to the pathname of the folder used to record all outgoing mail, so that we then can look into the generated message:

```
# echo Body |
#   LC_ALL=C MAILRC=/dev/null \
#   mailx -d -n -Sv15-compat -Ssendwait \
#     -Sexpandaddr=fail,-all,+addr \
#     -Snosave -Srecord=/tmp/out.mbox \
#     -Smimetypes-load-control \
#     -X'mimetype "application/pdf pdf"' \
#     -Sfrom='Me <me@home>' \
#     -a **somefile.pdf** -s Subject \
#      -. '(foo2bar) <foo2@bar.example>' bob@hey.example
# mailx -Rf /tmp/out.mbox

```

The S-nail manual page tries to provide some kind of _exponential learning-curve_ in its first sections, right after the option listing, and especially the sections "A starter", "Sending mail" and "Reading mail" should be worth a glance when looking for more "quick shots".

## First configuration adjustments

Configuration files are the user-specific `$HOME/.mailrc` and the systemwide `/etc/mail.rc`, the latter of which is subject to the usual ArchLinux update mechanism. Thus let's leave that alone and place the following in the private user-specific configuration file, adjusting bold strings. By the way, by using the _-n_ command line argument or by setting the _$NAIL_NO_SYSTEM_RC_ environment variable it is possible to avoid that the global configuration file will be loaded, and by pointing the _MAILRC_ environment variable to `/dev/null` the unavoidable per-user configuration file can be turned behaviour neutral; we've used these possibilities in the detached script example above. And note that all the remaining examples in this document are based upon this configuration template, which simply sets some security and send mode basics:

```
# All the examples require v15-compat!
set v15-compat

# ArchLinux-specific locations of certificates.
# Since these are subject to the ArchLinux update mechanism,
# use only those, don't try to load OpenSSL builtin ones.
# And use the TLS specific set: see "man 8 update-ca-trust"
#set ssl-ca-dir=/etc/ssl/certs
set ssl-ca-file=/etc/ssl/certs/ca-certificates.crt
set ssl-no-default-ca

# Don't use protocols older than TLS v1.2.
# Change this only when the remote server doesn't support it:
# maybe use ssl-protocol-HOST (or -USER@HOST) syntax to define
# such explicit exceptions, then, e.g.
#     _ssl-protocol-**USER**@archlinux.org_="-ALL,+TLSv1.2"
set ssl-protocol="-ALL,+TLSv1.2"

# Explicitly define the list of ciphers, which may improve security,
# especially with protocols older than TLS v1.2\.  See ciphers(1).
# Hint: it is important to include "@STRENGTH": only with it the
# final list will be sorted by algorithm strength.
# This is an example: in reality it is possibly best to only use
# ssl-cipher-list-HOST (or -USER@HOST), as necessary, again..
set ssl-cipher-list="ALL:!aNULL:!MEDIUM:!LOW:!MD5:!RC4:!EXPORT:@STRENGTH"

# Request strict transport security checks
set ssl-verify=strict

# Essential setting: select allowed character sets
# (Have a look at the "CHARACTER SETS" manual section)
set sendcharsets=utf-8,iso-8859-1

# A very kind option: when replying to a message, first try to
# use the same encoding that the original poster used herself!
set reply-in-same-charset

# When replying to or forwarding a message the comment and name
# parts of email addresses are removed unless this variable is set
set fullnames

# When sending messages, wait until the Mail-Transfer-Agent finishs.
# Only like this you'll be able to see errors reported through the exit
# status of the MTA (including the builtin SMTP one)!
set sendwait

# Only use builtin MIME types, no mime.types(5) files.
# That set is often sufficient, but look at the output of the
# **mimetype** command to ensure this is true for you, too
set mimetypes-load-control

# Default directory where we act in (relative to $HOME)
set folder=mail
# A leading "+" (often) means: under _folder_
# _record_ is used to save copies of sent messages
set MBOX=+mbox.mbox record=+sent.mbox DEAD=+dead.mbox

# Define some shortcuts; now one may say, e.g., **file mymbo**
shortcut mymbo %:+mbox.mbox \
         myrec +sent.mbox

# This is optional, but you should get the big picture
# by reading the manual before you leave that off
set from="**Your Name <youremail@domain>**" 

# Mailing-list specifics (manual: "Mailing lists"):
set followup-to followup-to-honour=ask-yes reply-to-honour=ask-yes
# And teach some non-subscribed / some subscribed lists, too
mlist @xyz-editor.xyz$ @xyzf.xyz$
mlsubscribe ^xfans@xfans.xyz$

```

The above combination of SSL/TLS configuration results in the most secure end-to-end TLS transport that is possible at the time of this writing.

When in the following **USER** and **PASS** informations are specified as part of an URL (other possibilities exist) they must become URL percent encoded; S-nail offers the **urlencode** command which does this for you:

```
# printf 'urlencode USER PASS\nx\n' | mailx -#

```

Of course: printf as well as S-nail / mailx are subject to your locale settings:

```
# # In UTF-8:
# printf 'urlencode SPAß\nx\n' | mailx -#
  in: <SPAß> (5 bytes)
  out: <SPA%C3%9F> (9 bytes)
# # In ISO-8859-1:
# printf 'urlencode SPAß\nx\n' | mailx -#
  in: <SPAß> (4 bytes)
  out: <SPA%DF> (6 bytes)

```

## Sending mail with an external SMTP server

To send messages via the builtin SMTP (Simple Mail Transfer Protocol) client to an external SMTP server, several options have to be set or adjusted. Add the following as appropriate to the configuration as above, changing bold strings.

```
# It may be necessary to set _hostname_ and/or _smtp-hostname_
# if the "SERVER" of _smtp_ and "domain" of _from_ don't match.
# Reading the "ON URL SYNTAX.." and _smtp_ manual entries may be worthwhile
# (Remember **USER** and **PASS** must be URL percent encoded)
set smtp=**(smtp[s]/submission)://[USER[:PASS]@]SERVER[:PORT]** \
    smtp-auth=**login[/plain]...** \
    smtp-use-starttls

# E.g. here is a real life example of a very huge free mail provider
# (Activate this account via _mailx -AXooglX_ from the command line,
# or use the _? acc[ount] XooglX_ command in interactive mode)
account XooglX {
   # Localize options, forget them when changing the account
   localopts yes
   # (The plain smtp:// proto is optional)
   set smtp=**USER:PASS**@smtp.gmXil.com smtp-use-starttls
   set from="**Your Name <youremail@domain>**"
}

# And here is a pretty large one which does not allow sending mails
# if there is a domain name mismatch _on the SMTP protocol level_,
# which would bite us if the value of _from_ does not match, e.g.,
# for people who have a sXXXXeforge project and want to speak
# with the mailing list under their project account (in _from_),
# still sending the message through their normal mail provider
account XandeX {
   localopts yes
   set smtp=smtps://**USER:PASS**@smtp.yaXXex.ru:465 \
       hostname=yaXXex.com smtp-hostname=
   set from="**Your Name <youremail@domain>**"
}

```

**Tip:** If you have enabled two-step authentication in Gmail, and you have added an application specific password for S-nail, you will want to use that password rather than your regular Gmail password, which may work without enabling the otherwise necessary "less secure apps".

Note that, when storing passwords in `$HOME/.mailrc`, you should set appropriate permissions with `chmod 0600`. You can also set the _netrc-lookup_ option and store user credentials in `$HOME/.netrc` (or _$NETRC_) instead; e.g., here is a real life example that sets up SMTP, POP3 as well as IMAP, storing all user credentials in there:

```
account XandeX {
   localopts yes
   set from="Your Name <youremail@domain>"
   set netrc-lookup
   #set agent-shell-lookup="gpg -d .pass.gpg"
   set smtp=smtps://smtp.yXXXXx.ru:465 \
       smtp-hostname= hostname=yXXXXx.com
   set pop3-keepalive=240
   shortcut pop pop3s://pop.yXXXXx.ru
   # Type **xp** to login to the POP3 account
   ghost xp 'fi pop'
   set imap-keepalive=240
   shortcut imap imaps://imap.yXXXXx.ru
   # Type **xi** to login to the IMAP account
   ghost xi 'fi imap'
 }

```

and, in `$HOME/.netrc`:

```
machine *.yXXXXx.ru login **USER** password **PASS**

```

(Here **USER** and **PASS** are clear text, not URL encoded.) You can furtherly diversify things and use encrypted password storage, since ArchLinux compiles in password agent support. To adjust the example, simply don't specify the _password **PASS**_ token in `$HOME/.netrc` but instead uncomment the _agent-shell-lookup_ line in the example account above. The encrypted password storage `.pass.gpg` can be created like this:

```
# echo **PASS** > .pass
# gpg -e .pass
# eval `gpg-agent --daemon --pinentry-program=/usr/bin/pinentry-curses --max-cache-ttl 99999 --default-cache-ttl 99999`

```

Test the configuration (use the _-d_ command line option for a dry-run):

```
# echo test-body | mailx -vv -A XandeX -s test-subject **some@where**

```

## Interactive usage

The ArchLinux version of S-nail includes the builtin command line editor with history capabilities as well as regular expression and coloured message display support. Because S-nail strives for POSIX standard compliance some settings have to be adjusted before using it interactively doesn't baffle all descriptions, however. Reading the manual is unavoidable, but add, at a minimum, the following on top of the example configuration:

```
# (The global configuration /etc/mail.rc provides some commented basics;
# in particular it shows all options that POSIX mandates as defaults.)

# Start into interactive mode even if the system mailbox is empty or
# doesn't exist.  S-nail would exit immediately without that one
set emptystart

# When composing a message, let period `.' on a line by itself finalize
# composition, before start directly into _$EDITOR_
set dot 
set editalong

# Start _$PAGER_ when a message is longer than VALUE lines;
# without VALUE: screen _$LINES_
set crt=

# Colourize headers when displaying messages (note that _$PAGER_ may
# require special flags, e.g., less(1) needs the -R option; S-nail will
# however set the _$LESS_ environment variable accordingly, but only if
# that was not set before..)
set colour-pager

# A nicer prompt for a modern terminal
set prompt="\033[31m?\?[\$ \@]\& \033[0m"

# Add more entries to the history, and make that persistent
set history-gabby NAIL_HISTFILE=+.s-nailhist NAIL_HISTSIZE=-1

# When **p**rinting messages, show only these headers
# (Easier to **retain** what you want than to **ignore**
# what you don't; use **P**rint to see all headers and **S**how
# to see the raw message content)
retain date from to cc subject

# Try to get around weird MIME attachment specifications
# (This option can take a value, see the manual for more)
set mime-counter-evidence

# Display HTML parts inline, nicer than what the builtin viewer can achieve
#set pipe-text/html="lynx -stdin -dump -force_html"
# Learn another mimetype
mimetype 'model/vrml wrl vrml'

# Create some new commands so that, e.g., `ls /tmp' will..
ghost ls !ls -latro
ghost ps !ps axu

```

Once you're in it use **list** to print all available builtin commands. ArchLinux compiles in the "DOCSTRINGS" feature, so that typing `?X' tries to expand "X" and print a help string; since S-nail will allow abbreviations of all commands this is sometimes handy; try, e.g., **?h**, **?he** and **?hel** ... The command **help** will print a short summary of the most frequent used commands.

### I'm in!

When starting into interactive mode a summary of the content of the initially opened mailbox is printed, as via the **headers** command. In the header display messages are given numbers (starting at 1) which uniquely identify messages. Messages can be printed with the **print** command, or short: **p**. Whereas **p** honours **retain**ed (or **ignore**d) list of headers to be displayed, the **P**rint command will not and display all headers; the **Sh**ow command will print raw message content.

By default the current message (dot) is printed, but just like with many other commands it is possible to specify lists of messages, as is documented in the manual section "Specifying messages"; e.g., **p:u** will display all unread messages, **p.** will print the dot, **p 1 5** will print the messages 1 and 5 and **p-** and **p+** will print the last and the next message, respectively. Note that simply typing RETURN in an empty line acts like **next** (**n**), and thus prints the next message.

The command **from** (**f**) is nice for an overview, e.g., **f '@<@arch linux'** will print the header summary of all messages that contain the string "arch linux" in some message header, whereas **f '@arch linux'** will only match those with "arch linux" in their subject; finally, the regular expression **f @^A[^[:space:]]+** finds... well, a complaint of the ArchWiki maintainer about the content of this page, ugh; that is, be aware that quoting may be necessary when there is whitespace in search expressions etc.

*   **file** and **File** open a new mailbox, the latter in readonly mode (which can be handy to avoid flag updates etc.)
*   **newmail** (dependent on the mailbox, checks for new mail and) prints a listing of new messages
*   **he** (headers) reprints the message list
*   **z-**, **z+**, **z0**, **z$** scroll through the header display (dependent on the terminal you are using the Home/End/PageUp/PageDown keys will be working aliases)
*   **folders** shows a listing of mailboxes under the currently set _folder_
*   **r** replies to all addressees of the given message(s)
*   **R** replies to the sender of the given message(s)
*   **Lreply** "mailing-list" reply to the given message(s)
*   **move** or **mv** moves (a) message(s)
*   **(un)flag** marks (a) message(s) as (un)flagged
*   **new** marks (a) message(s) unread
*   **seen** marks (a) message(s) read
*   **P** prints (a) message(s) with all headers
*   **p** prints (a) message(s) and all non-ignored headers.
*   **show** prints the raw message of content of (a) message(s)

### Message composition

Composition is started by typing **mail user@host** or by replying to a message. When you return from _$EDITOR_ (assuming _editalong_ is set) you'll find yourself in the native editor, where many operations can be performed using tilde escapes (short help available via **~?**). Of particular interest is **~@**, which either allows interactive editing of the attachment list, or, when given arguments, to add a(n) (comma-separated list of) additional attachment(s).

To send the mail, signal EOT with `Ctrl+d` or type "." on its own line (the latter requires the _dot_ option).

## Using S/MIME

The manual contains a step-by-step example of how to create your certificates etc. ("Signed and encrypted messages with S/MIME"). Assuming you have your private key and signed certificate already, just create the paired file we need

```
# cat private-key.pem signed-certificate.pem > ~/pair.pem

```

and setup S-nail via

```
set smime-sign-cert=~/pair.pem \
    smime-sign-message-digest=SHA256 \
    smime-sign

```

From now any message that is sent will be signed. The default message digest would be SHA1, as mandated by [RFC 5751](//tools.ietf.org/html/rfc5751). Note that S/MIME always works relative to the setting of the variable _from_, so it seems best to instead place the above settings in an **account**. The **verify** command verifies S/MIME messages, but note that S/MIME decryption and verification is solely based upon OpenSSL for now, which only supports messages with a simplicistic MIME structure. Sorry. By the way, if you miss hyperlinks and a table-of-content to get yourself going, the manual on the projects' website offers this; and the manual that ships with ArchLinux does, too, but needs the mdocmx(7) extension to be visible.

## Workaround missing OpenPGP support

S-nail doesn't yet support OpenPGP. However, using a macro it is possible to at least automatically verify inline _--clearsign_ed messages, and using command ghosts their usage becomes handy: e.g., use the following in resource file and you will be able to verify a clearsigned message by just typing **V**:

```
 define V {
   localopts yes
   set pipe-text/plain="set -C;\
     : > \"${TMPDIR}/${NAIL_FILENAME_GENERATED}\";\
     trap \"rm -f \\\"${TMPDIR}/${NAIL_FILENAME_GENERATED}\\\"\" EXIT;\
     trap \"exit 75\" INT QUIT TERM;\
     set +C;\
     cat > \"${TMPDIR}/${NAIL_FILENAME_GENERATED}\";\
     < \"${TMPDIR}/${NAIL_FILENAME_GENERATED}\" awk \
         -v TMPFILE=\"${TMPDIR}/${NAIL_FILENAME_GENERATED}\" '\
       BEGIN {done=0}\
       /^-----BEGIN PGP SIGNED MESSAGE-----/,/^$/ {\
         if (done++ != 0)\
           next;\
         print \"--- GPG --verify ---\";\
         system(\"gpg --verify \" TMPFILE \" 2>&1\");\
         print \"--- GPG --verify ---\";\
         print \"\";\
         next;\
       }\
       /^-----BEGIN PGP SIGNATURE-----/,/^-----END PGP SIGNATURE-----/ {\
         next;\
       }\
       {print}\
       '"
   print
 }
 define RK {
   !printf 'Key IDs to gpg --recv-keys: ';\
     read keyids;\
     gpg --recv-keys ${keyids};
 }
 ghost V call V
 ghost RK call RK

```

## Using an IMAP mailbox

The following is only a quick hint, it is also possible to define _folder_ to point to an IMAP server folder, for example.

```
set v15-compat

# or many servers will expire the session
set imap-keepalive=240
set imap-cache=~/.imap_cache

# You may want to define shortcuts to folders, for example:
shortcut myimap "**imaps://USER:PASS@server:port"**

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=S-nail&oldid=408068](https://wiki.archlinux.org/index.php?title=S-nail&oldid=408068)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Email clients](/index.php/Category:Email_clients "Category:Email clients")