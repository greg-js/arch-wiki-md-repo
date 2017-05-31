pkgstats envia uma lista de todos os pacotes instalados, [módulos de kernel](https://www.archlinux.org/news/pkgstats-now-collects-modules-usage/), a arquitetura e o *mirror* que você está usando para o projeto do Arch Linux. Essa informação é anônima e não pode ser usada para identificar o usuário, porém vai ajudar os desenvolvedores do Arch a priorizar seus esforços ([código-fonte](https://git.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/pkgstats)).

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [pkgstats](https://www.archlinux.org/packages/?name=pkgstats).

## Uso

*pkgstats* é configurado para executar automaticamente toda semana usando [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"). Uma vez instalado, ele será ativado após a próxima reinicialização.

Se você não deseja esperar por um ciclo de reinicialização, você pode [iniciar](/index.php/Start "Start") manualmente o `pkgstats.timer`.

*pkgstats* também pode ser executado manualmente: veja `pkgstats -h` para informações de uso.

## Resultados e referência

Estatísticas estão disponíveis em [https://www.archlinux.de/?page=Statistics](https://www.archlinux.de/?page=Statistics).

O projeto código aberto a seguir permite que você obtenha dados estatísticos como JSON: [ArchLinuxPkgStatsScraper](https://github.com/chrissound/ArchLinuxPkgStatsScraper)

Você pode ler a [discussão oficial no fórum](https://bbs.archlinux.org/viewtopic.php?id=105431) para mais informações.