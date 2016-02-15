## Contents

*   [1 Introduction](#Introduction)
*   [2 Separate branding from upstream packages](#Separate_branding_from_upstream_packages)
    *   [2.1 Pros](#Pros)
    *   [2.2 Cons](#Cons)
*   [3 Package Naming Scheme](#Package_Naming_Scheme)
*   [4 Essential Artwork](#Essential_Artwork)
    *   [4.1 Completed](#Completed)
    *   [4.2 Pending](#Pending)
*   [5 Other Resources](#Other_Resources)

# Introduction

This article is part of the [DeveloperWiki](/index.php/DeveloperWiki "DeveloperWiki"). Feel free to add any suggestions or concerns.

# Separate branding from upstream packages

Create a separate package of artwork for upstream packages, including:

*   login themes
*   desktop environment additions (wallpapers, icons, etc.)
*   splash screens

Include post-install notes informing the user where to find the theme and where to modify its preference.

#### Pros

*   Upstream packages are delivered as-is
*   Users can choose whether to download Arch-branded content

#### Cons

*   Users will have to modify theme settings manually

# Package Naming Scheme

If artwork is separated from upstream packages, we should have a consistent naming scheme, for example:

*   archlinux-artwork
*   archlinux-wallpaper
*   archlinux-themes-gdm
*   archlinux-themes-kdm
*   archlinux-themes-slim
*   archlinux-themes-xfce

# Essential Artwork

Provide at least 1 style-neutral (minimalist) theme for the standard packages:

#### Completed

*   Framebuffer logo
*   SLiM
*   Qingy
*   Splashy
*   GDM
*   KDM

#### Pending

*   XDM

# Other Resources

[DeveloperWiki](/index.php/DeveloperWiki "DeveloperWiki")