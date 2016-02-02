# Help:Style/Formatting and punctuation

< [Help:Style](/index.php/Help:Style "Help:Style")

The following directions define how different parts of the content of an article should be highlighted through formatting or punctuation.

## Contents

*   [1 General rules](#General_rules)
    *   [1.1 First instances](#First_instances)
    *   [1.2 Links](#Links)
    *   [1.3 Name/term lists](#Name.2Fterm_lists)
*   [2 Cases by formatting/punctuation](#Cases_by_formatting.2Fpunctuation)
    *   [2.1 Italic](#Italic)
    *   [2.2 Bold](#Bold)
    *   [2.3 Monospace](#Monospace)
    *   [2.4 Quote marks](#Quote_marks)
*   [3 Specific cases](#Specific_cases)
    *   [3.1 Acronym/abbreviation expansions](#Acronym.2Fabbreviation_expansions)
        *   [3.1.1 Examples](#Examples)
    *   [3.2 CLI lines](#CLI_lines)
        *   [3.2.1 Examples](#Examples_2)
    *   [3.3 Configuration parameters, variables, options, properties...](#Configuration_parameters.2C_variables.2C_options.2C_properties...)
        *   [3.3.1 Examples](#Examples_3)
    *   [3.4 Daemons/services, kernel modules](#Daemons.2Fservices.2C_kernel_modules)
        *   [3.4.1 Example](#Example)
    *   [3.5 Executable/application names](#Executable.2Fapplication_names)
        *   [3.5.1 Examples](#Examples_4)
    *   [3.6 File content](#File_content)
        *   [3.6.1 Examples](#Examples_5)
    *   [3.7 File extensions](#File_extensions)
        *   [3.7.1 Example](#Example_2)
    *   [3.8 File names and paths](#File_names_and_paths)
        *   [3.8.1 Examples](#Examples_6)
    *   [3.9 Generic words used in an improper or questionable way](#Generic_words_used_in_an_improper_or_questionable_way)
        *   [3.9.1 Example](#Example_3)
    *   [3.10 GUI/TUI text](#GUI.2FTUI_text)
        *   [3.10.1 Examples](#Examples_7)
    *   [3.11 Important part of file/command line contents](#Important_part_of_file.2Fcommand_line_contents)
        *   [3.11.1 Example](#Example_4)
    *   [3.12 Keyboard keys](#Keyboard_keys)
        *   [3.12.1 Example](#Example_5)
    *   [3.13 Package and group names](#Package_and_group_names)
        *   [3.13.1 Example](#Example_6)
    *   [3.14 Pseudo-variables in file/command line contents](#Pseudo-variables_in_file.2Fcommand_line_contents)
        *   [3.14.1 Example](#Example_7)
    *   [3.15 Quotations](#Quotations)
        *   [3.15.1 Examples](#Examples_8)
    *   [3.16 References to titles, headings...](#References_to_titles.2C_headings...)
        *   [3.16.1 Example](#Example_8)
    *   [3.17 Repository names](#Repository_names)
        *   [3.17.1 Example](#Example_9)
    *   [3.18 Stressed/strong words or statements](#Stressed.2Fstrong_words_or_statements)
        *   [3.18.1 Examples](#Examples_9)
    *   [3.19 Technical terms](#Technical_terms)
        *   [3.19.1 Examples](#Examples_10)
    *   [3.20 Words/letters when referenced as mere "text entities"](#Words.2Fletters_when_referenced_as_mere_.22text_entities.22)
        *   [3.20.1 Examples](#Examples_11)

## General rules

These general rules always override [#Specific cases](#Specific_cases). For cases not covered in this guide, [Wikipedia:Manual of Style](https://en.wikipedia.org/wiki/Manual_of_Style "wikipedia:Manual of Style") is the authority reference.

*   Do not mix more than one highlighting method except where explicitly allowed by these rules.
    This rule also applies in the cases where some formatting is already set by CSS rules, for example bold in [definition list terms](/index.php/Help:Editing#Definition_lists "Help:Editing"). If the preset CSS formatting is not allowed on the affected item (e.g. bold on [#File names and paths](#File_names_and_paths)), then you have to resort using a different, compatible wiki markup altogether (e.g. [bullet points](/index.php/Help:Editing#Bullet_points "Help:Editing") instead of a definition list).
*   Do not use different highlighting methods from the ones defined in this manual; this includes, but is not limited to, underlining, blinking, full-word capitalization, colors, asterisks, exclamation marks, emoticons, HTML tags with a `style` attribute.

### First instances

*   The first relevant appearance of a term or name in an article (e.g. executable names) can be _highlighted_ (see below) if regarded as worthy of particular attention, considering the topic of the article or the specific section. The first "relevant" appearance may not be the absolute first appearance of the name: its choice is left to the editor.
*   The preferable way of highlighting the name is using a link to a closely related article in the wiki or to an external page, like Wikipedia; if there are no possible pertinent links, **bold** can be used as a fallback solution.

	Package and group names should make use of [Template:Pkg](/index.php/Template:Pkg "Template:Pkg"), [Template:AUR](/index.php/Template:AUR "Template:AUR") or [Template:Grp](/index.php/Template:Grp "Template:Grp").

*   If the name is already introduced by the title of the article or by a section heading, its first relevant appearance in the body can only be used as a link anchor, but not simply highlighted in bold, except in the case of [#Name/term lists](#Name.2Fterm_lists).
*   First-instance highlighting can be applied only to the [#Specific cases](#Specific_cases) that explicitly allow it.

### Links

*   No formatting shall be applied to the anchor text of links.

### Name/term lists

*   It is allowed, not mandatory, to keep consistent formatting in lists of names or terms, even if normally not all of the items would require to be formatted. This can involve for example all-caps terms, which should not be italic-ized by themselves, or names in a list where most of the items are formatted according to [#First instances](#First_instances).
    "List" is to be intended in a broad sense, so that for example also all the initial words of a series of subsequent paragraphs could be considered forming a list of terms.

## Cases by formatting/punctuation

Cases marked by  are affected by [#First instances](#First_instances). Cases marked by  apply to monospaced text.

### Italic

Use the MediaWiki syntax `''italic text''` instead of `<i>` tags.

*   [#Executable/application names](#Executable.2Fapplication_names)
*   [#File extensions](#File_extensions)
*   [#Repository names](#Repository_names)
*   [#Package and group names](#Package_and_group_names)
*   [#Pseudo-variables in file/command line contents](#Pseudo-variables_in_file.2Fcommand_line_contents)
*   [#GUI/TUI text](#GUI.2FTUI_text)
*   [#Technical terms](#Technical_terms)
*   [#Stressed/strong words or statements](#Stressed.2Fstrong_words_or_statements)
*   [#Acronym/abbreviation expansions](#Acronym.2Fabbreviation_expansions)

### Bold

Use the MediaWiki syntax `'''bold text'''` instead of `<b>` tags.

*   [#Important part of file/command line contents](#Important_part_of_file.2Fcommand_line_contents)
*   [#Stressed/strong words or statements](#Stressed.2Fstrong_words_or_statements)
*   [#First instances](#First_instances)

### Monospace

Use [Template:ic](/index.php/Template:Ic "Template:Ic") `{{ic|monospace text}}` instead of `<code>` tags for text outside of code blocks.

*   [#File names and paths](#File_names_and_paths)
*   [#Daemons/services, kernel modules](#Daemons.2Fservices.2C_kernel_modules)
*   [#Configuration parameters, variables, options, properties...](#Configuration_parameters.2C_variables.2C_options.2C_properties...)
*   [#CLI lines](#CLI_lines)
*   [#File content](#File_content)
*   [#Keyboard keys](#Keyboard_keys)

### Quote marks

Use typewriter quotes `"quoted text"` instead of single quotes `'quoted text'` or typographic quotes `“quoted text”`.

*   [#References to titles, headings...](#References_to_titles.2C_headings...)
*   [#Words/letters when referenced as mere "text entities"](#Words.2Fletters_when_referenced_as_mere_.22text_entities.22)
*   [#Generic words used in an improper or questionable way](#Generic_words_used_in_an_improper_or_questionable_way)
*   [#Quotations](#Quotations)

## Specific cases

[#General rules](#General_rules) always override the following rules.

### Acronym/abbreviation expansions

Use _italic_.

#### Examples

*   Pacman is the Arch Linux _pac_kage _man_ager.
*   [cat](https://en.wikipedia.org/wiki/cat_(Unix) "wikipedia:cat (Unix)") (_catenate_) is a standard Unix utility that concatenates and lists files.

### CLI lines

Use `monospace`. Must be inline command examples, not simple mentions of [#Executable/application names](#Executable.2Fapplication_names). Also console output and text that may reasonably be useful to paste in a terminal.

#### Examples

*   You are encouraged to type `man _command_` to read the _man_ page of any command.
*   You can use the command `ip link` to discover the names of your interfaces.
*   If you get a `ping: unknown host` error, first check if there is an issue with your cable or wireless signal strength.
*   Type `yes` and choose _Quit_ (or press `Q`) to exit without making any more changes.
*   Execute `pacman -Syu` with root privileges.

### Configuration parameters, variables, options, properties...

Use `monospace`. Also affects command options, user groups, IP addresses, environment variables and variables in general.

When both the short and long form of a command option have to be represented, use the "/" symbol without spaces to separate them, for example `-a`/`--anything`.

#### Examples

*   By default, the keyboard layout is set to `us`.
*   [...] where _layout_ can be `fr`, `uk`, `dvorak`, `be-latin1`, etc.
*   As of v197, _udev_ no longer assigns network interface names according to the `wlanX` and `ethX` naming scheme.
*   In this example, the Ethernet interface is `enp2s0f0`.
*   If you are unsure, your Ethernet interface is likely to start with the letter "e", and unlikely to be `lo` or start with the letter "w".
*   Currently, you may include a maximum of three `nameserver` lines.
*   You will need to create an extra [BIOS Boot Partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") of size 1007 KiB and `EF02` type code.
*   All files should have `644` permissions and `root:root` ownership.
*   The `-i` switch can be omitted if you wish to install every package from the [base](https://www.archlinux.org/groups/x86_64/base/) group without prompting.
*   Adding your user to [groups](/index.php/Users_and_groups "Users and groups") (`sys`, `disk`, `lp`, `network`, `video`, `audio`, `optical`, `storage`, `scanner`, `power`, etc.) is **not** necessary for most use cases with systemd.
*   If you are behind a proxy server, you will need to export the `http_proxy` and `ftp_proxy`environment variables.
*   To use other locales for other `LC_*` variables, run `locale` to see the available options and add them to _locale.conf_. It is not recommended to set the `LC_ALL` variable. An advanced example can be found [here](/index.php/Locale#Setting_system-wide_locale "Locale").
*   [...] this roughly equates to what you included in the `DAEMONS` array.
*   If you are running a private network, it is safe to use IP addresses in `192.168.*.*` for your IP addresses, with a subnet mask of `255.255.255.0` and a broadcast address of `192.168.*.255`. The gateway is usually `192.168.*.1` or `192.168.*.254`.
*   By giving the `-net nic` argument to QEMU, it will, by default, assign a virtual machine a network interface with the link-level address `52:54:00:12:34:56`.

### Daemons/services, kernel modules

Use `monospace`.

#### Example

*   The `dhcpcd.service` starts the daemon for all network interfaces.
*   Some unit names contain an `@` sign (e.g. `name@_string_.service`).

### Executable/application names

Use _italic_, but only for full lower-case names. Affected by [#First instances](#First_instances).

Note that this rule applies to executables only when they represent the application/file itself, not when used in [#CLI lines](#CLI_lines). In particular pay attention to executables that are usually run without any arguments.

#### Examples

*   Uncomment the selected locale in `/etc/locale.gen` and generate it with the _locale-gen_ utility.
*   Uncomment the selected locale in `/etc/locale.gen` and generate it with `locale-gen`.
*   As of v197, _udev_ no longer assigns network interface names according to the `wlan_X_` and `eth_X_` naming scheme.
*   The Arch Linux install media includes the following partitioning tools: _fdisk_, _gdisk_, _cfdisk_, _cgdisk_, _parted_.
*   If pacman fails to verify your packages, check the system time with `cal`.
*   Set a root password with `passwd`.

### File content

Use `monospace` for content that can be both read or written on a file or that may reasonably be useful to copy from or paste in a text editor.

#### Examples

*   At the end of the string type `nomodeset` and press `Enter`. Alternatively, try `video=SVIDEO-1:d` which, if it works, will not disable kernel mode setting.
*   Remove the `#` in front of the [locale](http://www.greendesktiny.com/support/knowledgebase_detail.php?ref=EUH-483) you want from `/etc/locale.gen`.

### File extensions

Use _italic_.

#### Example

*   Pacman is written in the C programming language and uses the _.pkg.tar.xz_ package format.

### File names and paths

Use `monospace`. Also device names and names with wildcards are affected. [#File extensions](#File_extensions) are treated differently, though.

#### Examples

*   To test if you have booted into UEFI mode check if directory `/sys/firmware/efi` has been created.
*   All files and directories appear under the root directory `/`, even if they are stored on different physical devices.
*   Edit `resolv.conf`, substituting your name servers' IP addresses and your local domain name.
*   Before installing, you may want to edit the `mirrorlist` file and place your preferred mirror first.
*   For kernel modules to load during boot, place a `*.conf` file in `/etc/modules-load.d/`, with a name based on the program that uses them.
*   Each partition is identified with a number suffix. For example, `sda1` specifies the first partition of the first drive, while `sda` designates the entire drive.

### Generic words used in an improper or questionable way

Use "typewriter quotes".

#### Example

*   Words/letters when referenced as mere "text entities".

### GUI/TUI text

Use _italic_. For example for menu entries. When representing navigation in menus, use the "_>_" symbol, still in _italic_, to separate the items.

#### Examples

*   Then, select _Boot Arch Linux_ from the menu and press `Enter` in order to begin with the installation.
*   When using Gparted, selecting the option to create a new partition table gives an _msdos_ partition table by default. If you are intending to follow the advice to create a GPT partition table then you need to choose _Advanced_ and then select _gpt_ from the drop-down menu.
*   Type `yes` and choose _Quit_ (or press `Q`) to exit without making any more changes.
*   For plugins to be updated, you should check to have their update repositories enabled in _Window > Preferences > Install/Update > Available Software Sites_.

### Important part of file/command line contents

Use **bold**. Since these contents are code themselves, when referenced outside of the template, `monospace` should be preserved.

#### Example

*   `# ln -s /usr/src/linux-**$(uname -r)**/include/generated/uapi/linux/version.h /usr/src/linux-**$(uname -r)**/include/linux/` 

	You can replace **`$(uname -r)`** with any kernel not currently running.

### Keyboard keys

Use `monospace`.

#### Example

*   You have to press a key (usually `Delete`, `F1`, `F2`, `F11`, or `F12`) during the POST.

### Package and group names

Use _italic_. Affected by [#First instances](#First_instances).

#### Example

*   The package _wireless_tools_ then provides a basic set of tools for managing the wireless connection.

### Pseudo-variables in file/command line contents

Use _italic_. When mentioning a variable outside of the template, `monospace` should be preserved.

Make sure that variables do not contain any spaces: underscores should be used in their place.

Ensure naming consistency with the rest of the article, which may already use a pseudo-variable. For example do not introduce a new `_keyboardlayout_` variable, if `_keyboard_layout_` is already used.

#### Example

*   `# loadkeys _keyboard_layout_` 

	[...] where `_keyboard_layout_` can be `fr`, `uk`, `dvorak`, `be-latin1`, etc.

*   Bring the interface up with `ip link set _interface_ up`.
*   You can connect to the network with:

	 `# wifi-menu _interface_name_` 

	Where `_interface_name_` is the interface of your wireless chipset.

### Quotations

For inline quotations, use "typewriter quotes". For block quotations, use indentation through a line-initial colon without any additional punctuation or formatting.

#### Examples

*   "All your data belongs to us" – Google
*   From [http://www.x.org/wiki/](http://www.x.org/wiki/):

	The X.Org project provides an open source implementation of the X Window System. The development work is being done in conjunction with the freedesktop.org community. The X.Org Foundation is the educational non-profit corporation whose Board serves this effort, and whose Members lead this work.

### References to titles, headings...

Use "typewriter quotes". When referencing section headings, however, use internal anchor links (`[[#Section]]`).

#### Example

*   The column "dm-crypt +/- LUKS" denotes features of dm-crypt for both LUKS ("+") and plain ("-") encryption modes. If a specific feature requires using LUKS, this is indicated by "(with LUKS)". Likewise "(without LUKS)" indicates usage of LUKS is counter-productive to achieve the feature and plain mode should be used.

### Repository names

Use _italic_ for repository names. Affected by [#First instances](#First_instances).

#### Example

*   To enable the _testing_ repository, you have to uncomment the `[testing]` section in `/etc/pacman.conf`.
*   If you enable the _testing_ repository, you must also enable the _community-testing_ repository.

### Stressed/strong words or statements

Use _italic_ for words whose importance in giving the meaning to a sentence would not be recognized otherwise; usually they would be pronounced in a stressed way if reading out loud.

When however particular attention is needed, words like "not", "only", "exactly", "strongly", "before"... can be highlighted in **bold**.

The same goes for very important statements that cannot be put in a separate Warning or Note as they are an essential part of the section itself.

#### Examples

*   Choose the best environment for _your_ needs.
*   This command can synchronize the repository databases _and_ update the system's packages.
*   If the screen does _not_ go blank and the boot process gets stuck.
*   [...] so please type it _exactly_ as you see it.
*   If you want, you can make it the _only_ mirror available by getting rid of everything else.
*   Partitioning can destroy data. You are **strongly** cautioned and advised to backup any critical data before proceeding.
*   keep up to date with changes in Arch Linux that require manual intervention **before** upgrading your system.
*   **When performing a system update, it is essential that users read all information output by pacman and use common sense.**
*   This means that partial upgrades are **not supported**.

### Technical terms

Use _italic_, except for all-caps terms (usually acronyms). Affected by [#First instances](#First_instances).

#### Examples

*   You are encouraged to type `man _command_` to read the _man_ page of any command.
*   This article deals with so-called _core_ utilities on a GNU/Linux system.
*   _Primary_ partitions can be bootable and are limited to four partitions per disk or RAID volume.
*   This is already a separate partition by default, by virtue of being mounted as _tmpfs_ by systemd.
*   You have to press a key (usually `Delete`, `F1`, `F2`, `F11` or `F12`) during the POST (Power On Self-Test) phase.

### Words/letters when referenced as mere "text entities"

Use "typewriter quotes".

#### Examples

*   When however particular attention is needed, words like "not", "only", "exactly", "strongly", "before"... can be highlighted in **bold**.
*   If you are unsure, your Ethernet interface is likely to start with the letter "e", and unlikely to be `lo` or start with the letter "w".

Retrieved from "[https://wiki.archlinux.org/index.php?title=Help:Style/Formatting_and_punctuation&oldid=386131](https://wiki.archlinux.org/index.php?title=Help:Style/Formatting_and_punctuation&oldid=386131)"