[PRoot](https://proot-me.github.io) é o programa que implementa funcionalidade similar ao [chroot](/index.php/Chroot_(Portugu%C3%AAs) "Chroot (Português)") do GNU/Linux, `mount --bind`, e binfmt_misc em espaço de usuário, permitindo que um usuário sem privilégios execute programas com um diretório raiz alternativo, muito parecido com a "jaula" do *chroot*. Isso é útil nos casos em que um chroot não é possível devido à falta de privilégios de root.

## Instalação

PRoot pode ser instalado pelo pacote [proot](https://aur.archlinux.org/packages/proot/). O *pacstrap* pode ser usado para inicializar o diretório com um ambiente Arch antes de executar *proot*.

## Uso

Após a instalação, PRoot não exige privilégios de root. Tal como acontece com o chroot, o PRoot deve receber um diretório para atuar como o novo diretório raiz do programa a ser executado. Se um programa não for especificado, o PRoot iniciará `/bin/sh` por padrão. Os sistemas de arquivos virtuais não precisam ser montados manualmente, pois PRoot lida com isso automaticamente.

```
proot -r ~/meuchroot/

```

Neste ponto, um shell começará, com `/` correspondente ao diretório `~/chroot/` no sistema hospedeiro.

Os caminhos podem estar explicitamente vinculados usando a opção `-b`:

```
proot -b /bin/bash:/bin/sh

```

Isso disponibiliza o /bin/bash do hospedeiro no /bin/sh do convidado

Internamente, o PRoot utiliza o emulador de modo de usuário [QEMU](/index.php/QEMU "QEMU") para permitir que os programas sejam executados dentro do PRoot mesmo quando eles são compilados para uma arquitetura diferente do sistema hospedeiro.

## Segurança

Assim como o chroot, o PRoot fornece apenas o isolamento a nível do sistema de arquivos. Os programas dentro da "jaula" do PRoot compartilham o mesmo kernel, hardware, espaço de processo e subsistema de rede. Chroot e PRoot não são projetados para serem substitos de aplicativos de [virtualização](/index.php/Virtualiza%C3%A7%C3%A3o "Virtualização") real, como hipervisores e paravirtualizadores.