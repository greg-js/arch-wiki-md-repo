## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 Configuração](#Configura.C3.A7.C3.A3o)

## Instalação

### BIOS

**Nota:** Para dispositivos particionados no formato GPT, em placas-mãe BIOS, o GRUB necessitará de uma "[Partição BIOS de boot](/index.php/GRUB#GPT_specific_instructions "GRUB")" de 2 MiB.

**Nota:** Por favor não utilize a nomenclatura `/dev/sda_X_` no comando abaixo. Você deve utilizar `/dev/sdb` se o Arch estiver instalado lá e se foi configurado na BIOS para que este seja o primeiro dispositivo na ordem de inicialização.

```
# pacman -S grub
# grub-install --target=i386-pc --recheck /dev/sda
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

### UEFI

**Nota:** Caso você possua um sistema EFI 32-bit, como os Macs de antes de 2008, instale o `grub-efi-i386` e use o `--target=i386-efi`.

```
# pacman -S grub-efi-x86_64 efibootmgr
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --recheck
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

Rode o próximo comando para criar a entrada do GRUB no menu da UEFI Veja [efibootmgr](/index.php/UEFI#efibootmgr "UEFI") para maiores informações.

```
# efibootmgr -c -g -d /dev/sdX -p Y -w -L "Arch Linux (GRUB)" -l '\\EFI\\arch_grub\\grubx64.efi'

```

## Configuração

Mesmo não havendo problemas na utilização de um `grub.cfg` gerado manualmente, é recomendado que iniciantes gerem tal arquivo automaticamente:

**Dica:** Para a busca automática de outros sistemas operacionais em seu computador, instale o pacote [os-prober](https://www.archlinux.org/packages/?name=os-prober) (`pacman -S os-prober`)antes de rodar o próximo comando.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```