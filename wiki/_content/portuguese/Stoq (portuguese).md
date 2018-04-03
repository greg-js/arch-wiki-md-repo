[Stoq](http://www.stoq.com.br) é uma suíte de gerenciamento empresarial open-source.

O aplicativo Stoq usa o PostgreSQL como banco de dados back-end, com um cliente através de uma interface gráfica.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
    *   [1.1 Instalação do Stoq](#Instala.C3.A7.C3.A3o_do_Stoq)
    *   [1.2 Configuração do Stoq](#Configura.C3.A7.C3.A3o_do_Stoq)
        *   [1.2.1 Conexão com banco de dados local](#Conex.C3.A3o_com_banco_de_dados_local)
        *   [1.2.2 Configurar conexão com banco de dados manualmente](#Configurar_conex.C3.A3o_com_banco_de_dados_manualmente)
        *   [1.2.3 Arquivo de configuração do Stoq](#Arquivo_de_configura.C3.A7.C3.A3o_do_Stoq)
    *   [1.3 Instalação do stoq-server](#Instala.C3.A7.C3.A3o_do_stoq-server)
    *   [1.4 Configuração do stoq-server](#Configura.C3.A7.C3.A3o_do_stoq-server)
        *   [1.4.1 Arquivo de configuração do stoq-server](#Arquivo_de_configura.C3.A7.C3.A3o_do_stoq-server)
    *   [1.5 Acessando via conexão serial](#Acessando_via_conex.C3.A3o_serial)
*   [2 Documentação adicional](#Documenta.C3.A7.C3.A3o_adicional)

## Instalação

### Instalação do Stoq

[Instale](/index.php/Help:Reading_(Portugu%C3%AAs)#Instala.C3.A7.C3.A3o_de_pacotes "Help:Reading (Português)") o pacote [stoq](https://aur.archlinux.org/packages/stoq/). Note que os pacote Stoq vêm com um braço de bibliotecas python2 disponíveis no [AUR](/index.php/AUR "AUR"). A instalação da dependência [webkitgtk2](https://aur.archlinux.org/packages/webkitgtk2/) levará muito tempo no processo de instalação.

### Configuração do Stoq

Após a execução do Stoq pela primeira vez será necessário configurar a localização do banco de dados. Nesta etapa existem duas opções para o cliente se conectar ao banco de dados:

*   Conectar no banco de dados localmente;
*   Configurar manualmente a conexão com o banco de dados.

#### Conexão com banco de dados local

Para conexão com o banco de dados no local é necessário [instalar](/index.php/Help:Reading_(Portugu%C3%AAs)#Instala.C3.A7.C3.A3o_de_pacotes "Help:Reading (Português)") o [postgresql](https://www.archlinux.org/packages/?name=postgresql).

Se a instância PostgreSQL ainda não estiver inicializada, seguir o artigo [Processo de instalação do PostgreSQL](/index.php/PostgreSQL#Installing_PostgreSQL "PostgreSQL"). Em seguida, como o root, [ative ou habilite](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)") o `postgresql.service`.

Na tela "Localização do banco de dados" utilizar a opção "Eu quero usar o Stoq apenas neste computador".

#### Configurar conexão com banco de dados manualmente

Na tela "Localização do banco de dados" utilizar a opção "Quero configurar a conexão com o banco de dados manualmente" e inserir os dados para a conexão com o banco de dados.

#### Arquivo de configuração do Stoq

O principal arquivo de configuraçãos do Stoq se encontra em `~/.stoq/stoq.conf`.

### Instalação do stoq-server

[Instale](/index.php/Help:Reading_(Portugu%C3%AAs)#Instala.C3.A7.C3.A3o_de_pacotes "Help:Reading (Português)") o pacote [stoq-server](https://aur.archlinux.org/packages/stoq-server/). Então [defina a senha](/index.php/Users_and_groups#Example_adding_a_user "Users and groups") do novo usuário *stoqserver*.

### Configuração do stoq-server

Se a instância PostgreSQL ainda não estiver inicializada, seguir o artigo [Processo de instalação do PostgreSQL](/index.php/PostgreSQL#Installing_PostgreSQL "PostgreSQL"). Em seguida, como o root, [ative ou habilite](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)") o `postgresql.service`.

É necessário criar uma nova configuração no PostgreSQL para o stoq-server. Para isso, entre no usário padrão para o PostgreSQL, 'postgres', usando os seguintes comandos:

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

Onde:

*   o `-p` é a porta que o PostgreSQL usa para conexões remotas;
*   e `-D` é o diretório que as configurações do stoq-server serão armazenadas.

Retorne ao usuário regular usando `exit`.

Para que o stoq-server seja acessível remotamente é necessário seguir o artigo [Configurar o PostgreSQL para ser acessível a partir de hosts remotos](/index.php/PostgreSQL#Configure_PostgreSQL_to_be_accessible_from_remote_hosts "PostgreSQL").

Como root, [ative ou habilite](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)") o `supervisord.service`.

Reinicie o processo do supervisor:

```
# supervisorctl update

```

```
# supervisorctl restart stoqserver

```

#### Arquivo de configuração do stoq-server

O principal arquivo de configuraçãos do stoq-server se encontra em `/usr/share/stoqserver/.stoq/stoq.conf`.

### Acessando via conexão serial

É possível o stoq-server se comunicar via conexão serial ou serial sobre uma conexão USB. Basta adicionar o usuário stoqserver ao grupo `uucp`.

```
# gpasswd -a stoqserver uucp

```

**Nota:** Você deve deslogar e logar novamente para ter efeito.

## Documentação adicional

Para mais informações, leia a [wiki](https://wiki.stoq.com.br) e o [manual](https://doc.stoq.com.br/manual/latest/) do Stoq.