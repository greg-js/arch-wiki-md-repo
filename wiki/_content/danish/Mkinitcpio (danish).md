**mkinitcpio** er den næste generation af initramfs skabelse.

En *initial ramdisk* er et midlertidigt filsystem som bruges til den første del af [systemstarten](/index.php?title=Boot_process_(Dansk)&action=edit&redlink=1 "Boot process (Dansk) (page does not exist)"). *initrd* og *initramfs* er to lidt forskellige metoder til at få denne fil ind i hukommelsen. Begge bruges almindeligvis til at lave forberedelser inde det rigtige rodfilsystem kan monteres.

## Overblik

mkinitcpio er et script skrevet i Bash, til at skabe et miljø til skabelse af denne første ramdisk.