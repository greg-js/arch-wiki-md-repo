# Help:Cheatsheet

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

For a full list of editing commands, see [Help:Editing](/index.php/Help:Editing "Help:Editing"). To experiment with editing, use the [sandbox](/index.php/Sandbox "Sandbox").

<table align="center" style="width:100%; border:1px #0771a6 solid; background:#f9f9f9; text-align:left; border-collapse:collapse;">

<tbody>

<tr style="background:#333333; color:#ffffff; font-size: 0.9em; text-align:center;">

<td colspan="3">**Works anywhere in the text (wikitext)**</td>

</tr>

<tr style="background:#333333; color:#ffffff; font-size: 0.9em; text-align:center;">

<td width="30%">Description</td>

<td>You type</td>

<td width="30%">You get</td>

</tr>

<tr>

<td>Italic text</td>

<td>

`''italic''`

</td>

<td>

_italic_

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Bold text</td>

<td>

`'''bold'''`

</td>

<td>

**bold**

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Bold and italic text</td>

<td>

`'''''bold & italic'''''`

</td>

<td>

_**bold & italic**_

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Link to another ArchWiki page</td>

<td>

`[[Name of page]]`  
`[[Name of page|Text to display]]`

</td>

<td>

[Name of page](/index.php?title=Name_of_page&action=edit&redlink=1 "Name of page (page does not exist)")  
[Text to display](/index.php?title=Name_of_page&action=edit&redlink=1 "Name of page (page does not exist)")

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Add a page to a category

_Categories should be placed at the **beginning** of pages._

</td>

<td>`[[Category:Category name]]`</td>

<td>The category name will display in a bar at the bottom when the page is previewed or saved.</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Signature

_Sign your contributions when posting to a_ Talk _page._

_Do not sign when contributing to an article._

</td>

<td>

`~~~~`

</td>

<td>

[Username](/index.php/Special:MyPage "Special:MyPage"), 04:52, 5 December 2015 (UTC)

</td>

</tr>

<tr style="background:#333333; color:#ffffff; font-size: 0.9em; text-align:center;">

<td colspan="3">**Works anywhere in the text (HTML)**</td>

</tr>

<tr style="background:#333333; color:#ffffff; font-size: 0.9em; text-align:center;">

<td width="30%">Description</td>

<td>You type</td>

<td width="30%">You get</td>

</tr>

<tr>

<td>Strikethrough</td>

<td>

`<s>strikethrough</s>`

</td>

<td>

<s>strikethrough</s>

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Underline</td>

<td>

`<u>underline</u>`

</td>

<td>

<u>underline</u>

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Centering text</td>

<td>

`<center>center</center>`

</td>

<td>

<center>center</center>

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Subscripts and superscripts</td>

<td>

`<sub>sub</sub> <sup>sup</sup>`

</td>

<td>

<sub>sub</sub> <sup>sup</sup>

</td>

</tr>

<tr style="background:#333333; color:#ffffff; font-size: 0.9em; text-align:center;">

<td colspan="3">**Works only at the beginning of lines**</td>

</tr>

<tr style="background:#333333; color:#ffffff; font-size: 0.9em; text-align:center;">

<td width="30%">Description</td>

<td>You type</td>

<td width="30%">You get</td>

</tr>

<tr>

<td>Code

_Start code lines with one or more spaces._

_See also [Help:Style#Code formatting](/index.php/Help:Style#Code_formatting "Help:Style")._

</td>

<td>

` $ echo Hello World`

</td>

<td> `$ echo Hello World` </td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Redirect to another page

_Redirects must be placed at the start of the first line._

</td>

<td>

`#REDIRECT [[Target page]]`

</td>

<td>

→ [Target page](/index.php?title=Target_page&action=edit&redlink=1 "Target page (page does not exist)")

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Section headings

_A Table of Contents will automatically be generated for articles with four or more headings._

_=Level 1= should not be used._

_See also [Help:Effective use of headers](/index.php/Help:Effective_use_of_headers "Help:Effective use of headers")._

</td>

<td>

`== Level 2 ==`  
`=== Level 3 ===`  
`==== Level 4 ====`  
`===== Level 5 =====`  
`====== Level 6 ======`  

</td>

<td>

## Level 2

### Level 3

#### Level 4

##### Level 5

###### Level 6

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Horizontal rule</td>

<td>

`----`

</td>

<td>

* * *

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Bulleted list</td>

<td>

`* One`  
`* Two`  
`** Two point one`  
`* Three`

</td>

<td>

*   One
*   Two
    *   Two point one
*   Three

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Numbered list</td>

<td>

`# One`  
`# Two`  
`## Two point one`  
`# Three`  

</td>

<td>

1.  One
2.  Two
    1.  Two point one
3.  Three

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Definition list</td>

<td>

`; Term one: Definition one`  
`; Term two: Definition two`  

</td>

<td>

Term one

Definition one

Term two

Definition two

</td>

</tr>

<tr style="border-top:1px solid #aaaaaa;">

<td>Indenting text

_This is generally used when replying on a_ Talk _page, as it keeps conversations easy to browse._

</td>

<td>

`no indent (normal)`  
`:first indent`  
`::second indent`  
`:::third indent`

</td>

<td>

no indent (normal)  

first indent

second indent

third indent

</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Help:Cheatsheet&oldid=393588](https://wiki.archlinux.org/index.php?title=Help:Cheatsheet&oldid=393588)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Help](/index.php/Category:Help "Category:Help")