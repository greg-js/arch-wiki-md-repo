**Aura** is a multilingual package manager for Arch Linux written in [Haskell](https://en.wikipedia.org/wiki/Haskell_(programming_language) "wikipedia:Haskell (programming language)"). It connects to both the [ABS](/index.php/ABS "ABS") and [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Aura caches built package files, so they can be managed like any ABS package would. This includes downgrading with `-C`.

See the [README](https://github.com/aurapm/aura/blob/master/README.md) and [documentation](https://github.com/aurapm/aura/tree/master/doc) for general information.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Binary Package](#Binary_Package)
    *   [1.2 Source Package](#Source_Package)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Auto-prompt for sudo](#Auto-prompt_for_sudo)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Build failing at configuration step](#Build_failing_at_configuration_step)
*   [4 See also](#See_also)

## Installation

### Binary Package

The easiest way to install aura without having to worry about Haskell dependencies is via the prebuilt [AUR](/index.php/AUR "AUR") binary package: [aura-bin](https://aur.archlinux.org/packages/aura-bin/).

**Note:** At the moment this only works for 64 bit architectures.

### Source Package

The [aura](https://aur.archlinux.org/packages/aura/) source package requires Haskell packages which may be not available in the [official repositories](/index.php/Official_repositories "Official repositories") or [AUR](/index.php/AUR "AUR"). All of Aura's dependencies are however available in the *haskell-core* repository. See [ArchHaskell#haskell-core](/index.php/ArchHaskell#haskell-core "ArchHaskell") on how to add *haskell-core* as a repository.

## Tips and tricks

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

## Troubleshooting

See [GitHub issues](https://github.com/aurapm/aura/issues) for known problems.

### Build failing at configuration step

If you get the following:

```
Configuring aura-1.x.x.x...
Setup: At least the following dependencies are missing:
regex-pcre-builtin -any
```

Then you need to rebuild the [haskell-regex-pcre-builtin](https://www.archlinux.org/packages/?name=haskell-regex-pcre-builtin) AUR package, or install it out of [haskell-core]. This usually occurs after ghc upgrades, and has to do with ghc and all the haskell libraries being linked by special hash values for security purposes.

## See also

*   [Aura's github page](https://github.com/fosskers/aura)
*   [Aura's ArchLinux forum post](https://bbs.archlinux.org/viewtopic.php?id=155778)