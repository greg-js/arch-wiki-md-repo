**Dica:** Esta é parte de um artigo multi-páginas do "The Beginners' Guide" (O Guia para Iniciantes). **[Clique aqui](/index.php/Beginners%27_Guide_(Portugu%C3%AAs) "Beginners' Guide (Português)")** se preferir ler o artigo completo.

Este documento irá guiá-lo com o processo de instalação do [Arch Linux](/index.php/Arch_Linux "Arch Linux") usando o [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Antes de instalá-lo, é aconselhado que leia o [FAQ](/index.php/FAQ "FAQ").

A [ArchWiki](/index.php/Main_page "Main page") que é mantida pela comunidade, é o primeiro recurso que deve ser consultada se surgirem problemas. O [IRC Channel](/index.php/IRC_Channel "IRC Channel") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) e o [forums](https://bbs.archlinux.org/) também são excelentes recursos quando uma resposta não pode ser encontrada em outro lugar. Conforme [O Jeito Arch](/index.php/The_Arch_Way_(Portugu%C3%AAs) "The Arch Way (Português)"), você é encorajado a usar `man _command_` para ler a página `man` de qualquer comando que você não estiver familiarizado.

## Contents

*   [1 Prefácio](#Pref.C3.A1cio)
    *   [1.1 Introdução](#Introdu.C3.A7.C3.A3o)
    *   [1.2 Licença](#Licen.C3.A7a)
    *   [1.3 O Jeito Arch](#O_Jeito_Arch)
    *   [1.4 Sobre este Guia](#Sobre_este_Guia)

## Prefácio

### Introdução

Seja bem-vindo. Este documento irá guiá-lo através do processo de instalação do [Arch Linux](/index.php/Arch_Linux "Arch Linux"); uma simples, leve, distribuição [GNU](/index.php/GNU_Project "GNU Project")/Linux voltada para usuários competentes. Este guia é destinado para novos usuários Arch, mas se esforça para servir como uma forte referência e uma base informativa para todos.

Antes de instalar, a comunidade do Arch Linux aconselha o utilizador a ler o [FAQ](/index.php/FAQ "FAQ").

**Destaques da Distribuição Arch Linux:**

*   Design e filosofia [simples](/index.php/The_Arch_Way_(Portugu%C3%AAs) "The Arch Way (Português)").
*   [Todos os pacotes](https://www.archlinux.org/packages/?q=) são compilados para arquiteturas [i686](https://en.wikipedia.org/wiki/i686 "wikipedia:i686") e [x86_64](https://en.wikipedia.org/wiki/AMD64 "wikipedia:AMD64").
*   Modelo [rolling-release](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release"), permitindo instalar uma única vez e atualizar continuamente para a ultima versão estável dos programas instalados.
*   Gerenciador do sistema e serviços [systemd](/index.php/Arch_boot_process "Arch boot process"), compatível com scripts SysV e LSB.
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"): Um simples e dinâmico criador de [initramfs](https://en.wikipedia.org/wiki/RAM_drive "wikipedia:RAM drive").
*   Gerenciador de pacotes [Pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") é leve e ágil, com um consumo de memória muito modesto.
*   O [Sistema de Compilação Arch](/index.php/Arch_Build_System "Arch Build System"): Um sistema de construção de pacotes ao estilo _ports_ (*BSD), proporcionando um framework simples para criar pacotes de instalação Arch a partir do código-fonte.
*   O [Repositório de Usuários do Arch](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"): contém milhares de contribuições dos usuários de scripts de construção e a possibilidade de partilhar os seus próprios scripts.

### Licença

Arch Linux, pacman, documentação e scripts possuem copyright ©2002-2007 por Judd Vinet, ©2007-2011 por Aaron Griffin e são licenciados sobre a [GNU General Public License Versão 2](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

### O Jeito Arch

**_Os princípios de design por trás do Arch são destinados a mantê-lo [simples](/index.php/The_Arch_Way_(Portugu%C3%AAs) "The Arch Way (Português)")._**

'Simples', neste contexto, deverá significar 'sem acréscimos desnecessários, modificações ou complicações'. Em resumo, uma abordagem elegante e minimalista.

**Alguns pensamentos que você deve ter em mente para considerar a simplicidade:**

*   _" 'Simples' é definido a partir de um ponto de vista técnico, não de um ponto de vista da usabilidade. É melhor ser tecnicamente elegante, com uma curva de ensino superior, do que ser fácil de usar e tecnicamente [inferior]." -Aaron Griffin_
*   _Entia non sunt multiplicanda praeter necessitatem_ ou "Entidades não devem ser multiplicadas desnecessariamente." - A Navalha de Occam. O termo _navalha_ refere-se ao ato de cortar para longe complicações desnecessárias para se chegar a mais simples a explicação do método, ou teoria.
*   _"A parte extraordinária do [meu método] reside na sua simplicidade. A altura de cultivo corre sempre para a simplicidade."_ - Bruce Lee

### Sobre este Guia

O [Arch wiki](/index.php/Main_page "Main page") mantido pela comunidade é um recurso excelente e deve ser consultado para primeiras questões. O canal [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)), e o [fórum](https://bbs.archlinux.org/) também estão disponíveis, se a resposta não puder ser encontrada em outro lugar. Além disso, não se esqueça de verificar as páginas de `manual` para qualquer comando que você não estiver familiarizado; Isso geralmente pode ser invocado com `man _comando_`.

**Nota:** Seguindo este guia com cuidado é essencial para ter sucesso em instalar um sistema Arch Linux configurado corretamente, por isso _por favor_ leia atentamente. É altamente recomendado que você leia cada seção completamente <u>antes</u> de realizar quaisquer tarefas detalhadas.

O guia é dividido em 3 componentes principais:

*   [Parte I: Preparar a Instalação](/index.php/Beginners%27_Guide/Preparation_(Portugu%C3%AAs)#Prepare_the_Installation "Beginners' Guide/Preparation (Português)")
*   [Parte II: Instalar o sistema base](/index.php/Beginners%27_Guide/Installation_(Portugu%C3%AAs)#Install_the_Base_System "Beginners' Guide/Installation (Português)")
*   [Parte III: Extra](/index.php/Beginners%27_Guide/Extra_(Portugu%C3%AAs)#Post-Installation "Beginners' Guide/Extra (Português)")

**[Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide")**

* * *

**Prefácio** >> [Preparar a Instalação](/index.php/Beginners%27_Guide/Preparation_(Portugu%C3%AAs) "Beginners' Guide/Preparation (Português)") >> [Instalar o sistema base](/index.php/Beginners%27_Guide/Installation_(Portugu%C3%AAs) "Beginners' Guide/Installation (Português)") >> [Extras](/index.php/Beginners%27_Guide/Extra_(Portugu%C3%AAs) "Beginners' Guide/Extra (Português)")