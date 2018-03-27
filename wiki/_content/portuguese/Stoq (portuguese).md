[Stoq](http://www.stoq.com.br) é uma suíte de gerenciamento empresarial open-source.

O aplicativo Stoq usa o PostgreSQL como banco de dados back-end, com um cliente através de uma interface gráfica.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
    *   [1.1 Instalação do Stoq](#Instala.C3.A7.C3.A3o_do_Stoq)
    *   [1.2 Instalação do stoq-server](#Instala.C3.A7.C3.A3o_do_stoq-server)
    *   [1.3 Acessando via conexão serial](#Acessando_via_conex.C3.A3o_serial)
*   [2 Documentação adicional](#Documenta.C3.A7.C3.A3o_adicional)

## Instalação

### Instalação do Stoq

Instale o pacote [stoq](https://aur.archlinux.org/packages/stoq/). Note que os pacote Stoq vêm com um braço de bibliotecas python2 disponíveis no [AUR](/index.php/AUR "AUR"). A dependência de [webkitgtk2](https://aur.archlinux.org/packages/webkitgtk2/) levará muito tempo no processo de instalação.

O principal arquivo de configuração do Stoq se encontra em ~/.stoq/stoq.conf.

### Instalação do stoq-server

Instale o pacote [stoq-server](https://aur.archlinux.org/packages/stoq-server/). Então [defina a senha](/index.php/Users_and_groups#Example_adding_a_user "Users and groups") do novo usuário *stoqserver*.

Com o root, [start](/index.php/Start "Start") e [enable](/index.php/Enable "Enable") o `postgresql.service`. Se a instância PostgreSQL ainda não estiver inicializada, seguir o artigo [PostgreSQL install process](/index.php/PostgreSQL#Installing_PostgreSQL "PostgreSQL").

É necessário criar uma nova configuração no PostgreSQL para o stoqserver. Para isso, entre no usário padrão para o PostgreSQL, 'postgres', usando os seguintes comandos:

*   Se você tiver [sudo](https://www.archlinux.org/packages/?name=sudo) e seu usuário estiver no `sudoers`:

	 `$ sudo -u postgres -i` 

*   Senão:

```
$ su
# su -l postgres

```

Use o script stoqsconf para gerar os arquivos de configurações necessárias:

```
[postgres]$ stoqsconf -p 5432 -D "/usr/share/stoqserver"

```

O principal arquivo de configuraçãos do stoqserver se encontra em /usr/share/stoqserver/.stoq/stoq.conf.

Como root, [start](/index.php/Start "Start") ou [enable](/index.php/Enable "Enable") o `supervisord.service`.

Reinicie o processo do supervisor:

```
# supervisorctl update

```

```
# supervisorctl restart stoqserver

```

É necessário [start](/index.php/Start "Start") ou [enable](/index.php/Enable "Enable") o `postgresql.service` e `supervisord.service` antes de iniciar o Stoq com o stoqserver.

### Acessando via conexão serial

É possível o stoqserver se comunicar via conexão serial ou serial sobre uma conexão USB. Basta adicionar o usuário stoqserver ao grupo `uucp`.

```
# gpasswd -a stoqserver uucp

```

**Nota:** Você deve deslogar e logar novamente para ter efeito.

## Documentação adicional

Para mais informações, leia o [Manual do Stoq](https://doc.stoq.com.br/manual/latest/).