Arch Linux uses the BSD Mail descendant S-nail as its POSIX mailx incarnation. Mailx is the *user side* of the Unix mail system, whereas the *system side* was traditionally taken by [sendmail](/index.php/Sendmail "Sendmail"). S-nail is MIME capable and has extensions for line editing, S/MIME, SMTP and POP3, among others. In Arch Linux it supports direct mail delivery via SMTP, so that messages can be sent directly to external SMTP servers: In this very mode of operation no local mail-transfer-agent (MTA) is necessary on the *system side*. Note, however, that it does not have a mail-queue mechanism, but simply tries to send the message over SMTP once and directly.

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

The [s-nail](https://www.archlinux.org/packages/?name=s-nail) package is part of the Arch Linux [base](https://www.archlinux.org/groups/x86_64/base/) group and therefore hopefully installed already. v14.9.0 brought a lot of changes and improvements, reading the [announcement](https://www.sdaoden.eu/code-nail-ann.html) may be helpful.

Because the systemwide configuration file (`/etc/mail.rc`) brings in some useful standards, sending mail over an installed local mail-transfer-agent (MTA), such as [sendmail](/index.php/Sendmail "Sendmail") or [postfix](/index.php/Postfix "Postfix"), can be as easy as follows:

```
# echo 'Message body' | mailx -d -s 'A subject' -a an_attachment.txt foo1@bar.example 'Foo2 <foo2@bar.example>'

```

Using the `-d`ebug flag results in a sandbox dry-run. You can adjust the program which is used as a MTA by setting the variable `mta` (fine-tuning via `mta-arguments`, `mta-no-default-arguments`, `mta-argv0`. See the manual, "On sending mail, and non-interactive mode"):

```
# < /etc/passwd LC_ALL=C mailx -d -:/ -Ssendwait -Sttycharset=utf8 -Smta=/usr/bin/sendmail -s 'My password file!' -. 'Back <side@book>'
# echo Message was passed successfully: $?

```

By default message delivery is asynchronous, and mailx will exit as soon as the prepared message has been passed over to the delivery mechanism, stating only whether message preparation was successful (or not). If the `sendwait` option is set, however, the exit status of the started (builtin or not) MTA will be used as the message delivery "success" or "failure" status.

The `-.` command line option will forcefully terminate option processing and turn on message send mode.

As shown in the previous example scripts can (and should) detach from environmental settings and configuration files via`
**Template error:** are you trying to use the = sign? Visit [Help:Template#Escape template-breaking characters](/index.php/Help:Template#Escape_template-breaking_characters "Help:Template") for workarounds.
`and `-:/`, and use explicit `-S` and `-X` command line flags to create their own reproducible setup.

Sending messages to file and command "addresses" (not over the MTA) is possible if the `expandaddr` option is set:

```
# echo bla | mailx -Sexpandaddr -s test ./mbox.mbox
# echo bla | mailx -Sexpandaddr -s test '|cat >> ./mbox.mbox'
# echo bla | mailx -Sexpandaddr -s test -

```

`expandaddr` can be given a value and be used for address verification. For example, the following *only* allows network addressees. The following example can be used as is, except for {ic|-d}}, provided that you have a *somefile.pdf* somewhere. It sets the `record` variable to the pathname of the folder used to record all outgoing mail, so that we then can look into the generated message:

```
# echo Body |
#   LC_ALL=C mailx -d -:/ -Sv15-compat -Ssendwait -Sttycharset=utf8 \
#     -Sfrom='Me <me@home>' \
#     -Sexpandaddr=fail,-all,+addr \
#     -Snosave -Srecord=/tmp/out.mbox \
#     -Smimetypes-load-control \
#     -X'mimetype application/pdf pdf' \
#     -a somefile.pdf -s Subject \
#      -. '(foo2bar) <foo2@bar.example>' bob@hey.example
# mailx -Rf /tmp/out.mbox

```

The manual sections "A starter", "On sending mail, and non-interactive mode" and "On reading mail, and interactive mode" should be worth a glance when looking for more "quick shots".

In cases when in the following *USER* and *PASS* are specified as part of an URL (and only then), they must become URL-percent-encoded: mailx offers the `urlcodec` command which does this for you:

```
# printf 'urlcodec encode *USER* *PASS*
x
' | mailx -#

```

printf as well as mailx are subject to your locale settings:

```
# # In UTF-8:
# printf 'urlcodec encode SPAß
x
' | mailx -#
  SPA%C3%9F
# # In ISO-8859-1:
# printf 'urlc enc SPAß
x
' | mailx -#
  SPA%DF

```

## First configuration adjustments

