# OpenSync

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

OpenSync is a framework which provides synchronization services for PIM data. Generally it consists of the library libopensync, various plugins and the cli msynctool/osynctool.

## Versioning

The OpenSync project provides a stable release, currently version 0.22, and a unstable/experimental release 0.3x, currently latest is version 0.39\. Project access via SVN is also possible. A release date for the next stable version 0.40 is not yet announced.

## Dependencies

Generally a mixture of different version numbers should be avoided especially between the stable and experimental releases. A version 0.22 plugin insists on a version 0.22 libopensync and a version 0.39 plugin should joined with the corresponding unstable library version. Since not every version step provides all available plugins, your chosen version of libopensync may depend on your plugin needs.

<table class="wikitable">

<tbody>

<tr>

<td>branch</td>

<td>stable</td>

<td colspan="2">unstable</td>

</tr>

<tr>

<td>libopensync version</td>

<td>[libopensync-stable](https://aur.archlinux.org/packages/libopensync-stable/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libopensync-stable)]</sup>-0.22</td>

<td>0.33 - 0.38</td>

<td>0.39</td>

</tr>

<tr>

<td>available plugins</td>

<td>

*   evolution2
*   file
*   gnokii
*   google-calendar
*   gpe
*   irmc
*   jescs
*   kdepim (KDE3)
*   ldap
*   moto
*   opie
*   palm
*   python
*   sunbird
*   syncce
*   syncml

</td>

<td>

see [http://opensync.org/download/releases/](http://opensync.org/download/releases/)

</td>

<td>

*   [libopensync-plugin-evolution2](https://aur.archlinux.org/packages/libopensync-plugin-evolution2/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libopensync-plugin-evolution2)]</sup>
*   [libopensync-plugin-file-unstable](https://aur.archlinux.org/packages/libopensync-plugin-file-unstable/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libopensync-plugin-file-unstable)]</sup>
*   [libopensync-plugin-syncml](https://aur.archlinux.org/packages/libopensync-plugin-syncml/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libopensync-plugin-syncml)]</sup>
*   [libopensync-plugin-vformat](https://aur.archlinux.org/packages/libopensync-plugin-vformat/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libopensync-plugin-vformat)]</sup>
*   [libopensync-plugin-xmlformat](https://aur.archlinux.org/packages/libopensync-plugin-xmlformat/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libopensync-plugin-xmlformat)]</sup>

</td>

</tr>

<tr>

<td>cli interface</td>

<td>[msynctool-stable](https://aur.archlinux.org/packages/msynctool-stable/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/msynctool-stable)]</sup></td>

<td>msynctool with corresponding version (?)</td>

<td>[osynctool](https://aur.archlinux.org/packages/osynctool/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/osynctool)]</sup></td>

</tr>

<tr>

<td>gui</td>

<td>[multisync-gui](https://aur.archlinux.org/packages/multisync-gui/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/multisync-gui)]</sup></td>

<td colspan="2">n.a.</td>

</tr>

</tbody>

</table>

The kdepim plugin in the stable branch is useless in KDE 4, since PIM data is managed by akonadi. A suitable plugin is proposed as a part of the oncoming version 0.40\. A user who wants to synchronize a syncml-capable mobile phone with evolution might be satisfied with the latest unstable version. Other users might prefer the old but stable branch. Since the _community_ repository provides the latest unstable version of libopensync a manual downgrading is necessary. For i686, there is a unofficial user repository:

```
[kpiche]
# Stable OpenSync packages.
Server = [http://kpiche.archlinux.ca/repo](http://kpiche.archlinux.ca/repo)

```

## Configuration

Examples for 0.22 release: [http://www.opensync.org/wiki/releases/0.2x](http://www.opensync.org/wiki/releases/0.2x)

Retrieved from "[https://wiki.archlinux.org/index.php?title=OpenSync&oldid=392524](https://wiki.archlinux.org/index.php?title=OpenSync&oldid=392524)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [System administration](/index.php/Category:System_administration "Category:System administration")