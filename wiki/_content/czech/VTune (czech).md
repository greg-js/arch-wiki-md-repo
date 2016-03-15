Instalace Intel VTune 9.1 na Arch Linux

## Instalace VTune

*   stáhněte si VTune
*   stáhněte si [patch](http://archlinux-stuff.googlecode.com/files/vtune-linux-9.1-arch.patch.gz)
*   rozbalte archív s VTune a proveďte patch souborů
*   nainstalujte [rpm4](https://aur.archlinux.org/packages/rpm4/) nebo [rpm4 ze sergejova repozitáře](http://arch.pp.ru/sergej-repo/)
*   proveďte příkaz

```
# rpm --initdb

```

*   a spusťte VTune instalátor

## Instalace ovladače

(VTune nefunguje na jádře verze 2.6.31, takže budete nejspíš potřebovat nainstalovat kernel26-lts)

*   stáhněte si [patch](http://archlinux-stuff.googlecode.com/files/vtune-linux-9.1-driver.patch.gz)
*   zkopírujte zdrojové kódy ovladače z /opt/intel/vtune/vdk/src do nového adresáře a opatchujte je.
*   proveďte příkaz

```
# ./configure
# make

```

*   *   jestliže kompilace selže chybovou zprávou 'the frame size of 1140 bytes is larger than 1024 bytes', přidejte volbu -Wframe-larger-than=2048 do EXTRA_CFLAGS v Makefile souboru
*   zkopírujte modul do adřesáře s jadernými moduly

```
# cp vtune_drv*.ko /lib/modules/misc/vtune_drv.ko

```

*   proveďte

```
# depmod -AeF /boot/System.map26

```

*   a aktivujte jaderný modul

```
# modprobe vtune_drv

```

*   Co se týče jádra verze 2.6.31, je zde změna v API. find_task_by_pid_ns() není nalezena. Jediná možnost jak to napravit, je vrátit se na verzi jádra 2.6.30 nebo počkat až Intel aktualizuje zdrojový kód ovladače. Pokud by měl někdo patch, který tento problém vyřeší, přidejte ho sem na Wiki.