Configuration files are the user-specific `$HOME/.mailrc` and the systemwide `/etc/mail.rc`, the latter of which is subject to the usual ArchLinux update mechanism, thus volatile and not the right place for modifications. All the remaining examples in this article are based upon this configuration template, which simply sets some security and send mode basics:

```
# All the examples require v15-compat!
set v15-compat

# ArchLinux-specific locations of certificates.
# Since these are subject to the ArchLinux update mechanism,
# use only those, don't try to load OpenSSL builtin ones.
# And use the TLS specific set: see "man 8 update-ca-trust"
#set ssl-ca-dir=/etc/ssl/certs
set ssl-ca-file=/etc/ssl/certs/ca-certificates.crt
set ssl-ca-no-defaults

# Don't use protocols older than TLS v1.2.
# Change this only when the remote server doesn't support it:
# maybe use ssl-protocol-HOST (or -USER@HOST) syntax to define
# such explicit exceptions, then, e.g.
#     ssl-protocol-USER@archlinux.org="-ALL,+TLSv1.2"
set ssl-protocol=-ALL,+TLSv1.2

# Explicitly define the list of ciphers, which may improve security,
# especially with protocols older than TLS v1.2\.  See ciphers(1).
# This is an example: in reality it is possibly best to only use
# ssl-cipher-list-HOST (or -USER@HOST), as necessary, again..
set ssl-cipher-list=TLSv1.2:!aNULL:!eNULL:@STRENGTH
#set ssl-cipher-list="ALL:!aNULL:!eNULL:!MEDIUM:!LOW:!MD5:!RC4:!EXPORT"

# Request strict transport security checks
set ssl-verify=strict

# Essential setting: select allowed character sets
# (Have a look at the "Character sets" manual section)
set sendcharsets=utf-8,iso-8859-1

# A very kind option: when replying to a message, first try to
# use the same encoding that the original poster used herself!
set reply-in-same-charset
# When replying to or forwarding a message the comment and name
# parts of email addresses are removed unless this variable is set
set fullnames

# When sending messages, wait until the Mail-Transfer-Agent finishs.
set sendwait

# Only use builtin MIME types, no mime.types(5) files.
# That set is often sufficient, but look at the output of the
# `mimetype' command to ensure this is true for you, too
set mimetypes-load-control

# Default directory where we act in (relative to $HOME if not absolute)
set folder=mail
# A leading "+" (often) means: under folder
# record is used to save copies of sent messages, $DEAD is error storage
# inbox: system mailbox, by default /var/mail/$USER: **file %**
# $MBOX: secondary mailbox: **file &**
set MBOX=+mbox.mbox record=+sent.mbox DEAD=+dead.mbox
set inbox=+system.mbox

# Define some shortcuts; now one may say, e.g., file mymbo
shortcut mymbo %:+mbox.mbox \
         myrec +sent.mbox

# This is optional, but you should get the big picture
# by reading the manual before you leave that off
set from="*Your Name <youremail@domain>*"

# Mailing-list specifics (manual: "Mailing lists"):
set followup-to followup-to-honour=ask-yes reply-to-honour=ask-yes
# And teach some non-subscribed / some subscribed lists, too
mlist @xyz-editor.xyz$ @xyzf.xyz$
mlsubscribe ^xfans@xfans.xyz$

```

## Sending mail with an external SMTP server

To send messages via the built-in SMTP (Simple Mail Transfer Protocol) client to an external SMTP server, several options have to be set or adjusted. Add the following as appropriate to the configuration as above, changing bold strings. Reading the manual section "On URL syntax and credential lookup" is worthwhile.

```
# It can be as easy as
# (Remember **USER** and **PASS** must be URL percent encoded)
set mta=smtp://**USER**:**PASS**@**HOST** \
    smtp-use-starttls

# It may be necessary to set *hostname* and/or *smtp-hostname*
# if the "SERVER" of *smtp* and "domain" of *from* don't match.
# Reading the "ON URL SYNTAX.." and *smtp* manual entries may be worthwhile
set mta=**(smtp[s]/submission)://[USER[:PASS]@]SERVER[:PORT]** \
    smtp-auth=**login[/plain]...** \
    smtp-use-starttls

# E.g. here is a real life example of a very huge free mail provider
# (Activate this account via *mailx -AXooglX* from the command line,
# or use the *? acc[ount] XooglX* command in interactive mode)
account XooglX {
   # Localize options, forget them when changing the account
   localopts yes
   # (The plain smtp:// proto is optional)
   set mta=smtp://**USER:PASS**@smtp.gmXil.com smtp-use-starttls
   set from="**Your Name <youremail@domain>**"
}

