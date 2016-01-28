# Ttytter

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Needs heavy wikification, use of formal language, compliance with [Help:Style](/index.php/Help:Style "Help:Style"). (Discuss in [Talk:Ttytter#](https://wiki.archlinux.org/index.php/Talk:Ttytter))

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [List of Applications](/index.php/List_of_Applications "List of Applications").**

**Notes:** There is already a ttytter entry in the list with a link to the official website, this article doesn't seem to add any useful content. See also [Help:Style#Hypertext metaphor](/index.php/Help:Style#Hypertext_metaphor "Help:Style"). (Discuss in [Talk:Ttytter#](https://wiki.archlinux.org/index.php/Talk:Ttytter))

**ttytter** Not another Twitter client! Yes, another Twitter client. The difference here is that you're dealing with a multi-functional, fully 100% text, Perl command line client.

tytter is a twitter client for the command line

[ttytter](https://www.archlinux.org/packages/?name=ttytter)

When you start TTYtter without a keyfile, which will be the case the first time you run it, it will automatically

start an assistant to help you create the keyfile. You only need to create the keyfile once for each account. It will never expire.

TTYtter will find where your cURL is located, and if successful, you should see something like this:

[ttyter launch image](http://postimg.org/image/fthxntgv3/)

Once installed simply type

```
ttytter -dostream

```

into your command line and it will prompt you for the Oauth key, click the given URL

and type in the key which appears in your browser.

Now you should see your twitter timeline in the shell.

Note: If you use this screen name on other machines you use TTYtter on, simply copy the keyfile there

To enable ANSI colours and some other features here is a template .ttytterrc which should suffice for most users

[.ttytterrc](http://paste.debian.net/147463/) create this file in your home dir and restart ttytter to see the differences.

For a more indepth look at ttytter & its commands see the [ttytter homepage](http://www.floodgap.com/software/ttytter/#bt)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Ttytter&oldid=360642](https://wiki.archlinux.org/index.php?title=Ttytter&oldid=360642)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")

Hidden categories:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")
*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")