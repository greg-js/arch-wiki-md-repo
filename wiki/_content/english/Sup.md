[Sup](https://sup-heliotrope.github.io/) is a powerful new mail client developed for people who manage lots of mail. It can be viewed as a cross between Mutt and Gmail, with very fast operation and search, tagging, automatic contact management, support for a wide variety of accounts at once, and more.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Filtering mail](#Filtering_mail)
        *   [2.1.1 Local filtering](#Local_filtering)
        *   [2.1.2 Filter serverside](#Filter_serverside)
    *   [2.2 sup sources](#sup_sources)
    *   [2.3 sup hooks](#sup_hooks)
        *   [2.3.1 before-poll hook](#before-poll_hook)
    *   [2.4 Viewing HTML attachments](#Viewing_HTML_attachments)
    *   [2.5 Viewing non-text attachments](#Viewing_non-text_attachments)
*   [3 Usage](#Usage)
*   [4 Back-up and Restore](#Back-up_and_Restore)
*   [5 See also](#See_also)

## Installation

Sup only works with [Ruby](/index.php/Ruby "Ruby") 2.3.3\. Arch moved to a newer Ruby which makes sup crash. Sup is at the moment not being actively maintained to keep up with new versions of Ruby.

You can temporarily install sup using this workaround using [RVM](/index.php/RVM "RVM"). After installing RVM, do the following (this follows the solution given [here](https://github.com/sup-heliotrope/sup/issues/532#issuecomment-274184299))

Install Ruby 2.3.3 with RVM:

```
$ rvm install 2.3.3

```

Switch to this version and install `xapian-ruby` and `sup`:

```
$ rvm 2.3.3 do gem install xapian-ruby
$ rvm 2.3.3 do gem install sup

```

Run `sup` with `rvm 2.3.3 do sup`. It is recommended to add an alias of this to your `.bashrc` or `zshrc`:

```
$ alias sup='rvm 2.3.3 do sup'

```

## Configuration

Sup comes with an easy to use configuration tool called `sup-config`. To use it, start it in the console and walk through the steps, which are as follows:

1.  Enter your full name.
2.  Enter your primary e-mail address, as well as any alternate e-mail addresses.
3.  Enter the path to your signature file, if you have one.
4.  Enter the editor that should be used to compose new mail, as well as any arguments that should be passed to it.
5.  Add sources for your mail, including:
    1.  mbox files
    2.  maildir directories

Support for remote sources (POP3, IMAP, IMAPS, and mbox+ssh) was removed in the 0.12 release.

Sup is for the most part only an MUA (mail user agent) and cannot handle downloading mail on its own. You can use tools like offlineimap, fetchmail, and rsync to transfer email to the local system mbox or maildir folders.

The [sup wiki has an example](https://github.com/sup-heliotrope/sup/wiki/Complete-gmail-configuration) for configuring a gmail+imap source using offlineimap. The [Mutt#POP3](/index.php/Mutt#POP3 "Mutt") subsection shows some additional mail transfer methods.

After the email sources have been added, `sup-config` will execute the `sup-sync` command to import mail into your mailbox.

### Filtering mail

sup works by having all relevant mail in one view at a time and no folders. To control exactly what is viewed and what is not mail needs filtering.

There are many ways to filter mail. Depending on how you access your mail you might want to filter on the serverside (with e.g. [imapfilter](https://aur.archlinux.org/packages/imapfilter/) or on the clientside.

To decide which way to go consider these two scenarios:

*   you always check mail on the same computer using sup -> go for local filtering
*   you want to be able to read your (uncluttered) email (through webmail) when using other computers -> filter on the server

#### Local filtering

The sup hook [before-add-message.rb](https://github.com/sup-heliotrope/sup/wiki/Auto-Add-Labels-To-New-Messages) enables you with a little ruby knowledge to filter your mail and applying *labels*, *archive*, *mark read* etc. to mail easily.

#### Filter serverside

Sup only hides from view so to keep the serverside clean you have to resort to another tool. [imapfilter](https://aur.archlinux.org/packages/imapfilter/) is a popular mailfilter. Set it up starting from the [example.config](https://github.com/lefcha/imapfilter/blob/master/samples/config.lua).

**Tip:** Some servers impose **quotas** and to keep within it you can use [archivemail](https://aur.archlinux.org/packages/archivemail/) to clear the server from old mail.

### sup sources

Sup uses the file `~/.sup/sources.yaml` to get sync your mail with its index and supports adding one or more labels to all mail from a source.

```
--- 
- !supmua.org,2006-10-01/Redwood/Maildir 
  uri: maildir:/home/User/Mail/Inbox
  usual: true
  archived: false
  id: 1
  labels: []
- !supmua.org,2006-10-01/Redwood/Maildir 
  uri: maildir:/home/User/Mail/Pulse
  usual: true
  archived: true
  id: 2
  labels:
  - pulse
  - cruft
```

As seen in the example the *Pulse* folder has 2 labels: *pulse* and *cruft*. All the mail from Pulse is archived on import and hidden from view avoiding a cluttered screen. See the [sup wiki](https://github.com/sup-heliotrope/sup/wiki/Adding-sources) for details on labels and ids.

**Warning:** The source-statements need to have unique ids to work properly.

### sup hooks

sup has to types of hooks: interactive and non-interactive to enable the user to easily customize the program. See details in the [sup wiki on hooks](https://github.com/sup-heliotrope/sup/wiki/Hooks) for details.

#### before-poll hook

To activate the filtering and syncing automatically we set up a non-interactive startup hook using **before-poll**:

```
 File: ~/.sup/hooks/before-poll.rb
 Executes immediately before a poll for new messages commences.
 No variables.

```

Here is a simple example (without filtering)

```
 say "Running offlineimap..."
 system "offlineimap", "-o", "-u", "quiet"

```

Here is a simple example (with filtering)

```
 say "Running imapfilter..."
 system "imapfilter", "-c", "path-to-config.lua"
 say "Running offlineimap..."
 system "offlineimap", "-o", "-u", "quiet"

```

Now running sup will start filtering and then synching mail when sup starts or whenever you poll mail manually. See details in the [sup wiki on before-poll](https://github.com/sup-heliotrope/sup/wiki/Triggering-mail-collection)

### Viewing HTML attachments

create `~/.sup/hooks/mime-decode.rb` with

```
   require 'shellwords'
   unless sibling_types.member? "text/plain"
     case content_type
     when "text/html"
       `/usr/bin/w3m -dump -T #{content_type} #{Shellwords.escape filename}`
     end
   end

```

Or

```
    require 'shellwords'
    unless sibling_types.member? "text/plain"
      case content_type
      when "text/html"
	`/usr/bin/links -dump #{Shellwords.escape filename}`
      end
    end
```

Note the difference in program executed. See details on [the sup wiki](https://github.com/sup-heliotrope/sup/wiki/Viewing-Attachments#decoding-attachments)

### Viewing non-text attachments

**Note:** Install [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) to use xdg-open

create `~/.sup/hooks/mime-view.rb` with

```
# filename has already been shellesacped
  pid = Process.spawn("xdg-open", filename,
                    :out => '/dev/null',
                    :err => '/dev/null')

  Process.detach pid

  true
```

See details on [the sup wiki](https://github.com/sup-heliotrope/sup/wiki/Viewing-Attachments)

## Usage

Execute the `sup` command to start the Sup mail client. The program should show the messages imported by `sup-config`.

The most important key for new users to remember is the `?` key. This will display a full list of keyboard commands at any point, reminding new users how to navigate the program.

To navigate between threads, use the arrow keys or the `j` and `k` keys (`Shift+j` and `Shift+k` work like the Page Up and Page Down keys). To jump between threads with new messages, press the Tab key. Sup doesn't load all threads by default; press `Shift+m` to load more (more messages will automatically load to fill the window).

To view a thread, select it and press the `Enter` key. To expand or collapse an individual message while viewing a thread, select the message and press the `Enter` key. Press `Shift+n` to expand only new messages (the default view) or `Shift+e` to toggle the state of all messages. Press `o` to show or hide hidden parts of a message (such as signatures).

To navigate between messages in a thread, press the `n` and `p` keys. To display the headers on a message, press the `h` key.

To cycle through buffers, press the `b` key, or press the `;` key to view a list of all of the open buffers. To kill a buffer, press the `x` key.

To archive a thread, press the `a` key. This will hide it from the inbox until someone replies to it, at which point it will reappear. To kill a thread, press the `&` key. This is equivalent to Gmail's "mute" function, which hides a message even if people reply to it. It will never re-appear in the inbox, but it will still show up in search results.

To star a thread, press the `*` key. To mark a thread as spam, press the `Shift+s` key. Sup doesn't have any built-in spam filter; for that, consider a program such as [spamassassin](https://www.archlinux.org/packages/?name=spamassassin).

To tag a thread, press the `t` key. To label the messages in a thread, press the `l` key. To search labels, press the `Shift+l` key. `Enter` a label for which to search or press the `Enter` key to call up a list of labels. To perform a full text search, press the `\` key.

To view a list of contacts, press the `Shift+c` key. To e-mail one of the people on the list, select his or her name and press the `Enter` key.

## Back-up and Restore

Backing-up e-mail is very important. To ensure that you do not lose anything, first back up the sources, such as mbox files and maildir directories, then run:

```
$ sup-dump > *filename*

```

This will back-up all message states in a text file. To restore your message states from this text file, simply run:

```
$ sup-sync [<source>+] --restored --restore *filename*

```

Just remember that the commands above only back-up and restore message states. The messages themselves will need to be backed-up separately.

## See also

*   [Website](https://sup-heliotrope.github.io/)
*   [Wiki](https://github.com/sup-heliotrope/sup/wiki)
*   [README](https://github.com/sup-heliotrope/sup/blob/develop/README.md)
*   [FAQ](https://github.com/sup-heliotrope/sup/blob/develop/doc/FAQ.txt)
*   [Philosophical statement](https://github.com/sup-heliotrope/sup/blob/develop/doc/Philosophy.txt)