# And here is a pretty large one which does not allow sending mails
# if there is a domain name mismatch *on the SMTP protocol level*,
# which would bite us if the value of *from* does not match, e.g.,
# for people who have a sXXXXeforge project and want to speak
# with the mailing list under their project account (in *from*),
# still sending the message through their normal mail provider
account XandeX {
   localopts yes
   set mta=smtps://**USER:PASS**@smtp.yaXXex.ru:465 \
       hostname=yaXXex.com smtp-hostname=
   set from="**Your Name <youremail@domain>**"
}

```

**Tip:** If you have enabled two-step authentication in Gmail, and you have added an application specific password for S-nail, you will want to use that password rather than your regular Gmail password, which may work without enabling the otherwise necessary "less secure apps".

Note that, when storing passwords in `$HOME/.mailrc`, you should set appropriate permissions with `chmod 0600`. You can also set the *netrc-lookup* option and store user credentials in `$HOME/.netrc` (or *$NETRC*) instead; e.g., here is a real life example that sets up SMTP, POP3 as well as IMAP, storing all user credentials in there:

```
account XandeX {
   localopts yes
   set from="Your Name <youremail@domain>"
   wysh set netrc-lookup # netrc-pipe='gpg -qd ~/.netrc.gpg'
   set mta=smtps://smtp.yXXXXx.ru:465 \
       smtp-hostname= hostname=yXXXXx.com
   set pop3-keepalive=240
   shortcut pop pop3s://pop.yXXXXx.ru
   # Type **xp** to login to the POP3 account
   commandalias xp 'fi pop'
   set imap-keepalive=240
   shortcut imap imaps://imap.yXXXXx.ru
   # Type **xi** to login to the IMAP account
   commandalias xi 'fi imap'
 }

```

and, in `$HOME/.netrc`:

```
machine *.yXXXXx.ru login **USER** password **PASS**

```

In this case **USER** and **PASS** are clear text, not URL encoded. You can further diversify things and use encrypted password storage. To adjust the example accordingly, simply encrypt your `~/.netrc` file with OpenPGP and uncomment the `netrc-pipe` statement above. The encrypted storage `~/.netrc.gpg` can be created like this:

```
# gpg -e .netrc
# eval `gpg-agent --daemon --pinentry-program=/usr/bin/pinentry-curses --max-cache-ttl 99999 --default-cache-ttl 99999`

```

Test the configuration (use the *-d* command line option for a dry-run):

```
# echo test-body | mailx -vv -A XandeX -s test-subject **some@where**

```

## Interactive usage

Mailx has a wide-glyph aware command line editor with history capabilities and coloured message display support. Because it strives for POSIX standard compliance some settings have to be adjusted before using it interactively doesn't baffle all descriptions, however. Reading the manual is unavoidable, but add, at a minimum, the following on top of the example configuration:

```
# (The global configuration /etc/mail.rc provides some commented basics;
# in particular it shows all options that POSIX mandates as defaults.)

# Start into interactive mode even if the system mailbox is empty or
# doesn't exist.  mailx will exit immediately without that one
set emptystart

# When composing a message, start directly into *$EDITOR*
set editalong

# Start *$PAGER* when a message is longer than VALUE lines;
# without VALUE: screen *$LINES*
set crt=

# A nicer prompt for a modern terminal
wysh set prompt='?\${?}!\${!}[\${account}#\${mailbox-display}]? '

# Add more entries to the history, and make that persistent
set history-gabby history-file=+.s-nailhist
# When **p**rinting messages, show only these headers
# (Easier to **retain** what you want than to **ignore**
# what you don't; use **P**rint to see all headers and **S**how
# to see the raw message content)
retain date from to cc subject

# Try to get around weird MIME attachment specifications
# (This option can take a value, see the manual for more)
set mime-counter-evidence=0xE

# Display HTML parts inline, nicer than what the builtin viewer can achieve
#set pipe-text/html='@* lynx -stdin -dump -force_html'
# Learn another mimetype
mimetype model/vrml wrl vrml

# Create some new commands so that, e.g., `ls /tmp' will..
commandalias ls !ls -latro
commandalias ps !ps axu

```

Once you're in it use **list** to print all available builtin commands. Typing `?X' tries to expand "X" and print a help string; since mailx allows abbreviations of all commands this is sometimes handy, try, e.g., **?h**, **?he** and **?hel** ... The command **help** will print a short summary of the most frequent used commands, more so if the variable `verbose` is set.

### I'm in!

When starting into interactive mode a summary of the content of the initially opened mailbox is printed, as via the **headers** command. In the header display messages are given numbers (starting at 1) which uniquely identify messages. Messages can be printed with the **print** command, or short: **p**. Whereas **p** honours **retain**ed (or **ignore**d) list of headers to be displayed, the **P**rint command will not and display all headers; the **Sh**ow command will print raw message content.

