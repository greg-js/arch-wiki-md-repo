*Se você instalar o Arch com o sistema de arquivos ext2, é uma boa ideia para habilitar o journal e transferir para o sistema de arquivos ext3\. O Journal possui ótimos benefícios*

Precisa executar o comando:

```
tune2fs -j DRIVE 

```

Na /dev/discs/disc0/part1 ou /dev/hda1 por exemplo.

Note que depois de ter feito, **você precisa editar** no:

```
/etc/fstab

```

altere

```
ext2

```

para

```
ext3

```

na partição do sistemas de arquivos.

Então (no kernel padrão) precisará executar o comando para reconstruir a imagem do initrd.

```
mkinitcpio -p kernel26

```