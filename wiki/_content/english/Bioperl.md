[Bioperl](http://www.bioperl.org/wiki/Main_Page) is a set of scripts in the Perl programming language to aid researchers in [Computational Biology](https://en.wikipedia.org/wiki/Computational_biology "wikipedia:Computational biology") and [Bioinformatics](https://en.wikipedia.org/wiki/Bioinformatics "wikipedia:Bioinformatics").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Extras](#Extras)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 See also](#See_also)

## Installation

Install [bioperl](https://aur.archlinux.org/packages/bioperl/) from the [AUR](/index.php/AUR "AUR").

## Configuration

If you installed from the AUR to the `/usr` path (default), the path to bioperl should be added to the @INC array of perl. This is easily done editing the PERL5LIB variable in your .bashrc file, like this:

```
$ nano ~/.bashrc

```

Then adding this line to the end of the file:

```
export PERL5LIB=$PERL5LIB:/usr/share/perl5/site_perl/5.10.0

```

Note: Please take a look at folder `/usr/share/perl5/site_perl/` to see if the version is the same, the folder 5.10.0 (or a newer version) should contain a folder named BIO. If nor 5.10.0 neither other version is found, look for the Bio folder in `vendor_perl` or any other perl5 folder where the Bio folder may have been installed, add the path where the Bio folder is to the bash file.

After saving the file, for the `$PERL5LIB` variable to be updated, bash must be reloaded in terminal:

```
$ bash

```

It is adviced to install extra modules from CPAN, to avoid having dependencies errors.

*   Upgrade CPAN

```
# perl -MCPAN -e shell
install Bundle::CPAN
q

```

*   Install/upgrade Module::Build, and make it your preferred installer

```
# cpan
install Module::Build
o conf prefer_installer MB
o conf commit
q

```

## Extras

The package Bioperl-run, which provides wrapper modules around many common bioinformatics applications and tools, is not installed by default.

```
# cpan
d /bioperl/

```

Which would return something like this:

```
Distribution    BIRNEY/bioperl-1.2.2.tar.gz
Distribution    BIRNEY/bioperl-1.2.3.tar.gz
Distribution    BIRNEY/bioperl-1.2.tar.gz
Distribution    BIRNEY/bioperl-1.4.tar.gz
Distribution    BIRNEY/bioperl-db-0.1.tar.gz
Distribution    BIRNEY/bioperl-ext-1.4.tar.gz
Distribution    BIRNEY/bioperl-gui-0.7.tar.gz
Distribution    BIRNEY/bioperl-run-1.4.tar.gz
Distribution    BOZO/Fry-Lib-BioPerl-0.15.tar.gz
Distribution    CJFIELDS/BioPerl-1.6.0.tar.gz
Distribution    CJFIELDS/BioPerl-1.6.1.tar.gz
Distribution    CJFIELDS/BioPerl-db-1.6.0.tar.gz
Distribution    CJFIELDS/BioPerl-network-1.6.0.tar.gz
Distribution    CJFIELDS/BioPerl-run-1.6.1.tar.gz
Distribution    CRAFFI/Bundle-BioPerl-2.1.8.tar.gz
15 items found

```

Then simply do (check the version compatibility):

```
install CJFIELDS/BioPerl-run-1.6.1.tar.gz
q

```

## Troubleshooting

If you run into trouble while compiling your perl scripts, with an error like `Can't locate (Name of the Module) in @INC`, install the missing modules like this:

```
# cpan
install Module::Name
q

```

## See also

*   [Installing Bioperl for Unix](http://www.bioperl.org/wiki/Installing)