## Contents

*   [1 Volba](#Volba)
    *   [1.1 Tradiční](#Tradi.C4.8Dn.C3.AD)
    *   [1.2 Použití Arch Build System](#Pou.C5.BEit.C3.AD_Arch_Build_System)
*   [2 Links](#Links)

## Volba

Arch Linux nabízí několik metod pro kompilaci kernelu.

##### Tradiční

Tradiční cesta je pravděpodobně nejjednodušší, ale ztrácíte možnost překompilování:[the traditional way](/index.php/Kernel_Compilation_From_Source "Kernel Compilation From Source") **or** [the traditional way for new users](/index.php/Kernel_Compilation_From_Source_For_New_Users_Guide "Kernel Compilation From Source For New Users Guide")

Tato metoda zahrnuje manuální stažení zdrojového tarballu a sestavení v domovském adresáři jako normální uživatel. Jedna konfigurační, dvě kompilační/instalační metody jsou dostupné; tradiční manuální metoda stejně dobře jako makepkg/pacman.

##### Použití Arch Build System

Je zde několik cest k automatizaci ABS v procesu sestavování svého kernelu. V současné době není žádný univerzální postup a můžete si vybrat postup, který Vám nejvíc sedne. Uvědomte si, že některé metody zahrnují úpravu PKGBUILD skriptu, proto je vhodné se seznámit s ABS na ostatních balíčcích před použitím k sestavování kernelu. Podívejte se [this thread](https://bbs.archlinux.org/viewtopic.php?id=66253) na fóru pro diskuze ohledně sestavování pomocí ABS..

*   První metoda je jednoduché použití skriptu z `/var/abs/core/kernel26`. Tatkto je oficiální kernel, ale uvědomte si, že tento PKGBUILD nebyl vytvořen s úpravami. Není to těžké upravit, pokud děláte malé úpravy.

*   Jsou zde dvě metody popsané na wiki pro použití abs: [Kernel Compilation with ABS](/index.php/Kernel_Compilation_with_ABS "Kernel Compilation with ABS") a [Custom Kernel Compilation with ABS](/index.php/Custom_Kernel_Compilation_with_ABS "Custom Kernel Compilation with ABS"). Obě mají odlišnou filozofii, tak si vyberte, která Vám bude vyhovovat.

*   Najděte uživatele, který navrhl balíček v AUR.

## Links

*   [O'Reilly - Linux Kernel in a Nutshell](http://www.kroah.com/lkn/) (free and opensource ebook covering configuration, installation and many more about the kernel)