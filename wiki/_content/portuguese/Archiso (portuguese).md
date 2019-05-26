**Status de tradução:** Esse artigo é uma tradução de [Archiso](/index.php/Archiso "Archiso"). Data da última tradução: 2019-05-23\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Archiso&diff=0&oldid=571877) na versão em inglês.

Artigos relacionados

*   [Remasterizando a ISO de Instalação](/index.php/Remastering_the_Install_ISO "Remastering the Install ISO")
*   [Archiso como servidor pxe](/index.php/Archiso_as_pxe_server "Archiso as pxe server")
*   [Archboot](/index.php/Archboot "Archboot")
*   [Instalação offline](/index.php/Offline_installation "Offline installation")

**Archiso** é um pequeno conjunto de scripts bash capazes de construir imagens em CD/DVD/USB Live totalmente funcionais do Arch Linux. É a mesma ferramenta usada para gerar as imagens oficiais, mas como é uma ferramenta muito genérica, pode ser usada para gerar qualquer coisa desde sistemas de resgate, discos de instalação, até sistemas de CD/DVD/USB Live, e quem sabe o que outro. Simplificando, se envolve Arch em uma montanha russa brilhante, pode fazê-lo. O coração e a alma de Archiso são *mkarchiso*. Todas as suas opções estão documentadas em sua saída de uso, portanto, seu uso direto não será coberto aqui. Em vez disso, este artigo da wiki funcionará como um guia para rolar sua própria mídia ao vivo em pouco tempo!

