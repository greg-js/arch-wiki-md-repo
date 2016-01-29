# Help:Style

Related articles

*   [Help:Style/Formatting and punctuation](/index.php/Help:Style/Formatting_and_punctuation "Help:Style/Formatting and punctuation")
*   [Help:Style/White space](/index.php/Help:Style/White_space "Help:Style/White space")
*   [Help:Editing](/index.php/Help:Editing "Help:Editing")
*   [Help:Reading](/index.php/Help:Reading "Help:Reading")
*   [Help:Discussion](/index.php/Help:Discussion "Help:Discussion")
*   [Help:Template](/index.php/Help:Template "Help:Template")

These style conventions encourage tidy, organized, and visually consistent articles. Follow them as closely as possible when editing the ArchWiki.

## Contents

*   [1 Article pages](#Article_pages)
    *   [1.1 Title](#Title)
    *   [1.2 Layout](#Layout)
    *   [1.3 Magic words](#Magic_words)
    *   [1.4 Categories](#Categories)
    *   [1.5 Interlanguage links](#Interlanguage_links)
    *   [1.6 Article status templates](#Article_status_templates)
    *   [1.7 Related articles box](#Related_articles_box)
    *   [1.8 Preface or introduction](#Preface_or_introduction)
    *   [1.9 Section headings](#Section_headings)
    *   [1.10 Code formatting](#Code_formatting)
    *   [1.11 Command line text](#Command_line_text)
    *   [1.12 File editing requests](#File_editing_requests)
    *   [1.13 Keyboard keys](#Keyboard_keys)
    *   [1.14 Package management instructions](#Package_management_instructions)
        *   [1.14.1 Official packages](#Official_packages)
        *   [1.14.2 AUR packages](#AUR_packages)
        *   [1.14.3 Unofficial repositories](#Unofficial_repositories)
    *   [1.15 systemd units operations](#systemd_units_operations)
    *   [1.16 Notes, Warnings, Tips](#Notes.2C_Warnings.2C_Tips)
    *   [1.17 Shells](#Shells)
    *   [1.18 Hypertext metaphor](#Hypertext_metaphor)
    *   [1.19 Coding style](#Coding_style)
    *   [1.20 Supported kernel versions](#Supported_kernel_versions)
    *   [1.21 "Tips and tricks" sections](#.22Tips_and_tricks.22_sections)
    *   [1.22 "Troubleshooting" sections](#.22Troubleshooting.22_sections)
    *   [1.23 "Known issues" sections](#.22Known_issues.22_sections)
    *   [1.24 "See also" sections](#.22See_also.22_sections)
    *   [1.25 Non-pertinent content](#Non-pertinent_content)
    *   [1.26 Language register](#Language_register)
*   [2 Category pages](#Category_pages)
*   [3 Redirect pages](#Redirect_pages)
*   [4 User pages](#User_pages)
*   [5 Generic rules](#Generic_rules)
    *   [5.1 Edit summary](#Edit_summary)
    *   [5.2 HTML tags](#HTML_tags)

## Article pages

### Title

*   Titles should use [sentence case](https://en.wikipedia.org/wiki/Letter_case#Usage "wikipedia:Letter case"), e.g. "Title for new page" is correct, while "Title for New Page" is not. Note that common words that are part of a proper name or an upper-case acronym must be capitalized, e.g. "Advanced Linux Sound Architecture", not "Advanced Linux sound architecture".
    Namespaces are not considered part of titles, so "ArchWiki:Example article" is correct, while "ArchWiki:example article" is not. Subpage names should start with a capital letter, so "My page/My subpage" is correct, while "My page/my subpage" is not.
*   By default, the topic name in titles should be in the singular form; it should be in the plural form if it represents a group or class of something and is a countable noun or perceived as such.
*   If the subject of the article is commonly known both with the full name and the acronym, prefer using the full name in the title of the article. Do not include both the full name and the acronym (e.g. in parentheses) in the title, but rather use a [redirect](/index.php/Help:Editing#Redirects "Help:Editing") on the acronym page that points to the page titled with the full name.
*   See the [Help:Article naming guidelines](/index.php/Help:Article_naming_guidelines "Help:Article naming guidelines") article for more information.

### Layout

*   Order elements in an article as follows:

1.  [#Magic words](#Magic_words) (optional)
2.  [#Categories](#Categories)
3.  [#Interlanguage links](#Interlanguage_links)
4.  [#Article status templates](#Article_status_templates) (optional)
5.  [#Related articles box](#Related_articles_box) (optional)
6.  [#Preface or introduction](#Preface_or_introduction)
7.  Table of contents (automatic)
8.  Article-specific sections

### Magic words

*   Behavior switches — and in general, all of the [magic words](https://www.mediawiki.org/wiki/Help:Magic_words "mw:Help:Magic words") that change how an article is displayed or behaves but do not add content by themselves — should all go at the very top of articles.
    This rule applies in particular to `{{DISPLAYTITLE:title}}` and [Template:Lowercase title](/index.php/Template:Lowercase_title "Template:Lowercase title"), which makes use of the former.

### Categories

*   Every article must be categorized under at least one existing category.
*   An article can belong to more than one category, provided one is not ancestor of the others.
*   Categories must be included at the top of every article, right below any magic words.

    **Note:** This is different from some other MediaWiki projects such as Wikipedia, which include categories at the bottom.

*   There should be no blank lines between categories and the first line of text (or interlanguage links, if present), because this introduces extra space at the top of the article.
*   See the [Help:Category](/index.php/Help:Category "Help:Category") article for more information.

### Interlanguage links

*   If the article has translations in the local or an external Arch Linux wiki, interlanguage links must be included right below the categories and above the first line of text.
    Note that they will actually appear in the appropriate column to the left side of the page.
*   There should be no blank lines between interlanguage links and the first line of text, because this introduces extra space at the top of the article.
*   When adding or editing interlanguage links you should take care of repeating your action for all the already existing translations.
*   Do not add more than one interlanguage link for each language to an article.
*   Do not add interlanguage links for the same language of the article.
*   The interlanguage links must be sorted alphabetically based on the language tag, not the local name, so for example `[[fi:Title]]` comes before `[[fr:Title]]` even though "Suomi" would come after "Français".
*   See the [Help:i18n](/index.php/Help:I18n "Help:I18n") and [Wikipedia:Help:Interlanguage links](https://en.wikipedia.org/wiki/Help:Interlanguage_links "wikipedia:Help:Interlanguage links") articles for more information.

### Article status templates

*   [Article status templates](/index.php/Help:Template#Article_status_templates "Help:Template") can be included right below the categories (or interlanguage links, if present) and right above the introduction (or the Related articles box, if present).
*   Article status templates can also be used inside article sections, when appropriate.
*   Always accompany an article status template with some words of explanation in the dedicated field (examples are provided in each template's page), possibly even opening a discussion in the talk page.

### Related articles box

*   Provides a simple list of related internal articles.
*   Optionally included right below categories (or interlanguage links, or Article status templates, if present).
*   It can only be made of [Template:Related articles start](/index.php/Template:Related_articles_start "Template:Related articles start"), [Template:Related](/index.php/Template:Related "Template:Related") and [Template:Related articles end](/index.php/Template:Related_articles_end "Template:Related articles end"). See also the guidelines in those pages.
*   Non-English articles can make use of [Template:Related2](/index.php/Template:Related2 "Template:Related2") for translating the anchor text.
*   Use the ["See also" section](#.22See_also.22_sections) for a more complete and detailed list that also includes link descriptions and interwiki or external links.

### Preface or introduction

*   Describes the topic of the article.
    Rather than paraphrasing or writing your own (possibly biased) description of a piece of software, you can use the upstream author's description, which can usually be found on the project's home page or about page, if it exists. An example is [MediaTomb](/index.php/MediaTomb "MediaTomb").
*   Included right above the first section of the article.
*   Do not explicitly make an `==Introduction==` or `==Preface==` section: let it appear above the first section heading. A table of contents is shown automatically between the preface and first section when there are sufficient sections in the article.
*   See [Help:Writing article introductions](/index.php/Help:Writing_article_introductions "Help:Writing article introductions") for more information.

### Section headings

*   Headings should start from level 2 (`==`), because level 1 is reserved for article titles.
*   Do not skip levels when making subsections, so a subsection of a level 2 needs a level 3 heading and so on.
*   Headings use sentence case; _not_ title case: _My new heading_; not _My New Heading_.
*   Avoid using links in headings because they break style consistency and do not stand out well enough. Usually the anchor text is also found in the section content, otherwise you can use a simple sentence like:

NaN

*   See the [Help:Effective use of headers](/index.php/Help:Effective_use_of_headers "Help:Effective use of headers") articles for more information.

### Code formatting

*   Use `{{ic|code}}` for short lines of code, file names, command names, variable names and the like to be represented inline, for example:
    Run `sh ./hello_world.sh` in the console.

*   For single lines of code (command line input or output code and file content) to be represented in a proper frame, simply start them with a single space character, see also [Help:Editing#Code](/index.php/Help:Editing#Code "Help:Editing"). For example:

```
$ sh ./hello_world.sh

```

```
Hello World

```

*   Use `{{bc|code}}` for multiple lines of code (command line input or output code and file content) to be represented in a proper frame, for example:

```
#!/bin/sh

# Demo
echo "Hello World"
```

*   Use `{{hc|input|output}}` when in the need of representing both command line input and output, for example:

 `$ sh ./hello_world.sh`  `Hello World` 

*   When you need to represent file content and you feel it may be difficult for readers to understand which file that code refers to, you can also use `{{hc|filename|content}}` to show the file name in the heading, for example:

 `~/hello_world.sh` 

```
#!/bin/sh

# Demo
echo "Hello World"
```

*   For blocks of code such as a configuration file, consider focusing the reader to the relevant lines and ellipsing (`...`) any surrounding, non-relevant content.

*   See the [Help:Template](/index.php/Help:Template "Help:Template") article for more information and for troubleshooting problems with template-breaking characters like `=` or `|`.

### Command line text

*   When using inline code ([Template:ic](/index.php/Template:Ic "Template:Ic")), no prompt symbol is to be represented, but any notes about permissions must be added explicitly to the surrounding text.
*   When using block code ([Template:bc](/index.php/Template:Bc "Template:Bc") or lines starting with a space character), use `$` as a prompt for regular user commands; use `#` as a prompt for root commands.

    **Note:** Because `#` is also used to denote comments in text files, you should always make sure to avoid ambiguities, usually by explicitly writing to run the command or edit a text file.

    *   The sentence introducing a command block should usually end with `:`.
    *   Unless really necessary, prefer using: `# _command_` instead of writing: `$ sudo _command_` 
    *   Do not use the root prompt and the _sudo_ command together, like in: `# sudo _command_` The only exception is when _sudo_ is used with the `-u` flag: in this case the prompt can match the others of the same code block, or default to `$`.
    *   Do not add comments in the same box of a command, for example: `# pacman -S foo  #Install package foo` 
    *   Avoid writing excessively long lines of code: use line-breaking techniques when possible.
*   Do not assume the user uses [sudo](/index.php/Sudo "Sudo") or other privilege escalation utilities (e.g. _gksu_, _kdesu_).

### File editing requests

*   Do not assume a specific text editor (_nano_, _vim_, _emacs_, etc.) when requesting text file edits, except when necessary.
*   Do not use implicit commands to request text file edits, unless strictly necessary. For example, `$ echo -e "clear\nreset" >> ~/.bash_logout` should be:

NaN

### Keyboard keys

*   The standard way to represent keyboard keys in articles is using instances of [Template:ic](/index.php/Template:Ic "Template:Ic").
*   Letter keys should be represented in lower case: `a`. To represent upper-case letters, use `Shift+a` instead of `Shift+A` or `A`.
*   The correct way to represent key _combinations_ makes use of the `+` symbol to join keys, with no additional spaces around it, in a single instance of the template: `Ctrl+c`.
    `Ctrl + c`, `Ctrl`+`c`, `Ctrl-c` are non-compliant forms, and should be avoided.
*   The correct way to represent key _sequences_ is either verbose, e.g. "press `g` followed by `Shift+t`", or concise, separating the keys with a single space in different instances of the template: `g` `Shift+t`.
*   The following are the standard ways of representing some special keys:
    *   `Shift` (not `SHIFT`)
    *   `Ctrl` (not `CTRL` or `Control`)
    *   `Alt` (not `ALT`)
    *   `Super` (not `Windows` or `Mod`)
    *   `Enter` (not `ENTER` or `Return`)
    *   `Esc` (not `ESC` or `Escape`)
    *   `Space` (not `SPACE`)
    *   `Backspace`
    *   `Tab`
    *   `Ins` (not `INS` or `Insert`)
    *   `Del` (not `DEL` or `Delete`)
    *   `PrintScreen`
    *   `PageUp`
    *   `PageDown`

### Package management instructions

#### Official packages

*   Please avoid using examples of _pacman_ commands in order to give instructions for the installation of official packages: this has been established both for simplicity's sake (every Arch user should know [pacman](/index.php/Pacman "Pacman")'s article by memory) and to avoid errors such as `pacman -Sy package` or possibly never-ending discussions like the choice between `pacman -S package` and `pacman -Syu package`. All the more reason you should not suggest the use of _pacman_ frontends or wrappers.

NaN

*   Links to the referenced packages are mandatory and should be created using [Template:Pkg](/index.php/Template:Pkg "Template:Pkg"), for example `{{Pkg|foobar}}`.

NaN

*   The above examples also make use of a link to [install](/index.php/Install "Install") (e.g. `[[install]]`): this is recommended to be used at least on the first occurrence of an installation request, especially in articles that are more likely to be visited by Arch novices.
*   Examples of _pacman_ commands are nonetheless accepted and even recommended in the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide").
*   If the package is hosted in the _core_, _extra_, or _community_ repositories, do not make reference to the repository, thus facilitating maintenance because it is not uncommon for a package to be moved to a different repository. If however the package is hosted in an official repository which is not enabled by default (_multilib_, _testing_, etc.), mentioning it is required, using a wording like:

NaN

#### AUR packages

*   Please avoid using examples of how to install AUR packages, neither with the official method nor mentioning AUR helpers: every user who installs unofficial packages should have read the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") article, and be aware of all the possible consequences on his system.

NaN

*   Links to the referenced packages are mandatory and should be created using [Template:AUR](/index.php/Template:AUR "Template:AUR"), for example `{{AUR|foobar}}`.

#### Unofficial repositories

*   When suggesting to use an unofficial repository for installing a pre-built package, do not provide instructions for enabling the repository, but make sure such repository is included in [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") and then simply link to it. Also, just like with [official packages](#Official_packages), do not add examples of _pacman_ commands. For example:

NaN

*   The link to [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") is mandatory and should point to the relevant repository section, for example `[[Unofficial user repositories#example|example]]`.

### systemd units operations

*   Do not give examples of how to enable, start, or perform any other basic operations with _systemctl_ on [systemd](/index.php/Systemd "Systemd") units. Instead, use a simple sentence listing the units involved, possibly remarking dependencies or conflicts with other units, and a description of the actions to be performed. For example:

NaN

*   Make sure to link to the [systemd#Using units](/index.php/Systemd#Using_units "Systemd") article section, either directly or through a dedicated [redirect](https://wiki.archlinux.org/index.php?title=Special:WhatLinksHere/Systemd&hidelinks=1&hidetrans=1) like `[[start]]`, `[[enable]]` or `[[stop]]`.
*   Examples of _systemctl_ commands are nonetheless accepted and even recommended in the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide").

### Notes, Warnings, Tips

*   A [Note](/index.php/Template:Note "Template:Note") should be used for information that somehow diverges from what the user would naturally expect at some point in the article. This includes also information that gives more in-depth knowledge on something in particular that otherwise would be considered a bit extraneous to the article. Another example is when needing to point out a temporary announcement like a change in the name of a package.

NaN

*   A [Warning](/index.php/Template:Warning "Template:Warning") should be used where the described procedure could carry severe consequences such as being reasonably difficult to undo or resulting in damage to the system. Warnings should generally indicate both the worst case scenarios as well as the conditions that could lead to or avoid such worst cases.

NaN

*   A [Tip](/index.php/Template:Tip "Template:Tip") should indicate a method or procedure that could be useful and bring benefits to somebody, albeit not needed to complete the operation being dealt with, and therefore safely ignorable.
*   When two or more notes, warnings or tips have to appear one after each other at the same point of an article, prefer grouping their texts in a list inside a single template, avoiding stacking the templates unless they are completely unrelated. For example:

NaN

### Shells

*   Do not assume a particular shell as the user's shell (e.g. Bash), except when really needed: try to be as shell-neutral as possible when writing or editing articles.

### Hypertext metaphor

*   Try to interlink your article with as many others as you can, using the various keywords in the text.
*   Only link to a new article after creating it. In general, do not create links to non-existent articles.
*   For technical terms, such as [system call](https://en.wikipedia.org/wiki/system_call "wikipedia:system call"), not covered by an article in the ArchWiki, link to the relevant Wikipedia page.
*   When linking to other articles of the wiki, do not use full URLs; take advantage of the special syntax for internal links: `[[Wiki Article]]`. This will also let the wiki engine keep track of the internal links, hence facilitating maintenance.
    See [Help:Editing#Links](/index.php/Help:Editing#Links "Help:Editing") for in-depth information and more advanced uses of interwiki links syntax.
*   Avoid implicit links whenever possible. For example, prefer instructions like "See the [systemd](/index.php/Systemd "Systemd") article for more information" instead of "See [here](/index.php/Systemd "Systemd") for more information".
*   Except in rare cases, you should not leave an article as a dead-end page (an article that does not link to any other) or an orphan page (an article that is not linked to from any other).
*   Before writing a specific procedure in an article or describing something in particular, always check if there is already an article that treats that part in detail: in that case, link that article instead of duplicating its content.
*   If the upstream documentation for the subject of your article is well-written and maintained, prefer just writing Arch-specific adaptations and linking to the official documentation for general information.
*   Do not use interwiki links for links to localized pages of the same language of the article being edited because they will not be shown in [Special:WhatLinksHere](/index.php/Special:WhatLinksHere "Special:WhatLinksHere") pages. For example, using `[[:hu:Main page]]` in a Hungarian article is wrong, while `[[Main page (Magyar)]]` is correct.
    Using this kind of links between different languages is instead acceptable because this would make it easier to move the articles to a separate wiki in case a separate wiki is created in the future.
    Finally, note the difference of this kind of links from [#Interlanguage links](#Interlanguage_links), which do not have the colon at the beginning.

### Coding style

*   When adding commands or scripts, use a consistent coding style throughout the article, possibly also referring to the other articles, especially if there are any related ones. If available, respect the official or most common coding style guidelines for the language.
*   Avoid deprecated features of the programming/scripting language you are using: for example, use the `$()` syntax for shell command substitution instead of the backticks/grave (````) syntax.

### Supported kernel versions

*   Do not remove any notes or adaptations regarding kernel versions greater than or equal to the minimum version between the current [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) package in the _core_ repository and the kernel on the latest [installation media](https://www.archlinux.org/download/).

### "Tips and tricks" sections

*   _Tips and tricks_ sections provide advanced tips or examples of using the software.
*   Use the standard title of _Tips and tricks_.
*   The various tips and tricks should be organized in subsections.

### "Troubleshooting" sections

*   _Troubleshooting_ sections are used for frequently asked questions regarding the software or for solutions to common problems (compare to [#"Known issues" sections](#.22Known_issues.22_sections)).
*   Use the standard title of _Troubleshooting_. Common misspellings that should be avoided are _Trouble shooting_, _Trouble-shooting_, and _TroubleShooting_.
*   You can also report temporary workarounds for known bugs, but in this case, it is very desirable that you provide a link to the bug report. In case it has not been reported yet, you should report it yourself, thus increasing the chances that the bug will be properly fixed.
    There are great benefits in linking to a bug report both for readers and editors:
    *   For readers, the Wiki does not become a stopping point: they can find more information close to the source that may have otherwise been missed by their search efforts.
    *   For Wiki editors, it makes cleanup easier by reducing the effort involved in researching whether the reported bug is still an issue; this can even lead to greater autonomy if the reader finds new information and comes back to edit the wiki.

### "Known issues" sections

*   _Known issues_ sections are used for known bugs or usage problems which do not have a solution yet (compare to [#"Troubleshooting" sections](#.22Troubleshooting.22_sections)).
*   Use the standard title of _Known issues_.
*   If a bug report exists for the known issue, it is very desirable that you provide a link to it; otherwise, if it does not exist, you should report it yourself, thus increasing the chances that the bug will be fixed.

### "See also" sections

*   _See also_ sections contain a list of links to references and sources of additional information.
*   This should be a list where each entry is started with `*`, which creates a MediaWiki bulleted list.
*   Use the standard title of _See also_. Other similar titles such as _External links_, _More resources_, etc. should be avoided.

### Non-pertinent content

*   Please do not sign articles, nor credit article authors: the ArchWiki is a work of the community, and the history of each article is enough for crediting its contributors.
    Reporting the sources used to write an article, though, is good practice: you can use the "See also" section for this purpose.
*   Uploading files is disabled for normal users, and including the existing images in articles is not allowed. As an alternative you can include links to external images or galleries, and if you need to draw simple diagrams you may use an ASCII editor like [Asciiflow](http://www.asciiflow.com/). Rationale:
    *   Maintenance: Arch is rolling release, and images would make updating articles much more difficult.
    *   Necessity: Arch does not develop nor maintain any sort of GUI application, so we do not need to display any screenshot.
    *   Moderation: free image upload would require time to be spent removing oversized or inappropriate images.
    *   Accessibility: we support users with slow connections, text-only browsers, screen readers and the like.
    *   Efficiency: images waste server bandwidth and storage space.
    *   Simplicity: text-only articles just look simpler and tidier.

### Language register

*   Articles should be written using formal, professional, and concise language. Care should be taken to remove grammar and orthography errors through edit previews and proofreading.
*   Remember not only to answer _how_, but also _why_. Explanatory information always goes further toward imparting knowledge than does instruction alone.
*   Avoid contractions: "don't", "isn't", "you've", etc. should be "do not", "is not", and "you have", for example.
*   Avoid unnecessary [shortening](https://en.wikipedia.org/wiki/Shortening_(grammar) "wikipedia:Shortening (grammar)") of words: for example, instead of "repo", "distro", and "config", prefer "repository", "distribution", and "configuration".
    In the same fashion, prefer using the long form of _uncommon_ command options instead of their single-character counterpart.
*   Do not omit terms that are necessary to give an exact, unambiguous meaning to a sentence. For example, always add the word "repository" when mentioning the name of a repository.
*   Do not use indefinite time references such as "currently", "at the time of writing" or "soon"; replace them with definite expressions such as "as of May 2015" etc.
*   Write objectively: do not include personal comments on articles; use discussion pages for this purpose. In general, do not write in first person.

## Category pages

*   Every category must be appropriately categorized under at least one parent category, except for root categories, which are [Category:DeveloperWiki](/index.php/Category:DeveloperWiki "Category:DeveloperWiki"), [Category:Languages](/index.php/Category:Languages "Category:Languages"), [Category:Maintenance](/index.php/Category:Maintenance "Category:Maintenance") and [Category:Sandbox](/index.php/Category:Sandbox "Category:Sandbox").
*   A category can be categorized under more than one category, provided one is not ancestor of the others.
*   Avoid circular relationships: two categories cannot be reciprocal ancestors.
*   Do not categorize a category under itself (self-categorized category).
*   Categories must be included at the top of the category page.
*   Categories should not redirect, except temporarily during [renaming](/index.php/Help:Procedures#Rename_a_category "Help:Procedures").
*   By default, category names should be in the singular form ("topic" categories); they should be in the plural form if the singular form can be used to describe _one_ of its members ("set" categories).

## Redirect pages

*   Redirect pages should contain only the redirect code and nothing else. In rare cases, they can also contain a flag such as [Template:Deletion](/index.php/Template:Deletion "Template:Deletion").
*   Redirect only to internal articles; do not use interwiki redirections.

NaN

## User pages

*   Pages in the [User](https://wiki.archlinux.org/index.php?title=Special%3APrefixIndex&prefix=&namespace=2) namespace cannot be categorized.
*   Pages in the [User](https://wiki.archlinux.org/index.php?title=Special%3APrefixIndex&prefix=&namespace=2) namespace can only be linked from other pages in the _User_ or _talk_ namespaces, unless authorization to do otherwise is given by Administrators.

## Generic rules

### Edit summary

See [ArchWiki:Contributing#The 3 fundamental rules](/index.php/ArchWiki:Contributing#The_3_fundamental_rules "ArchWiki:Contributing").

### HTML tags

*   Usage of HTML tags is generally discouraged: always prefer using wiki markup or templates when possible, see [Help:Editing](/index.php/Help:Editing "Help:Editing") and related.
*   When tempted to use `<pre>code</pre>`, always resort to `{{bc|code}}`. When tempted to use `<tt>text</tt>` or `<code>text</code>`, always resort to `{{ic|text}}`.
*   Especially avoid HTML comments (`<!-- comment -->`): it is likely that a note added in a HTML comment can be explicitly shown in the article's discussion page.
    You can add an appropriate [Article status template](/index.php/Help:Template#Article_status_templates "Help:Template") in place of the comment.
*   Use `<br>` only when necessary: to start a new paragraph or break a line, put a blank line below it.
    Common exceptions to this rule are when it is necessary to break a line in a list item and you cannot use a sub-item, or inside a template and you cannot use a list.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Help:Style&oldid=410008](https://wiki.archlinux.org/index.php?title=Help:Style&oldid=410008)"