By default the current message (dot) is printed, but just like with many other commands it is possible to specify lists of messages, as is documented in the manual section "Specifying messages"; e.g., **p:u** will display all unread messages, **p.** will print the dot, **p 1 5** will print the messages 1 and 5 and **p-** and **p+** will print the last and the next message, respectively. Note that simply typing RETURN in an empty line acts like **next** (**n**), and thus prints the next message.

The command **from** is nice for an overview, e.g., **f '@<@arch linux'** will print the header summary of all messages that contain the string "arch linux" in some message header, whereas **f '@arch linux'** will only match those with "arch linux" in their subject; finally, the regular expression **f @^A[^[:space:]]+** finds... That is, be aware that quoting may be necessary when there is whitespace in search expressions etc.

*   **file** and **File** open a new mailbox, the latter in readonly mode
*   **newmail** (dependent on the mailbox, checks for new mail and) prints a listing of new messages
*   **he** (headers) reprints the message list
*   **z-**, **z+**, **z0**, **z$** scroll through the header display (dependent on the terminal you are using the Home/End/PageUp/PageDown keys will be working aliases)
*   **folders** shows a listing of mailboxes under the currently set *folder*
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

Composition is started by typing **mail user@host** or by replying to a message. When you return from *$EDITOR* (assuming *editalong* is set) you'll find yourself in the native editor, where many operations can be performed using tilde escapes (short help available via **~?**). Of particular interest is **~@**, which either allows interactive editing of the attachment list, or, when given arguments, to add a(n) (comma-separated list of) additional attachment(s), as well as """~^""", which is a multiplexer command which offers some control about the message, e.g., to create custom headers.

To send the mail, signal EOT with `Ctrl+d` or type `~.` on its own line.

## Using S/MIME

The manual contains a step-by-step example of how to create your certificates etc. ("Signed and encrypted messages with S/MIME" as well as "S/MIME step by step"). Assuming you have your private key and signed certificate already, just create the paired file we need

```
# cat private-key.pem signed-certificate.pem > ~/pair.pem

```

and setup S-nail via

```
set smime-sign-cert=~/pair.pem \
    smime-sign-message-digest=SHA256 \
    smime-sign

```

From now any message that is sent will be signed. The default message digest would be SHA1, as mandated by RFC 5751. Note that S/MIME always works relative to the setting of the variable *from*, so it seems best to instead place the above settings in an **account**. The **verify** command verifies S/MIME messages, but note that S/MIME decryption and verification is solely based upon OpenSSL for now, which only supports messages with a simplicistic MIME structure. Sorry. By the way, if you miss hyperlinks and a table-of-content to get yourself going, the manual on the projects' website offers this; and the manual that ships with ArchLinux does, too, but needs the mdocmx(7) extension to be visible.

## Workaround missing OpenPGP support

S-nail doesn't yet support OpenPGP. However, using a macro it is possible to at least automatically verify inline *--clearsign*ed messages, and using command ghosts their usage becomes handy: e.g., use the following in resource file and you will be able to verify a clearsigned message by just typing **V**:

```
 define V {
    \localopts yes; \wysh set pipe-text/plain=$'@*#++=@\
       < "${MAILX_FILENAME_TEMPORARY}" awk \
             -v TMPFILE="${MAILX_FILENAME_TEMPORARY}" \'\
          BEGIN{done=0}\
          /^-----BEGIN PGP SIGNED MESSAGE-----/,/^$/ {\
             if(done++ != 0)\
                next;\
             print "--- GPG --verify ---";\
             system("gpg --verify " TMPFILE " 2>&1");\
             print "--- GPG --verify ---";\
             print "";\
             next;\
          }\
          /^-----BEGIN PGP SIGNATURE-----/,/^-----END PGP SIGNATURE-----/ {\
             next;\
          }\
          {print}\
          \*;\*
       print
 }
 define RK {
   !printf 'Key IDs to gpg --recv-keys: ';\
     read keyids;\
     gpg --recv-keys ${keyids};
 }
 commandalias V '\'call V
 commandalias RK '\call RK'

```

## Using an IMAP mailbox

The following is only a quick hint, it is also possible to define *folder* and *inbox* to point to IMAP server folders, for example. Internationalised names are supported.

```
set v15-compat
# or many servers will expire the session
set imap-keepalive=240
set imap-cache=~/.imap_cache

```

```
# You may want to define shortcuts to folders, for example:
shortcut myimap "**imaps://USER:PASS@server:port"**
set inbox=myimap

```