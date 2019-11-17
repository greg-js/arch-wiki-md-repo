**Status de tradução:** Esse artigo é uma tradução de [TFTP](/index.php/TFTP "TFTP"). Data da última tradução: 2019-11-11\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=TFTP&diff=0&oldid=588141) na versão em inglês.

O [Trivial File Transfer Protocol](https://en.wikipedia.org/wiki/pt:Trivial_File_Transfer_Protocol "wikipedia:pt:Trivial File Transfer Protocol") (TFTP) fornece uma forma minimalista para transferir arquivos. É geralmente usado como uma parte da inicialização do [PXE](/index.php/PXE "PXE") ou para atualizar configuração ou firmware em dispositivos que possuem memória limitada, tal como roteadores, telefones IP e impressoras.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Servidor](#Servidor)
    *   [1.1 tftp-hpa](#tftp-hpa)
    *   [1.2 atftp](#atftp)
    *   [1.3 dnsmasq](#dnsmasq)
*   [2 Cliente](#Cliente)
    *   [2.1 tftp-hpa](#tftp-hpa_2)
    *   [2.2 curl](#curl)

## Servidor

Há várias implementações de servidor TFTP, algum deles estão listados abaixo e [iputils](https://www.archlinux.org/packages/?name=iputils) também inclui uma versão de tftp.

**Nota:** Certifique-se de não iniciar implementações diferentes de TFTP ao mesmo tempo. Eles vão falhar com um erro `got more than one socket`, pois apenas um pode escutar a porta TFTP padrão `69`.

### tftp-hpa

[Instale](/index.php/Instale "Instale") [tftp-hpa](https://www.archlinux.org/packages/?name=tftp-hpa) e então [inicie](/index.php/Inicie "Inicie") `tftpd.service`.

Para modificar parâmetros de serviço, edite `/etc/conf.d/tftpd`.

[tftp-hpa](https://www.archlinux.org/packages/?name=tftp-hpa) exige caminhos absolutos nas suas comunicações de tftp. Se o uso de caminhos absolutos não forem possíveis seja qual for o motivo, considere usar [atftp](https://www.archlinux.org/packages/?name=atftp).

### atftp

[Instale](/index.php/Instale "Instale") [atftp](https://www.archlinux.org/packages/?name=atftp) e então [inicie](/index.php/Inicie "Inicie") `atftpd.service`.

Para modificar parâmetros de serviço, edite `/etc/conf.d/atftpd`.

### dnsmasq

Veja [dnsmasq (Português)#Servidor TFTP](/index.php/Dnsmasq_(Portugu%C3%AAs)#Servidor_TFTP "Dnsmasq (Português)").

## Cliente

### tftp-hpa

[Instale](/index.php/Instale "Instale") [tftp-hpa](https://www.archlinux.org/packages/?name=tftp-hpa) e então use *tftp* pelo seu dia!

```
$ tftp

```

### curl

O [curl](https://www.archlinux.org/packages/?name=curl) padrão possui a habilidade de conectar a um servidor TFTP e colocar um arquivo por meio de:

```
$ curl -T ARQUIVO tftp://HOST

```