Se você precisar de um detalhamento técnico dos requisitos e das etapas de criação, consulte também a [documentação oficial do projeto](https://git.archlinux.org/archiso.git/tree/docs).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuração](#Configuração)
*   [2 Configurar a mídia live](#Configurar_a_mídia_live)
    *   [2.1 Instalando pacotes](#Instalando_pacotes)
        *   [2.1.1 Repositório local personalizado](#Repositório_local_personalizado)
        *   [2.1.2 Impedindo a instalação de pacotes pertencentes ao grupo base](#Impedindo_a_instalação_de_pacotes_pertencentes_ao_grupo_base)
        *   [2.1.3 Instalando pacotes do multilib](#Instalando_pacotes_do_multilib)
    *   [2.2 Adicionando arquivos à imagem](#Adicionando_arquivos_à_imagem)
    *   [2.3 Gerenciador de boot](#Gerenciador_de_boot)
        *   [2.3.1 Secure Boot do UEFI](#Secure_Boot_do_UEFI)
    *   [2.4 Gerenciador de login](#Gerenciador_de_login)
    *   [2.5 Alterando login automático](#Alterando_login_automático)
*   [3 Compilando a ISO](#Compilando_a_ISO)
    *   [3.1 Recompilar a ISO](#Recompilar_a_ISO)
*   [4 Usando a ISO](#Usando_a_ISO)
*   [5 Veja também](#Veja_também)
    *   [5.1 Documentação e tutoriais](#Documentação_e_tutoriais)
    *   [5.2 Exemplo de modelo para personalização](#Exemplo_de_modelo_para_personalização)
    *   [5.3 Criando uma ISO de instalação offline](#Criando_uma_ISO_de_instalação_offline)
    *   [5.4 Encontrar uma versão anterior de uma imagem ISO](#Encontrar_uma_versão_anterior_de_uma_imagem_ISO)

## Configuração

**Nota:** Recomenda-se atuar como root em todas as etapas a seguir. Caso contrário, é muito provável que tenha problemas com permissões falsas mais tarde.

Antes de começar, [instale](/index.php/Instale "Instale") o pacote [archiso](https://www.archlinux.org/packages/?name=archiso) ou [archiso-git](https://aur.archlinux.org/packages/archiso-git/).

O Archiso vem com dois "perfis": *releng* e *baseline*.

*   Se você deseja criar uma versão live totalmente personalizada do Arch Linux, pré-instalada com todos os seus programas e configurações favoritos, use *releng*. Esse perfil também é usado para compilar ISO oficiais do Arch Linux.

*   Se você quer apenas criar a mídia *live* mais básica, sem pacotes pré-instalados e uma configuração minimalista, use *baseline*.

Agora copie o perfil de sua escolha para um diretório (*archlive*, no exemplo abaixo) onde você pode fazer ajustes e compilá-lo. Execute o seguinte, substituindo `**perfil**` por `releng` ou `baseline`.

```
# cp -r /usr/share/archiso/configs/**perfil**/*archlive*

```

*   Se você estiver usando o perfil `releng` para criar uma imagem totalmente personalizada, poderá prosseguir para [#Configurar a mídia live](#Configurar_a_mídia_live).

*   Se você estiver usando o perfil `baseline` para criar uma imagem simples ou `releng` para replicar uma ISO oficial, não precisará fazer nenhuma personalização e prosseguir para [#Compilando a ISO](#Compilando_a_ISO).

## Configurar a mídia live

Esta seção detalha a configuração da imagem que você criará, permitindo que você defina os pacotes e as configurações que deseja que sua imagem live contenha.

Dentro do diretório `*archlive*` criado em [#Configuração](#Configuração), há vários arquivos e diretórios. Estamos preocupados apenas com alguns deles, principalmente:

*   `packages.x86_64` - é aqui que você lista, linha por linha, os pacotes que deseja instalar e
*   o diretório `airootfs` - esse diretório age como uma sobreposição e é onde você faz todas as personalizações.

Geralmente, cada tarefa administrativa que você faria normalmente após uma nova instalação, exceto a instalação do pacote, pode ser colocada no script `*archlive*/airootfs/root/customize_airootfs.sh`. Tem que ser escrito a partir da perspectiva do novo ambiente, então `/` no script significa a raiz da iso live a ser criada.

### Instalando pacotes

Edite as listas de pacotes em `packages.x86_64` para indicar quais pacotes estão instalados na mídia live.

**Nota:** Se você quiser usar um [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela") no Live CD, deverá adicionar os [drivers de vídeo](/index.php/Video_drivers "Video drivers") necessários e corretos, ou o gerenciador de janela poderá congelar durante o carregamento.

#### Repositório local personalizado

Para o propósito de preparar pacotes ou pacotes personalizados a partir de [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") / [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)"), você também pode [criar um repositório local personalizado](/index.php/Reposit%C3%B3rio_local_personalizado "Repositório local personalizado").

Você pode então adicionar seu repositório colocando o seguinte em `~/archlive/pacman.conf`, acima das outras entradas do repositório (para prioridade máxima):

 `~/archlive/pacman.conf` 
```
...
# repositório personalizado
[customrepo]
SigLevel = Optional TrustAll
Server = file:///home/**usuário**/customrepo/$arch
...
```

#### Impedindo a instalação de pacotes pertencentes ao grupo base

Por padrão, `/usr/bin/mkarchiso`, um script usado por `~/archlive/build.sh`, chama um dos [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) chamados `pacstrap` sem a opção `-i`, que faz com que o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") não aguardar por entrada de usuário durante o processo de instalação.

Ao colocar os pacotes do grupo base na lista negra adicionando-os à linha `IgnorePkg` em `~/archlive/pacman.conf`, o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") pergunta se eles ainda devem ser instalados, o que significa que eles quando eles forem, a entrada do usuário é ignorada. Para se livrar desses pacotes, existem várias opções:

*   **Suja**: Adicionar a opção `-i` a cada linha chamando `pacstrap` no `/usr/bin/mkarchiso`.

*   **Limpa**: Criar uma cópia de `/usr/bin/mkarchiso` na qual você adiciona a opção e adapta `~/archlive/build.sh` de forma que ela chama a versão modificada do script mkarchiso.

*   **Avançado**: Criar uma função para `~/archlive/build.sh` que remova explicitamente os pacotes após a instalação base. Isso deixaria o conforto de não ter que digitar muito durante o processo de instalação.

#### Instalando pacotes do multilib

Para instalar pacotes do repositório [multilib](/index.php/Multilib_(Portugu%C3%AAs) "Multilib (Português)"), simplesmente remova o comentário do repositório em `~/archlive/pacman.conf`:

 `pacman.conf` 
```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist
```

### Adicionando arquivos à imagem

**Nota:** Você deve ser root para fazer isso, não altere a propriedade de nenhum dos arquivos que você copiou, **tudo** dentro do diretório airootfs deve ser propriedade da raiz. As propriedades apropriadas serão resolvidas em breve.

O diretório airootfs atua como uma sobreposição, pense nele como o diretório raiz '/' em seu sistema atual, portanto, todos os arquivos que você colocar dentro deste diretório serão copiados na inicialização.

Então, se você tem um conjunto de scripts do iptables em seu sistema atual que deseja usar na imagem ao vivo, copie-os da seguinte forma:

```
# cp -r /etc/iptables ~/archlive/airootfs/etc

```

Colocar arquivos no diretório inicial dos usuários é um pouco diferente. Não os coloque dentro de `airootfs/home`, mas crie um diretório skel dentro de `airootfs/` e coloque-os lá. Em seguida, adicionaremos os comandos relevantes ao `customize_airootfs.sh` que usaremos para copiá-los durante a inicialização e classificar as permissões.

Primeiro, cria o diretório skel:

```
# mkdir ~/archlive/airootfs/etc/skel

```

Agora, copie os arquivos 'home' para o diretório skel, por exemplo, para `.bashrc`:

```
# cp ~/.bashrc ~/archlive/airootfs/etc/skel/

```

Quando `~/archlive/airootfs/root/customize_airootfs.sh` é executado e um novo usuário é criado, os arquivos do diretório skel serão automaticamente copiados para a nova pasta base, com as permissões definidas corretamente.

Da mesma forma, alguns cuidados são necessários para arquivos de configuração especiais que residem em algum ponto da hierarquia. Como um exemplo, o arquivo de configuração `/etc/X11/xinit/xinitrc` reside em um caminho que pode ser sobrescrito pela instalação de um pacote. Para colocar o arquivo de configuração deve-se colocar o `xinitrc` personalizado em `~/archlive/airootfs/etc/skel/` e então modificar `customize_airootfs.sh` para movê-lo adequadamente.

### Gerenciador de boot

O arquivo padrão deve funcionar bem, então você não precisa tocá-lo.

Devido à natureza modular do isolinux, você pode usar muitos addons, pois todos os arquivos *.c32 são copiados e disponibilizados para você. Dê uma olhada no [site oficial do syslinux](http://syslinux.zytor.com/wiki/index.php/SYSLINUX) e no [repositório git do archiso](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-). Utilizando os referidos addons, é possível fazer menus visualmente atraentes e complexos. Veja [aqui](http://syslinux.zytor.com/wiki/index.php/Comboot/menu.c32).

#### Secure Boot do UEFI

Se você deseja tornar seu Archiso inicializável em um ambiente ativado pelo UEFI Secure Boot, você deve usar um gerenciador de boot assinado. Você pode seguir as instruções em [Secure Boot#Booting an install media](/index.php/Secure_Boot#Booting_an_install_media "Secure Boot").

### Gerenciador de login

O início do X na inicialização do sistema é feita ativando o serviço [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") do gerenciador de login. Se você souber qual arquivo .service precisa de um link de software: Ótimo. Caso contrário, você pode descobrir facilmente caso esteja usando o mesmo programa no sistema em que você criou sua iso. Apenas use:

```
$ ls -l /etc/systemd/system/display-manager.service

```

Agora, crie o mesmo link em `~/archlive/airootfs/etc/systemd/system`. Para LXDM:

```
# ln -s /usr/lib/systemd/system/lxdm.service ~/archlive/airootfs/etc/systemd/system/display-manager.service

```

Isso vai habilitar LXDM na inicialização do sistema em seu sistema live.

Alternativamente, você pode simplesmente habilitar o serviço em `airootfs/root/customize_airootfs.sh` junto com outros serviços que estão habilitados lá.

Se você deseja que o ambiente gráfico inicie automaticamente durante a inicialização, certifique-se de editar `airootfs/root/customize_airootfs.sh` e substituir

```
systemctl set-default multi-user.target

```

com

```
systemctl set-default graphical.target

```

### Alterando login automático

A configuração para o login automático do getty está localizada em `airootfs/etc/systemd/system/getty@tty1.service.d/autologin.conf`.

Você pode modificar este arquivo para alterar o usuário de login automático:

```
[Service]
ExecStart=
ExecStart=-/sbin/agetty --autologin **isouser** --noclear %I 38400 linux

```

Ou remova-o completamente para desativar o login automático.

## Compilando a ISO

Agora você está pronto para transformar seus arquivos no .iso que você pode gravar em CD ou USB.

Dentro de `~/archlive`, execute:

```
# ./build.sh -v

```

O script agora baixará e instalará os pacotes que você especificou para `work/*/airootfs`, criará o kernel e iniciará as imagens, aplicará suas personalizações e, finalmente, compilará a iso em `out/`.

### Recompilar a ISO

Recompilar a iso após modificações não é oficialmente suportado. No entanto, é facilmente possível através da aplicação de dois passos. Primeiro você tem que remover os arquivos de bloqueio no diretório de trabalho:

```
# rm -v work/build.make_*

```

Se você editou `airootfs/root/customize_airootfs.sh` para criar um usuário sem privilégios, a recompilação falhará ao criá-lo porque o usuário já existirá ([FS#41865](https://bugs.archlinux.org/task/41865)). Para evitar esse problema, você precisa verificar se o usuário existe antes de executar `useradd`, por exemplo, executando `id`:

```
! id arch && useradd -m -p "" -g users -G "adm,audio,floppy,log,network,rfkill,scanner,storage,optical,power,wheel" -s /usr/bin/zsh arch

```

Também remova dados persistentes, como usuários criados ou links simbólicos, como `/etc/sudoers`.

As recompilações podem ser aceleradas ligeiramente editando o script pacstrap (localizado em /bin/pacstrap) e alterando o seguinte na linha 361:

Antes:

```
if ! pacman -r "$newroot" -Sy "${pacman_args[@]}"; then

```

Após:

```
if ! pacman -r "$newroot" -Sy --needed "${pacman_args[@]}"; then

```

Isso aumenta a velocidade do *bootstrap* inicial, já que ele não precisa baixar e instalar nenhum dos pacotes base que já estão instalados.

## Usando a ISO

Veja o artigo [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação") para várias opções.

## Veja também

### Documentação e tutoriais

*   [Página do projeto Archiso](https://projects.archlinux.org/archiso.git)
*   [Documentação oficial](https://projects.archlinux.org/archiso.git/tree/docs)

### Exemplo de modelo para personalização

*   [Uma distribuição DJ live rodando ArchLinux e compilada com Archiso](http://easy.open.and.free.fr/didjix/)

### Criando uma ISO de instalação offline

*   [Archiso offline](/index.php/Archiso_offline_(Portugu%C3%AAs) "Archiso offline (Português)")

### Encontrar uma versão anterior de uma imagem ISO

*   [Arch Linux Archive](/index.php/Arch_Linux_Archive_(Portugu%C3%AAs) "Arch Linux Archive (Português)")