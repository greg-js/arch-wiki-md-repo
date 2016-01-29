# Aura

**Aura** is a multilingual package manager for Arch Linux written in [Haskell](https://en.wikipedia.org/wiki/Haskell_(programming_language) "wikipedia:Haskell (programming language)"). It connects to both the official [ABS](/index.php/ABS "ABS") repositories and to the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), allowing easy control of all packages on an Arch system. It allows all pacman operations and provides new custom ones for dealing with [AUR](/index.php/AUR "AUR") packages. Aura caches built package files, so they can be managed like any ABS package would. This includes downgrading with `-C`.

See the [README](https://github.com/aurapm/aura/blob/master/README.md) and [documentation](https://github.com/aurapm/aura/tree/master/doc) for general information.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Binary Package](#Binary_Package)
    *   [1.2 Source Package](#Source_Package)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 AUR packages fail to build](#AUR_packages_fail_to_build)
    *   [2.2 Build failing at configuration step](#Build_failing_at_configuration_step)
    *   [2.3 Invalid argument](#Invalid_argument)
    *   [2.4 Auto-prompt for sudo](#Auto-prompt_for_sudo)
*   [3 See also](#See_also)

## Installation

### Binary Package

The easiest way to install aura without having to worry about Haskell dependencies is via the prebuilt [AUR](/index.php/AUR "AUR") binary package: [aura-bin](https://aur.archlinux.org/packages/aura-bin/)<sup><small>AUR</small></sup>.

**Note:** At the moment this only works for 64 bit architectures.

### Source Package

The [aura](https://aur.archlinux.org/packages/aura/)<sup><small>AUR</small></sup> source package requires Haskell packages which may be not available in the [official repositories](/index.php/Official_repositories "Official repositories") or [AUR](/index.php/AUR "AUR"). All of Aura's dependencies are however available in the _haskell-core_ repository. See [ArchHaskell#haskell-core](/index.php/ArchHaskell#haskell-core "ArchHaskell") on how to add _haskell-core_ as a repository.

## Troubleshooting

See [GitHub issues](https://github.com/aurapm/aura/issues) for known problems.

### AUR packages fail to build

See [List of AUR packages that don't build](https://github.com/aurapm/aura/issues/14).

### Build failing at configuration step

If you get the following:

```
Configuring aura-1.x.x.x...
Setup: At least the following dependencies are missing:
regex-pcre-builtin -any
```

Then you need to rebuild the [haskell-regex-pcre-builtin](https://www.archlinux.org/packages/?name=haskell-regex-pcre-builtin) AUR package, or install it out of [haskell-core]. This usually occurs after ghc upgrades, and has to do with ghc and all the haskell libraries being linked by special hash values for security purposes.

### Invalid argument

```
aura >> Determining dependencies...
aura: fd:6: hGetContents: invalid argument (invalid byte sequence)
```

This is a [known issue](https://github.com/aurapm/aura/issues/78) in 1.2.X and later versions. Make sure the [locale](/index.php/Locale "Locale") is configured correctly.

### Auto-prompt for sudo

Aura will not prompt for elevated privileges by default. If you'd like it do so (like some other AUR helpers) you can write a wrapper script to re-try aura with sudo when needed. The following creates a function `a` that wraps `aura`:

```
function a(){
    AURA="$(aura "$@")"

    if echo "$AURA" | grep -q '^aura >>= .*You have to use `.*sudo.*` for that.*$'
    then
        sudo aura "$@"
    else
        echo "$AURA"
    fi
}
```

Either add this function to your corresponding rc/profile or as a stand-alone script on your PATH.

## See also

*   [Aura's github page](https://github.com/fosskers/aura)
*   [Aura's ArchLinux forum post](https://bbs.archlinux.org/viewtopic.php?id=155778)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Aura&oldid=415585](https://wiki.archlinux.org/index.php?title=Aura&oldid=415585)"