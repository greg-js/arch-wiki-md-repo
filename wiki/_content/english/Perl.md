Related articles

*   [Perl Policy](/index.php/Perl_Policy "Perl Policy")
*   [Perl package guidelines](/index.php/Perl_package_guidelines "Perl package guidelines")
*   [mod_perl](/index.php/Mod_perl "Mod perl")

From [Wikipedia](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl"):

	Perl is a family of high-level, general-purpose, interpreted, dynamic programming languages. The languages in this family include Perl 5 and Perl 6.

	The Perl languages borrow features from other programming languages including C, shell script (sh), AWK, and sed. They provide powerful text processing facilities without the arbitrary data-length limits of many contemporary Unix commandline tools, facilitating easy manipulation of text files. Perl 5 gained widespread popularity in the late 1990s as a CGI scripting language, in part due to its then unsurpassed regular expression and string parsing abilities.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Perl 5](#Perl_5)
    *   [1.2 Perl 6](#Perl_6)
*   [2 Commands](#Commands)
    *   [2.1 Perl 5](#Perl_5_2)
    *   [2.2 Perl 6](#Perl_6_2)
*   [3 Perl 5 examples](#Perl_5_examples)
*   [4 Package management](#Package_management)
    *   [4.1 pacman and AUR](#pacman_and_AUR)
    *   [4.2 CPAN.pm](#CPAN.pm)
        *   [4.2.1 Configuring cpan](#Configuring_cpan)
        *   [4.2.2 Usage examples](#Usage_examples)
*   [5 Widget bindings](#Widget_bindings)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Improved module management](#Improved_module_management)
        *   [6.1.1 cpanminus](#cpanminus)
        *   [6.1.2 ucpan](#ucpan)
        *   [6.1.3 Bundle::CPAN](#Bundle::CPAN)
    *   [6.2 Re-run cpan configuration](#Re-run_cpan_configuration)
    *   [6.3 Create new module](#Create_new_module)
        *   [6.3.1 module-starter](#module-starter)
*   [7 See also](#See_also)
    *   [7.1 Perl 5](#Perl_5_3)
    *   [7.2 Perl 6](#Perl_6_3)
    *   [7.3 CPAN](#CPAN)
    *   [7.4 Tutorials](#Tutorials)
    *   [7.5 Miscellaneous](#Miscellaneous)

## Installation

### Perl 5

The [perl](https://www.archlinux.org/packages/?name=perl) package for Perl 5 is installed as part of the [base](https://www.archlinux.org/packages/?name=base) group during Arch Linux installation.

### Perl 6

A Perl 6 compiler is provided by [rakudo](https://aur.archlinux.org/packages/rakudo/) that targets MoarVM and JVM. This AUR package has [moarvm](https://aur.archlinux.org/packages/moarvm/) as a dependency.

## Commands

### Perl 5

The Perl language interpreter:

```
$ perl

```

Perl bug reporting:

```
$ perlbug

```

Lookup the Perl documentation in [POD](https://en.wikipedia.org/wiki/Plain_Old_Documentation "wikipedia:Plain Old Documentation") format:

```
$ perldoc

```

Send the Perl authors and maintainers a thank you message:

```
$ perlthanks

```

### Perl 6

Rakudo Perl 6 compiler:

```
$ perl6

```

## Perl 5 examples

Classic "Hello, World!" for calling with `$ perl hello-world.pl`:

 `hello-world.pl` 
```
use strict;
use warnings;

print "Hello, World!
";

```

With the executable bit set for calling with `$ ./hello-you`:

 `hello-you` 
```
#!/usr/bin/env perl

use strict;
use warnings;

print "Please enter your name: ";
my $name = <STDIN>;
chomp ($name);
print "Hello $name. Glad to meet you.
";

```

A one liner to print the first 10 Fibonacci numbers:

```
$ perl -le'$==1,(1x$_)=~/(^)(1|11\1)*(?{$=++})^/,print$=for 0..10'

```

## Package management

The [Comprehensive Perl Archive Network (CPAN)](https://www.cpan.org/) is a repository of over 250,000 software modules and accompanying documentation written in the Perl programming language by over 12,000 contributors.

CPAN is also the name of a Perl module, CPAN.pm, which is used to download and install Perl software from the CPAN archive.

### pacman and AUR

A number of popular CPAN modules are available as [packages](https://www.archlinux.org/packages/?q=cpan) in the Arch repositories. There are further modules available in the [AUR](https://aur.archlinux.org/packages/?K=cpan).

### CPAN.pm

The CPAN.pm module is included with Perl. It can be used interactively from the shell or in Perl scripts.

#### Configuring cpan

Before first use, the module needs to be configured. This is done interactively from the shell with (some output omitted):

 `$ cpan` 
```
CPAN.pm requires configuration, but most of it can be done automatically.
If you answer 'no' below, you will enter an interactive dialog for each
configuration option instead.

Would you like to configure as much as possible automatically? [yes]

```

Automated configuration will suit most users. Answering yes, the configuration will continue with:

```
To install modules, you need to configure a local Perl library directory or
escalate your privileges. CPAN can help you by bootstrapping the local::lib
module or by configuring itself to use 'sudo' (if available). You may also
resolve this problem manually if you need to customize your setup.

What approach do you want?  (Choose 'local::lib', 'sudo' or 'manual')
 [local::lib]

```

If you want `cpan` to install modules in your home directory choose `local::lib`. To install them system-wide choose `sudo`. Choosing `sudo` the configuration ends:

```
Autoconfiguration complete.

commit: wrote '/home/*username*/.cpan/CPAN/MyConfig.pm'

```

Choosing the `local::lib` option will result in addition modules being installed.

Choosing not to use automated configuration allows the user to set `cpan` options interactively in the shell. The table below shows some option names with a brief description and default value. More detailed information is displayed for each option during configuration.

| Name | Description | Default |
| cpan_home | CPAN build and cache directory | $HOME/.cpan |
| keep_source_where | Download target directory | $HOME/.cpan/sources |
| build_dir | Build process directory | $HOME/.cpan/build |
| prefs_dir | Customizable modules options directory | $HOME/.cpan/prefs |
| build_cache | Cache size for build directory | 100MB |
| cleanup_after_install | Remove build directory after successful install | No |
| shell | Preferred shell | /bin/bash |
| halt_on_failure | Halt on failure | No |
| colorize_output | Turn on colored output | No |
| histfile | History file location | $HOME/.cpan/histfile |
| histsize | History file size | 100 lines |

The configuration file $HOME/.cpan/CPAN/MyConfig.pm can be edited with your text editor of choice.

#### Usage examples

To simply install a modules pass them as parameters to `cpan` (multiple module names are separated by spaces):

```
$ cpan Acme::MetaSyntactic

```

The following examples are all in the `cpan` interactive shell, started with:

```
$ cpan

```

Display information on a module:

 `cpan[1]> m Acme::MetaSyntactic` 
```
Reading '/home/*username*/.cpan/Metadata'
  Database was generated on Fri, 08 Dec 2017 02:17:03 GMT
Module id = Acme::MetaSyntactic
    CPAN_USERID  BOOK (Philippe Bruhat (BooK) <book@cpan.org>)
    CPAN_VERSION 1.014
    CPAN_FILE    B/BO/BOOK/Acme-MetaSyntactic-1.014.tar.gz
    INST_FILE    (not installed)
```

View module README:

 `cpan[2]> readme Acme::MetaSyntactic` 
```
Acme::MetaSyntactic - Themed metasyntactic variables

DESCRIPTION

When writing code examples, it's always easy at the beginning:

   my $foo = "bar";
   $foo .= "baz";   # barbaz
...
```

Install a module:

```
cpan[3]> install Acme::MetaSyntactic

```

## Widget bindings

The following [widget toolkit](https://en.wikipedia.org/wiki/Widget_toolkit "wikipedia:Widget toolkit") bindings are available:

*   **gtk2-perl** — GTK2 bindings

	[http://gtk2-perl.sourceforge.net/](http://gtk2-perl.sourceforge.net/) || [gtk2-perl](https://www.archlinux.org/packages/?name=gtk2-perl)

*   **perl-gtk3** — GTK3 bindings

	[https://metacpan.org/release/Gtk3](https://metacpan.org/release/Gtk3) || [perl-gtk3](https://www.archlinux.org/packages/?name=perl-gtk3)

*   **Perl/TK** — Tk bindings

	[http://search.cpan.org/dist/Tk/](http://search.cpan.org/dist/Tk/) || [perl-tk](https://www.archlinux.org/packages/?name=perl-tk)

*   **perlqt** — [Qt](/index.php/Qt "Qt") bindings

	[https://github.com/KDE/perlqt](https://github.com/KDE/perlqt) || perlqt

*   **wxPerl** — wxWidgets bindings

	[http://www.wxperl.it/](http://www.wxperl.it/) || [perl-wx](https://aur.archlinux.org/packages/perl-wx/)

*   **Prima** — a perl multiplatform graphic toolkit

	[https://metacpan.org/release/Prima](https://metacpan.org/release/Prima) || [perl-prima](https://aur.archlinux.org/packages/perl-prima/)

Or you can just draw asci art to create simple gui/webpage user interface:

*   **GUIDeFATE** — Graphical User Interface Design From A Text Editor

	[https://metacpan.org/pod/GUIDeFATE](https://metacpan.org/pod/GUIDeFATE) || [perl-guidefate](https://aur.archlinux.org/packages/perl-guidefate/)

To use these with Perl, you may need to install the associated widget kits.

## Tips and tricks

### Improved module management

#### cpanminus

[cpanminus](https://metacpan.org/release/App-cpanminus) extends module management and aims to be zero configuration and integrates with `local::db`. To install use:

```
$ cpan App::cpanminus

```

The [cpanminus documentation](https://metacpan.org/pod/distribution/App-cpanminus/bin/cpanm) gives examples.

#### ucpan

[ucpan](https://metacpan.org/pod/distribution/App-ucpan/script/ucpan) is a nice, fully automatic updater for CPAN modules (especially installed in local-lib). To install use:

```
cpan App::ucpan

```

#### Bundle::CPAN

Installing the [Bundle::CPAN](https://metacpan.org/release/Bundle-CPAN) distribution will add a lot of nice functionality to CPAN.pm.

```
$ cpan Bundle::CPAN

```

### Re-run cpan configuration

```
$ cpan
cpan[1]> o conf init

```

### Create new module

#### module-starter

[Module::Starter](https://metacpan.org/pod/distribution/Module-Starter/bin/module-starter) helps you create your new module... Install:

```
cpanm Module::Starter

```

Usage:

```
module-starter --module=App::foobar  --author="My name here" --email=my@email.here --mb

```

This going to create your module tree...

**Note:** Option `--mb` create module which will use [Module::Build](https://metacpan.org/release/Module-Build). The next part assumes that you are using this module.

To add dependiences, put `module_name => version_or_0` inside `$builder -> requires` in file `Build.PL`

To install required dependiences for your project, run inside `App-foobar` folder:

```
cpanm --installdeps .

```

To skip git folder, add under `$builder`

```
add_to_manifest_skip => [ '.git' ],

```

Adding scripts can by done like this:

```
mkdir bin
touch bin/foobar

```

To run this script:

```
perl -Ilib bin/foobar

```

You can change your project version here: `lib/App/foobar.pm`

To install your module run this command in module root folder:

```
cpanm .

```

See more on: [cpan page](https://metacpan.org/release/Module-Build), [cookbook](https://metacpan.org/pod/Module::Build::Cookbook)

## See also

### Perl 5

*   [The Perl Programming Language (Perl homepage)](https://www.perl.org/)
*   [Wikipedia:Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl")
*   [Perl Tutorials](https://learn.perl.org/tutorials/)
*   [perl(1perl)](https://jlk.fjfi.cvut.cz/arch/manpages/man/perl.1perl)
*   [perldoc(1perl)](https://jlk.fjfi.cvut.cz/arch/manpages/man/perldoc.1perl)

### Perl 6

*   [The Perl 6 Programming Language](https://perl6.org/)
*   [Wikipedia:Perl 6](https://en.wikipedia.org/wiki/Perl_6 "wikipedia:Perl 6")
*   [Getting started with Perl 6](https://perl6.org/getting-started/)
*   [Rakudo](https://rakudo.org)
*   [wikipedia:Rakudo Perl 6](https://en.wikipedia.org/wiki/Rakudo_Perl_6 "wikipedia:Rakudo Perl 6")
*   [perl6(1)](https://linux.die.net/man/1/perl6)

### CPAN

*   [Comprehensive Perl Archive Network](https://www.cpan.org)
*   [wikipedia:CPAN](https://en.wikipedia.org/wiki/CPAN "wikipedia:CPAN")
*   [CPAN / CPAN Shell / CPANPLUS Quick Reference Guide](http://joshr.com/src/docs/CPANQuickReference.pdf)

### Tutorials

*   [Tutorials at perldoc](http://perldoc.perl.org/index-tutorials.html)
*   [cpan configuration](http://learnperl.scratchcomputing.com/tutorials/configuration/)
*   [PerlMonks Tutorials](http://www.perlmonks.org/?node=Tutorials)

### Miscellaneous

*   [Perl 5 vs 6](https://www.reddit.com/r/perl/comments/68bd1j/perl_5_vs_6/)