[Stoq](http://www.stoq.com.br) é uma suíte de gerenciamento empresarial open-source.

O aplicativo Stoq usa o [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") como banco de dados back-end, com um cliente através de uma interface gráfica.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Instalação do Stoq](#Instalação_do_Stoq)
    *   [1.2 Configuração do Stoq](#Configuração_do_Stoq)
        *   [1.2.1 Conexão com banco de dados local](#Conexão_com_banco_de_dados_local)
        *   [1.2.2 Configurar conexão com banco de dados manualmente](#Configurar_conexão_com_banco_de_dados_manualmente)
        *   [1.2.3 Arquivo de configuração do Stoq](#Arquivo_de_configuração_do_Stoq)
    *   [1.3 Instalação do stoq-server](#Instalação_do_stoq-server)
    *   [1.4 Configuração do stoq-server](#Configuração_do_stoq-server)
        *   [1.4.1 Arquivo de configuração do stoq-server](#Arquivo_de_configuração_do_stoq-server)
    *   [1.5 Acessando via conexão serial](#Acessando_via_conexão_serial)
*   [2 Documentação adicional](#Documentação_adicional)

## Instalação

### Instalação do Stoq

[Instale](/index.php/Instale "Instale") o pacote [stoq](https://aur.archlinux.org/packages/stoq/). A instalação da dependência [webkitgtk](https://aur.archlinux.org/packages/webkitgtk/) levará muito tempo no processo de instalação.

### Configuração do Stoq

Após a execução do Stoq pela primeira vez será necessário configurar a localização do banco de dados. Nessa etapa existem duas opções para o cliente se conectar ao banco de dados:

*   Conectar no banco de dados localmente;
*   Configurar manualmente a conexão com o banco de dados.

#### Conexão com banco de dados local

Para conexão com o banco de dados no local é necessário [instalar](/index.php/Instalar "Instalar") o [postgresql](https://www.archlinux.org/packages/?name=postgresql).

Se a instância PostgreSQL ainda não estiver inicializada, consulte [PostgreSQL#Initial configuration](/index.php/PostgreSQL#Initial_configuration "PostgreSQL").

Em seguida, como o root, [inicie](/index.php/Inicie "Inicie") ou [habilite](/index.php/Habilite "Habilite") o `postgresql.service`.

Na tela "Localização do banco de dados" utilizar a opção "Eu quero usar o Stoq apenas neste computador".

#### Configurar conexão com banco de dados manualmente

Na tela "Localização do banco de dados" utilizar a opção "Quero configurar a conexão com o banco de dados manualmente" e inserir os dados para a conexão com o banco de dados.

#### Arquivo de configuração do Stoq

O principal arquivo de configurações do Stoq se encontra em `~/.stoq/stoq.conf`.

### Instalação do stoq-server

[Instale](/index.php/Instale "Instale") o pacote [stoq-server](https://aur.archlinux.org/packages/stoq-server/). Então [defina a senha](/index.php/Usu%C3%A1rios_e_grupos#Exemplo_de_adicionar_um_usuário "Usuários e grupos") do novo usuário *stoqserver*.

### Configuração do stoq-server

Se a instância PostgreSQL ainda não estiver inicializada, consulte [PostgreSQL#Initial configuration](/index.php/PostgreSQL#Initial_configuration "PostgreSQL").

Em seguida, como o root, [inicie](/index.php/Inicie "Inicie") ou [habilite](/index.php/Habilite "Habilite") o `postgresql.service`.

É necessário criar uma nova configuração no PostgreSQL para o stoq-server. Para isso, entre no usuário padrão para o PostgreSQL, 'postgres', usando os seguintes comandos:

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

Como root, [inicie](/index.php/Inicie "Inicie") ou [habilite](/index.php/Habilite "Habilite") o `supervisord.service`.

Reinicie o processo do supervisor:

```
# supervisorctl update

```

```
# supervisorctl restart stoqserver

```

#### Arquivo de configuração do stoq-server

O principal arquivo de configurações do stoq-server se encontra em `/usr/share/stoqserver/.stoq/stoq.conf`.

### Acessando via conexão serial

É possível o stoq-server se comunicar via conexão serial ou serial sobre uma conexão USB. Basta adicionar o usuário stoqserver ao grupo `uucp`.

```
# gpasswd -a stoqserver uucp

```

**Nota:** Você deve deslogar e logar novamente para ter efeito.

## Documentação adicional

Para mais informações, leia a [wiki](https://wiki.stoq.com.br) e o [manual](https://doc.stoq.com.br/manual/latest/) do Stoq.