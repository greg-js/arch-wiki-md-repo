Artigos relacionados

*   [CD Burning](/index.php/CD_Burning "CD Burning")
*   [Archiso](/index.php/Archiso "Archiso")
*   [Multiboot USB drive](/index.php/Multiboot_USB_drive "Multiboot USB drive")

##### Método *nix

Insira um dispositivo flash vazio ou expansível, determine o seu caminho, e grave o ISO para o dispositivo com o programa `dd`:

 `# dd if=archlinux-2010.05-''{core|netinstall}''-''{i686|x86_64|dual}''.iso of=/dev/sd''x''` 

onde `if=` é o caminho para o arquivo .iso e `of=` é o seu dispositivo flash. Certifique-se de usar `/dev/sd**x**` e não `/dev/sd**x1**`. Você vai precisar de um dispositivo de memória flash grande o suficiente para acomodar a imagem.

Para verificar se a imagem foi gravada com sucesso no dispositivo flash, tome nota do número de registros (blocos) lidos e gravados, e em seguida, realizar a operação a seguir:

 ` $ dd if=/dev/sd''x'' count=''número_de_registros'' status=noxfer | md5sum` 

O retorno do md5sum deve coincidir com o [md5sum do arquivo de imagem archlinux baixado (2010.05)](ftp://ftp.archlinux.org/iso/2010.05/md5sums.txt); ambas devem combinar o md5sum da imagem conforme listado no arquivo md5sums no espelho do site de distribuição. Um processo normal será parecido com este:

 `$ [sudo] dd if=archlinux-2010.05-core-i686.iso of=/dev/sdc #Grava o .iso no drive` 
```
 744973+0 records in
 744973+0 records out
 381426176 bytes (381 MB) copied, 106.611 s, 3.6 MB/s

```
 `$ [sudo] dd if=/dev/sdc count=744973 status=noxfer | md5sum #Verifica a integridade` 
```
 4850d533ddd343b80507543536258229  -
 744973+0 records in
 744973+0 records out
```

Continue em [Inicializar o Instalador Arch Linux](#Inicializar_o_Instalador_Arch_Linux)

##### Método para Microsoft Windows

Baixe o "Disk Imager" a partir de [https://launchpad.net/win32-image-writer/+download](https://launchpad.net/win32-image-writer/+download). Insira a mídia flash. Inicie o Disk Imager e selecione o arquivo de imagem (Disk Imager só aceita arquivos *.IMG, então você tem que colocar "*.iso" no diálogo de abrir arquivo para selecionar o instantâneo do Arch). Selecione a letra da unidade associada à unidade flash. Clique em "write" (gravar).

Existem também outras soluções para a [gravação de imagens ISO bootáveis para pen-drives USB](/index.php/Install_from_a_USB_flash_drive#On_Windows "Install from a USB flash drive"). Se você tiver problemas com desconexão de pen-drives USB, tente usar outra porta USB e/ou cabo.

Continue em [Inicializar o Instalador Arch Linux](#Inicializar_o_Instalador_Arch_Linux)