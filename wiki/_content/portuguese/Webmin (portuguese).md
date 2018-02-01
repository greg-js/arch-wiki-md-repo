Do projeto [Webmin](http://www.webmin.com/):

	Webmin é uma interface baseada em web para administração de sistemas para Unix. Utilizando qualquer navegador moderno, você pode configurar contas de usuários, Apache, DNS, compartilhamento de arquivos e muito mais. Webmin remove a necessidade de editar manualmente arquivos de configuração Unix como `/etc/passwd`, e permite que você gerencie o um sistema de um console ou remotamente. Veja a página [standard modules](http://www.webmin.com/standard.html) para uma lista de todas as funções incluídas no Webmin, ou confira os [screenshots](http://www.webmin.com/demo.html).

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Configuração](#Configura.C3.A7.C3.A3o)
*   [3 Iniciando](#Iniciando)
*   [4 Uso](#Uso)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [webmin](https://aur.archlinux.org/packages/webmin/) do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). Webmin exige [perl-net-ssleay](https://www.archlinux.org/packages/?name=perl-net-ssleay) para suporte a [HTTPS](https://en.wikipedia.org/wiki/pt:https "wikipedia:pt:https").

## Configuração

Para permitir o acesso ao Webmin de um computador remoto, configure seu firewall para permitir acesso a porta TPC 10000\. Você pode querer configurar o firewall para restringir o acesso apenas a determinados endereços IP.

## Iniciando

Inicie [serviço](/index.php/Daemons_(Portugu%C3%AAs) "Daemons (Português)") webmin usando [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"). Habilite se deseja que Webmin seja iniciado no boot.

## Uso

Em um navegador web, digite o endereço HTTPS de seu servidor com a porta 10000 para acessar Webmin:

```
https://*host*:10000

```

Você precisa entrar com a senha de root do servidor para usar a interface Webmin e administrar o servidor.