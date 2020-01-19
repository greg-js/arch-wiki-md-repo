**Status de tradução:** Esse artigo é uma tradução de [System backup](/index.php/System_backup "System backup"). Data da última tradução: 2019-08-17\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=System_backup&diff=0&oldid=580157) na versão em inglês.

Artigos relacionados

*   [Programas de sincronização e backup](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")
*   [Manutenção do sistema#Backup](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Backup "Manutenção do sistema")
*   [Clonagem de disco](/index.php/Clonagem_de_disco "Clonagem de disco")
*   [Migrar instalação para novo hardware](/index.php/Migrate_installation_to_new_hardware "Migrate installation to new hardware")
*   [Recuperação de arquivos](/index.php/File_recovery "File recovery")

É importante fazer um backup regular dos dados do sistema e do usuário armazenados, por exemplo, em `/etc`, `/home`, `/var` e em instalações de servidores, também `/srv`.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Usando snapshots de Btrfs](#Usando_snapshots_de_Btrfs)
*   [2 Usando snapshots de LVM](#Usando_snapshots_de_LVM)
*   [3 Usando rsync](#Usando_rsync)
*   [4 Usando tar](#Usando_tar)
*   [5 Usando SquashFS](#Usando_SquashFS)
*   [6 Backup inicializável](#Backup_inicializável)
    *   [6.1 Atualizar o fstab](#Atualizar_o_fstab)
    *   [6.2 Atualizar o arquivo de configuração do gerenciador de boot](#Atualizar_o_arquivo_de_configuração_do_gerenciador_de_boot)
    *   [6.3 Primeira inicialização](#Primeira_inicialização)

## Usando snapshots de Btrfs

Veja [Btrfs#Snapshots](/index.php/Btrfs#Snapshots "Btrfs") e [Snapper](/index.php/Snapper "Snapper").

## Usando snapshots de LVM

Veja [LVM (Português)#Snapshots](/index.php/LVM_(Portugu%C3%AAs)#Snapshots "LVM (Português)") e [Criar snapshots do sistema de arquivos raiz com LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM").

## Usando rsync

Veja [rsync#As a backup utility](/index.php/Rsync#As_a_backup_utility "Rsync").

## Usando tar

Veja [Backup completo do sistema com tar](/index.php/Full_system_backup_with_tar "Full system backup with tar").

## Usando SquashFS

Veja [Backup completo do sistema com SquashFS](/index.php/Full_system_backup_with_SquashFS "Full system backup with SquashFS").

## Backup inicializável

Ter um backup inicializável pode ser útil caso o sistema de arquivos seja corrompido ou se uma atualização quebrar o sistema. O backup também pode ser usado como uma base de teste para atualizações, com o repositório *testing* habilitado, etc. Se você transferiu o sistema para uma partição ou unidade diferente e deseja inicializá-lo, o processo é tão simples quanto atualizar o backup do `/etc/fstab` e o arquivo de configuração do seu gerenciador de boot.

Esta seção pressupõe que você fez o backup do sistema em outra unidade ou partição, que seu carregador de inicialização atual está funcionando bem e que você deseja inicializar a partir do backup também.

### Atualizar o fstab

Sem reinicializar, edite o [fstab](/index.php/Fstab "Fstab") do backup comentando ou removendo todas as entradas existentes. Adicione uma entrada para a partição que contém o backup, como o exemplo aqui:

```
/dev/sda*X*    /             *ext4*      defaults                 0   1

```

Lembre-se de usar o nome do dispositivo e o tipo de sistema de arquivos adequados.

### Atualizar o arquivo de configuração do gerenciador de boot

Para [Syslinux](/index.php/Syslinux "Syslinux"), tudo o que você precisa fazer é duplicar a entrada atual, exceto apontar para uma unidade ou partição diferente.

**Dica:** Em vez de editar `syslinux.cfg`, você também pode editar temporariamente o menu durante a inicialização. Quando o menu aparecer, pressione a tecla `Tab` e altere as entradas relevantes. As partições são contadas a partir de uma, as unidades são contadas a partir de zero.

Para o [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)"), é recomendado que você [gere novamente o arquivo de configuração principal](/index.php/GRUB_(Portugu%C3%AAs)#Gerar_o_arquivo_de_configuração_principal "GRUB (Português)") automaticamente. Se você quiser instalar recentemente todos os arquivos do GRUB em algum lugar diferente de `/boot`, como `/mnt/newroot/boot`, use a opção `--boot-directory`.

Além disso, verifique a nova entrada no menu `/boot/grub/grub.cfg`. Certifique-se de que o UUID esteja correspondendo à nova partição, caso contrário, ele ainda pode inicializar o sistema antigo. Encontre o UUID de uma partição com [lsblk](/index.php/Lsblk_(Portugu%C3%AAs) "Lsblk (Português)"):

```
$ lsblk -no NAME,UUID /dev/sd*XY*

```

sendo que `/dev/sd*XY*` é a partição desejada (p.ex., `/dev/sdb3`). Para listar os UUIDs das partições que o GRUB acha que pode inicializar, use o *grep*:

```
# grep UUID= /boot/grub/grub.cfg

```

### Primeira inicialização

Reinicialize o computador e selecione a entrada correta no gerenciador de boot. Isso carregará o sistema pela primeira vez. Todos os periféricos devem ser detectados e as pastas vazias em `/` serão preenchidas.

Agora, você pode editar novamente o `/etc/fstab` para adicionar as partições e os pontos de montagem removidos anteriormente.