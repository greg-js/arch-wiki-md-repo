**Status de tradução:** Esse artigo é uma tradução de [pkgstats](/index.php/Pkgstats "Pkgstats"). Data da última tradução: 2019-06-28\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Pkgstats&diff=0&oldid=576131) na versão em inglês.

pkgstats envia uma lista de todos os pacotes instalados, a arquitetura e o *mirror* que você está usando para o projeto do Arch Linux. Essa informação é anônima e não pode ser usada para identificar o usuário, porém vai ajudar os desenvolvedores do Arch a priorizar seus esforços ([código-fonte](https://git.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/pkgstats)).

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [pkgstats](https://www.archlinux.org/packages/?name=pkgstats).

## Uso

*pkgstats* é configurado para executar automaticamente toda semana usando [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"). Uma vez instalado, ele será ativado após a próxima reinicialização.

Se você não deseja esperar por um ciclo de reinicialização, você pode [iniciar](/index.php/Inicie "Inicie") manualmente o `pkgstats.timer`.

*pkgstats* também pode ser executado manualmente: veja `pkgstats -h` para informações de uso.

## Resultados e referência

Estatísticas e documentação estão disponíveis em [https://pkgstats.archlinux.de/](https://pkgstats.archlinux.de/).

O projeto código aberto a seguir permite que você obtenha dados estatísticos como JSON: [ArchLinuxPkgStatsScraper](https://github.com/chrissound/ArchLinuxPkgStatsScraper), bem como um front-end web para comparar os dados está disponível: [https://trycatchchris.co.uk/archpackagecompare/](https://trycatchchris.co.uk/archpackagecompare/comparePackage/gnome-terminal/lxterminal/rxvt/rxvt-unicode/st/terminator/termite/xterm).

Você pode ler a [discussão oficial no fórum](https://bbs.archlinux.org/viewtopic.php?id=105431) para mais informações.