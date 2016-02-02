# Help:Template

A template is a piece of predefined [wikitext](https://en.wikipedia.org/wiki/Wikitext "wikipedia:Wikitext") that can be inserted into an article. Templates are primarily used to aid in formatting content.

## Contents

*   [1 Usage](#Usage)
    *   [1.1 Style](#Style)
    *   [1.2 Escape template-breaking characters](#Escape_template-breaking_characters)
        *   [1.2.1 Named parameters](#Named_parameters)
        *   [1.2.2 nowiki tags](#nowiki_tags)
        *   [1.2.3 HTML entities](#HTML_entities)
*   [2 Creation](#Creation)
*   [3 List of templates](#List_of_templates)
    *   [3.1 Testing](#Testing)
    *   [3.2 Article status templates](#Article_status_templates)
    *   [3.3 Related articles templates](#Related_articles_templates)
    *   [3.4 Code formatting templates](#Code_formatting_templates)
    *   [3.5 Note templates](#Note_templates)
    *   [3.6 Miscellaneous templates](#Miscellaneous_templates)
    *   [3.7 Package templates](#Package_templates)
    *   [3.8 Table templates](#Table_templates)
*   [4 See also](#See_also)

## Usage

Templates are used by adding the following markup to an article:

```
{{Template name}}

```

Most templates take additional arguments, such as [Template:Note](/index.php/Template:Note "Template:Note"):

```
{{Note|This text should be noted.}}

```

which produces:

**Note:** This text should be noted.

Some templates use named parameters, such as [Template:hc](/index.php/Template:Hc "Template:Hc"):

```
{{hc|head=/etc/rc.local|output=exit 0}}

```

which produces:

 `/etc/rc.local`  `exit 0` 

The general format is:

```
{{Template name|param1|param2|...|paramN}}

```

See each template's page for specific usage instructions.

### Style

*   Templates should be used with the capitalization shown in the examples in their pages, for example `{{Pkg|...` and `{{ic|...` are correct, while `{{pkg|...` and `{{Ic|...` are not.
*   There should be no spaces around the template name: `{{Template name|...` is correct, while for example `{{ Template name |...` is not.
*   Templates should not be categorized.

### Escape template-breaking characters

There are some characters that, if used inside a template, will break its output: most frequently this happens with "=" (the equal sign) and "|" (the pipe sign). Solutions to this problem are described below.

#### Named parameters

If the problem is only with "=" signs, the recommended solution is to explicitly introduce template parameters with their names or positional numbers. This is very useful for variable definitions or [external links](/index.php/Help:Editing#External_links "Help:Editing") with query strings in URLs, but will not work for other offending characters, like "|". For example:

```
{{Tip|1=https://www.archlinux.org/?foo=bar}}

```

**Tip:** [https://www.archlinux.org/?foo=bar](https://www.archlinux.org/?foo=bar)

Or, with multiple parameters:

```
{{hc|1=$ echo "="|2==}}

```

```
{{hc|head=$ echo "="|output==}}

```

 `$ echo "="`  `=` 

#### nowiki tags

If you are having problems with characters other than "=", e.g. "|", the recommended solution is to enclose the whole parameter in `<nowiki>` tags. This method displays all kinds of characters, but completely prevents the wiki engine from processing text markup, such as links and other templates. For example:

```
{{Tip|<nowiki>= | }} https://www.archlinux.org/ {{ic|foo}}</nowiki>}}

```

**Tip:** = | }} https://www.archlinux.org/ {{ic|foo}}

Enclosing only specific parts (or even single characters) in `<nowiki>` tags still works of course, but for readability it is recommended to use such method only if links or other templates have to be normally displayed. For example:

```
{{Tip|<nowiki>= | }}</nowiki> https://www.archlinux.org/ {{ic|foo}}}}

```

**Tip:** = | }} [https://www.archlinux.org/](https://www.archlinux.org/) `foo`

#### HTML entities

Replacing the offending characters with their respective HTML entities always works, but since it reduces the readability of the source text, it is recommended only when the solutions above are not practicable. For example:

```
{{Tip|&#61; &#124; &#125;&#125;}}

```

**Tip:** = | }}

## Creation

**Note:**

*   Before creating a template, discuss the idea in [Help talk:Template](/index.php/Help_talk:Template "Help talk:Template").
*   Only create relevant templates. If you are attempting to create a very specialized template that will likely only ever be used on a few articles, please do not bother, avoid cluttering up the templates namespace.
*   Only create concise templates. Remember [The Arch Way](/index.php/The_Arch_Way "The Arch Way"): Keep It Simple, Stupid!

The following template should be used when creating new templates to facilitate usage and editing:

```
<noinclude>
{{Template}}

A brief description of the template

== Usage ==

<nowiki>{{Template name|param1|param2|...|paramN}}</nowiki>

== Example ==

{{Template name|param1|param2|...|paramN}}</noinclude><includeonly>Template code goes here...</includeonly>

```

To begin the creation process, simply visit [Template:Template name](/index.php?title=Template:Template_name&action=edit&redlink=1 "Template:Template name (page does not exist)") (substituting `Template name` with the desired name of the template), [edit, and add the relevant wikitext](/index.php/Help:Editing "Help:Editing").

## List of templates

The templates that users can use directly in articles on the ArchWiki are listed below. Click on the links to see their detailed usage. For a list that also includes localizations and meta templates see [Special:AllPages/Template:](/index.php/Special:AllPages/Template: "Special:AllPages/Template:"), [Special:PrefixIndex/Template:](/index.php/Special:PrefixIndex/Template: "Special:PrefixIndex/Template:") or [Special:MostLinkedTemplates](/index.php/Special:MostTranscludedPages "Special:MostTranscludedPages").

**Warning:** Please do not experiment with existing templates. If you want to edit a non-protected template, copy the text to [Template:Sandbox](/index.php/Template:Sandbox "Template:Sandbox"), edit and test it there, and copy it back when it works. It is strongly recommended (and necessary for protected templates) to suggest any modifications on discussion pages first.

### Testing

*   [Template:Sandbox](/index.php/Template:Sandbox "Template:Sandbox")
*   [Template:Lorem Ipsum](/index.php/Template:Lorem_Ipsum "Template:Lorem Ipsum")

### Article status templates

*   [Template:Accuracy](/index.php/Template:Accuracy "Template:Accuracy")
*   [Template:Bad translation](/index.php/Template:Bad_translation "Template:Bad translation")
*   [Template:Deletion](/index.php/Template:Deletion "Template:Deletion")
*   [Template:Expansion](/index.php/Template:Expansion "Template:Expansion")
*   [Template:Laptop style](/index.php/Template:Laptop_style "Template:Laptop style")
*   [Template:Merge](/index.php/Template:Merge "Template:Merge")
*   [Template:Move](/index.php/Template:Move "Template:Move")
*   [Template:Out of date](/index.php/Template:Out_of_date "Template:Out of date")
*   [Template:Redirect](/index.php/Template:Redirect "Template:Redirect")
*   [Template:Stub](/index.php/Template:Stub "Template:Stub")
*   [Template:Style](/index.php/Template:Style "Template:Style")
*   [Template:Translateme](/index.php/Template:Translateme "Template:Translateme")

### Related articles templates

*   [Template:Related articles start](/index.php/Template:Related_articles_start "Template:Related articles start")
*   [Template:Related](/index.php/Template:Related "Template:Related")
*   [Template:Related articles end](/index.php/Template:Related_articles_end "Template:Related articles end")

### Code formatting templates

*   [Template:ic](/index.php/Template:Ic "Template:Ic")
*   [Template:bc](/index.php/Template:Bc "Template:Bc")
*   [Template:hc](/index.php/Template:Hc "Template:Hc")

### Note templates

*   [Template:Note](/index.php/Template:Note "Template:Note")
*   [Template:Tip](/index.php/Template:Tip "Template:Tip")
*   [Template:Warning](/index.php/Template:Warning "Template:Warning")

### Miscellaneous templates

*   [Template:App](/index.php/Template:App "Template:App")
*   [Template:Bug](/index.php/Template:Bug "Template:Bug")
*   [Template:Dead link](/index.php/Template:Dead_link "Template:Dead link")
*   [Template:Broken package link](/index.php/Template:Broken_package_link "Template:Broken package link")
*   [Template:Unsigned](/index.php/Template:Unsigned "Template:Unsigned")

### Package templates

*   [Template:Pkg](/index.php/Template:Pkg "Template:Pkg")
*   [Template:Grp](/index.php/Template:Grp "Template:Grp")
*   [Template:AUR](/index.php/Template:AUR "Template:AUR")

### Table templates

*   [Template:R](/index.php/Template:R "Template:R")
*   [Template:G](/index.php/Template:G "Template:G")
*   [Template:B](/index.php/Template:B "Template:B")
*   [Template:C](/index.php/Template:C "Template:C")
*   [Template:M](/index.php/Template:M "Template:M")
*   [Template:Y](/index.php/Template:Y "Template:Y")
*   [Template:Yes](/index.php/Template:Yes "Template:Yes")
*   [Template:No](/index.php/Template:No "Template:No")

## See also

*   [Template:Template](/index.php/Template:Template "Template:Template")
*   [http://meta.wikimedia.org/wiki/Help:Template](http://meta.wikimedia.org/wiki/Help:Template)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Help:Template&oldid=414593](https://wiki.archlinux.org/index.php?title=Help:Template&oldid=414593)"