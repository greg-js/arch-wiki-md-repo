[Android Debug Bridge](https://developer.android.com/studio/command-line/adb) (ADB) é uma ferramenta de linha de comando para instalar, desinstalar e debugar apps, transferir arquivos e acessar a console de um dispositivo.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Utilização](#Utiliza.C3.A7.C3.A3o)
    *   [2.1 Conectando um dispositivo](#Conectando_um_dispositivo)
    *   [2.2 Descobrindo IDs de Dispositivo](#Descobrindo_IDs_de_Dispositivo)
    *   [2.3 Adicionando regras no udev](#Adicionando_regras_no_udev)
    *   [2.4 Configurando o ADB](#Configurando_o_ADB)
    *   [2.5 Detectando o Dispositivo](#Detectando_o_Dispositivo)
    *   [2.6 Transferindo arquivos](#Transferindo_arquivos)
*   [3 Compilação de ferramentas ADB](#Compila.C3.A7.C3.A3o_de_ferramentas_ADB)
*   [4 Resolução de problemas](#Resolu.C3.A7.C3.A3o_de_problemas)

## Instalação

ADB faz parte das Ferramentas de Plataforma do [pacote SDK](/index.php/Android#SDK_packages "Android") e do pacote [android-tools](https://www.archlinux.org/packages/?name=android-tools).

## Utilização

### Conectando um dispositivo

**Tip:**

*   Alguns dispositivos precisam estar com o modo MTP habilitado para o ADB funcionar. Outros necessitam do modo PTP habilitado.
*   Regras [udev](/index.php/Udev "Udev") específicas de vários dispositivos estão incluídas no pacote [libmtp](https://www.archlinux.org/packages/?name=libmtp) então, se você tiver instalado este, os passos adiante podem ser desnecessários.
*   Certifique-se que seu cabo USB é capaz de carregar e transferir dados simultaneamente. Alguns cabos USB distribuídos com dispositivos móveis não possuem o pino de dados no cabo.

Para conectar um dispositivo ou telefone através do ADB no Arch você precisa:

1.  Talvez instalar o pacote [android-udev](https://www.archlinux.org/packages/?name=android-udev) caso você deseje conectar no dispositivo através de uma entrada no `/dev/`.
2.  Conectar seu dispositivo na USB.
3.  Habilitar USB Debugging(ou depuração USB) nas configurações do seu dispositivo:
    *   Jelly Bean (4.2) ou versões mais recentes: Acesse *Configurações > Sobre o Dispositivo* toque 7 vezes em *Número de Versão ou Versão de Compilação* até que uma popup apareça avisando que você ativou o modo desenvolvedor. Vá então para *Configurações > Opções do desenvolvedor > Depuração USB* e habilite esta opção. O dispositivo irá perguntar se você deseja aceitar a conexão vinda do computador. Para permitir permanentemente copie o arquivo `$HOME/.android/adbkey.pub` no caminho `/data/misc/adb/adb_keys` do dispositivo.
    *   Versões anteriores: Normalmente é feito em *Configurações > Aplicativos > Desenvolvimento > Depuração USB*. Reinicie o telefone para garantir que a depuração USB está habilitada.

Caso o comando (`adb devices` [reconheça seu dispositivo](#Detectando_o_Dispositivo) exibindo `"device" e não "unauthorized"` ou se estiver visível pela sua IDE, está feito. Caso contrário siga as instruções abaixo.

### Descobrindo IDs de Dispositivo

Cada dispositivo Android possui um ID de fabricante e produto (vendor/product). Exemplo do HTC Evo:

```
vendor id: 0bb4
product id: 0c8d

```

Conecte seu dispositivo e execute:

```
$ lsusb

```

Uma saída similar a esta deverá ser exibida

```
Bus 002 Device 006: ID 0bb4:0c8d High Tech Computer Corp.

```

### Adicionando regras no udev

Utilize as regras do pacote [android-udev](https://www.archlinux.org/packages/?name=android-udev) (ou [android-udev-git](https://aur.archlinux.org/packages/android-udev-git/)), instale as regras manualmente do [Android developer](https://source.android.com/source/initializing#configuring-usb-access), ou utilize o seguinte modelo para suas [regras udev](/index.php/Udev_rules "Udev rules") substituindo `[VENDOR ID]` e and `[PRODUCT ID]` pelos do seu dispositivo. Copie estas regras para `/etc/udev/rules.d/51-android.rules`:

 `/etc/udev/rules.d/51-android.rules` 
```
SUBSYSTEM=="usb", ATTR{idVendor}=="[VENDOR ID]", MODE="0660", GROUP="adbusers"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_adb"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_fastboot"

```

Para reiniciar as regras do udev execute:

```
# udevadm control --reload-rules

```

Certifique-se que você faz parte do [grupo](/index.php/Users_and_groups_(Portugu%C3%AAs)#Gerenciamento_de_grupo "Users and groups (Português)") `adbusers` para ter acesso a dispositivos `adb`.

### Configurando o ADB

O invés de criar regras no udev, você pode criar/editar o arquivo `~/.android/adb_usb.ini` que contém a lista dos vendor IDs;

 `~/.android/adb_usb.ini` 
```
0x27e8

```

### Detectando o Dispositivo

Após configurar as regras no udev, desconecte e reconecte seu dispositivo.

Então, execute:

```
$ adb devices

```

uma saída similar a esta será exibida:

```
List of devices attached 
HT07VHL00676    device

```

### Transferindo arquivos

Usando o adb você pode transferir arquivos entre o dispositivo e o seu computador. Para transferir arquivos para o dispositivo, execute

```
$ adb push *<o-que-copiar>* *<onde-por>*

```

E para puxar arquivos do dispositivo, execute

```
$ adb pull *<o-que-puxar>* *<diretório-local>*

```

Veja também [#Compilação de ferramentas ADB](#Compila.C3.A7.C3.A3o_de_ferramentas_ADB).

## Compilação de ferramentas ADB

*   [adbfs-rootless-git](https://aur.archlinux.org/packages/adbfs-rootless-git/) - Sistema de arquivos [FUSE](/index.php/FUSE "FUSE") utilizando o protocolo ADB
*   [adb-sync](https://github.com/google/adb-sync) (disponível em [adb-sync-git](https://aur.archlinux.org/packages/adb-sync-git/)) - ferramenta para sincronizar arquivos entre o computador e um dispositivo Android através do protocolo ADB.
*   [AndroidScreencast](http://xsavikx.github.io/AndroidScreencast) (disponível em [androidscreencast-bin](https://aur.archlinux.org/packages/androidscreencast-bin/)) – visualizar e controlar seu dispositivo Android do computador (protocolo ADB).

## Resolução de problemas

*   Caso você receba uma lista vazia (your device is not there), você não habilitou a Depuração USB no seu dispositivo. Faça isto acessando *Configurações > Aplicativos > Desenvolvimento* e habilitando a opção Depuração USB. No Android 4.2 (Jelly Bean) o menu "Opções do desenvolvedor" é oculto; para habilitar vá em *Configurações > Sobre o Dispositivo* toque 7 vezes em *Número de Versão ou Versão de Compilação*.

*   No Moto E, o dispositivo pode ter vendor/product IDs diferentes nos modos fastboot e sideload; se você receber o erro "no permission" verifique tais IDs utilizando o comando `lsusb`.