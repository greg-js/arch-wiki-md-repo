Se você deseja copiar alguns pacotes do Arch Linux para outro (por exemplo, com uma conexão lenta de internet), pode personalizar um CD, faça o seguinte:

*   Crie um respositório de pacotes usando o gensyc [Custom local repository with ABS and gensync](/index.php/Custom_local_repository_with_ABS_and_gensync "Custom local repository with ABS and gensync"). Copiando os pacotes para `/var/cache/pacman/pkg` para atualização do sistema Arch Linux.

*   Crie uma ISO de repositório CD-R ou CD-RW.

*   Monte o CD no computador desejado.

*   Adicione um repositório personalizado para `/etc/pacman.conf`:

```
 [mycd]
 Server = file:///mnt/cd/pkg

```

Outra opção simples é copiar os arquivos do CD para `/var/cache/pacman/pkg` no computador desejado. O Pacman será possível recupear os pacotes instalados sem utilizar a conexão, se os arquivos forem atualizados.

Possui outra opção [create a custom install CD](https://bbs.archlinux.org/viewtopic.php?id=1387).