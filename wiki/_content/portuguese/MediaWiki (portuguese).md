**Nota:** MediaWiki ainda não é completamente compatível com PHP 7.3.[[1]](https://www.mediawiki.org/wiki/Compatibility#PHP)[[2]](https://phabricator.wikimedia.org/project/view/3494/)

[MediaWiki](https://www.mediawiki.org/wiki/MediaWiki) é um software wiki de código aberto e livre escrito em [PHP](/index.php/PHP "PHP"), originalmente desenvolvido para a Wikipédia. Ele também alimenta este wiki (consulte [Special:Version](/index.php/Special:Version "Special:Version") e o [repositório do GitHub](https://github.com/archlinux/archwiki)).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Configuração](#Configuração)
    *   [2.1 PHP](#PHP)
    *   [2.2 Servidor web](#Servidor_web)
        *   [2.2.1 Apache](#Apache)
        *   [2.2.2 Nginx](#Nginx)
        *   [2.2.3 Lighttpd](#Lighttpd)
    *   [2.3 Banco de dados](#Banco_de_dados)
    *   [2.4 LocalSettings.php](#LocalSettings.php)
*   [3 Dicas e truques](#Dicas_e_truques)
    *   [3.1 Matemática (texvc)](#Matemática_(texvc))
    *   [3.2 Unicode](#Unicode)
    *   [3.3 VisualEditor](#VisualEditor)

## Instalação

Para executar o MediaWiki, você precisa de três coisas:

*   o pacote [mediawiki](https://www.archlinux.org/packages/?name=mediawiki), o qual obtém [PHP](/index.php/PHP "PHP")
*   um servidor web – [Apache](/index.php/Apache "Apache"), [Nginx](/index.php/Nginx "Nginx") or [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   um sistema de banco de dados – [MySQL](/index.php/MySQL "MySQL"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") or [SQLite](/index.php/SQLite "SQLite")

Para instalar o MediaWiki no [XAMPP](/index.php/XAMPP "XAMPP"), veja [mw:Manual:Installing MediaWiki on XAMPP](https://www.mediawiki.org/wiki/Manual:Installing_MediaWiki_on_XAMPP "mw:Manual:Installing MediaWiki on XAMPP")

## Configuração

As etapas para obter uma configuração funcional do MediaWiki envolvem a edição das configurações do PHP e a adição dos trechos de configuração do MediaWiki.

### PHP

MediaWiki precisa da extensão `iconv`, então você precisa descomentar `extension=iconv` em `/etc/php/php.ini`.

Dependências opcionais:

*   Para renderização de miniaturas, instale [ImageMagick](/index.php/ImageMagick "ImageMagick") ou [php-gd](https://www.archlinux.org/packages/?name=php-gd). Se você escolher o último, você também precisa descomentar `extension=gd`.
*   Para mais uma [normalização Unicode](https://www.mediawiki.org/wiki/Unicode_normalization_considerations/pt-br "mw:Unicode normalization considerations/pt-br") eficiente, instale [php-intl](https://www.archlinux.org/packages/?name=php-intl) e descomente `extension=intl`.

Habilite a API para seu SGBD:

*   Se você usa [MariaDB](/index.php/MariaDB "MariaDB"), descomente `extension=mysqli`.
*   Se você usa [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), instale [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql) e descomente `extension=pgsql`.
*   Se você usa [SQLite](/index.php/SQLite "SQLite"), instale [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) e descomente `extension=pdo_sqlite`.

Em segunda, ajuste a manipulação da sessão ou você pode receber um erro fatal (`PHP Fatal error: session_start(): Failed to initialize storage module[...]`) localizando o caminho `session.save_path`. Uma boa opção pode ser `/var/lib/php/sessions` ou `/tmp/`.

 `/etc/php/php.ini`  `session.save_path = "/var/lib/php/sessions"` 

Você precisará criar o diretório se ele não existir e depois restringir suas permissões:

```
# mkdir -p /var/lib/php/sessions/
# chown http:http /var/lib/php/sessions
# chmod go-rwx /var/lib/php/sessions

```

Se você usa [open_basedir do PHP](/index.php/PHP#Configuration "PHP") e deseja [permitir uploads de arquivos](https://www.mediawiki.org/wiki/Manual:Configuring_file_uploads "mw:Manual:Configuring file uploads"), é necessário incluir `/var/lib/media/wiki/` ([mediawiki](https://www.archlinux.org/packages/?name=mediawiki) faz links simbólicos de `images/` para `/var/lib/mediawiki/`).

### Servidor web

#### Apache

Siga [Apache HTTP Server#PHP](/index.php/Apache_HTTP_Server#PHP "Apache HTTP Server").

Copie `/etc/webapps/mediawiki/apache.example.conf` para `/etc/httpd/conf/extra/mediawiki.conf` e edite-o conforme necessário.

Adicione a seguinte linha a `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/mediawiki.conf

```

[Reinicie](/index.php/Reinicie "Reinicie") o daemon `httpd.service`.

**Nota:** O arquivo padrão de `/etc/webapps/mediawiki/apache.example.conf` substituirá a configuração de open_basedir do PHP, possivelmente conflitando com outras páginas. Esse comportamento pode ser alterado movendo a linha começando com `php_admin_value` entre as tags `<Directory>`. Além disso, se você estiver executando vários aplicativos que dependem do mesmo servidor, esse valor também poderá ser adicionado ao valor de open_basedir em `/etc/php/php.ini` em vez de em `/etc/httpd/conf/extra/mediawiki.conf`

#### Nginx

Para que o MediaWiki trabalhe com [Nginx](/index.php/Nginx "Nginx"), crie o seguinte arquivo:

 `/etc/nginx/mediawiki.conf` 
```
location / {
   index index.php;
   try_files $uri $uri/ @mediawiki;
}
location @mediawiki {
   rewrite ^/(.*)$ /index.php;
}
location ~ \.php5?$ {
   include /etc/nginx/fastcgi_params;
   fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
   fastcgi_index index.php5;
   fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
   try_files $uri @mediawiki;
}
location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
   try_files $uri /index.php;
   expires max;
   log_not_found off;
}
# Restrictions based on the .htaccess files
location ^~ ^/(cache|includes|maintenance|languages|serialized|tests|images/deleted)/ {
   deny all;
}
location ^~ ^/(bin|docs|extensions|includes|maintenance|mw-config|resources|serialized|tests)/ {
   internal;
}
location ^~ /images/ {
   try_files $uri /index.php;
}
location ~ /\. {
   access_log off;
   log_not_found off; 
   deny all;
}

```

Certifique-se que [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) está instalado em [iniciado](/index.php/Inicia "Inicia").

Inclua uma diretiva de servidor, semelhante a esta

 `/etc/nginx/nginx.conf` 
```
server {
  listen 80;
  server_name mediawiki;
  root /usr/share/webapps/mediawiki;
  index index.php;
  charset utf-8;
# For correct file uploads
  client_max_body_size    100m; # Equal or more than upload_max_filesize in /etc/php/php.ini
  client_body_timeout     60;
  include mediawiki.conf;

}

```

Ao final, [reinicie](/index.php/Reinicie "Reinicie") os daemons `nginx.service` e `php-fpm.service`.

#### Lighttpd

Você deve ter o [Lighttpd](/index.php/Lighttpd "Lighttpd") instalado e configurado. "mod_alias" e "mod_rewrite" na matriz server.modules do lighttpd são necessários. Anexe ao arquivo de configuração lighttpd as seguintes linhas

 `/etc/lighttpd/lighttpd.conf` 
```
alias.url += ("/mediawiki" => "/usr/share/webapps/mediawiki/")
url.rewrite-once += (
                "^/mediawiki/wiki/upload/(.+)" => "/mediawiki/wiki/upload/$1",
                "^/mediawiki/wiki/$" => "/mediawiki/index.php",
                "^/mediawiki/wiki/([^?]*)(?:\?(.*))?" => "/mediawiki/index.php?title=$1&$2"
)

```

[Reinicie](/index.php/Reinicie "Reinicie") o daemon `lighttpd.service`.

### Banco de dados

Configure um servidor de banco de dados conforme explicado no artigo do seu SGBD: [MySQL](/index.php/MySQL "MySQL"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") ou [SQLite](/index.php/SQLite "SQLite").

O MediaWiki pode criar automaticamente o banco de dados, se você fornecer a senha de root do banco de dados, durante a [próxima etapa](#LocalSettings.php). Caso contrário, o banco de dados precisa ser criado manualmente, consulte as [instruções do upstream](https://www.mediawiki.org/wiki/Manual:Installing_MediaWiki/pt-br#Criar_uma_base_de_dados "mw:Manual:Installing MediaWiki/pt-br").

### LocalSettings.php

Abra a url do wiki (geralmente `http://*seu_servidor*/mediawiki/`) em um navegador e faça a configuração inicial. Siga as [instruções do upstream](https://www.mediawiki.org/wiki/Manual:Config_script/pt-br "mw:Manual:Config script/pt-br").

O arquivo `LocalSettings.php` gerado é oferecido para download, salve-o em `/usr/share/webapps/mediawiki/LocalSettings.php`. Este arquivo define as configurações específicas do seu wiki. Sempre que você atualiza o pacote [mediawiki](https://www.archlinux.org/packages/?name=mediawiki), ele não é substituído.

## Dicas e truques

### Matemática (texvc)

Geralmente, instalar [texvc](https://www.archlinux.org/packages/?name=texvc) e habilitá-lo na configuração é o suficiente:

```
$wgUseTeX = true;

```

Se você tiver problemas, tente aumentar os limites para comandos shell:

```
$wgMaxShellMemory = 8000000;
$wgMaxShellFileSize = 1000000;
$wgMaxShellTime = 300;
```

### Unicode

Verifique se php, apache e mysql usam UTF-8\. Caso contrário, você poderá enfrentar erros estranhos devido à incompatibilidade de codificação.

### VisualEditor

A extensão VisualEditor MediaWiki fornece um editor de texto rico para o MediaWiki. Siga [mw:Extension:VisualEditor](https://www.mediawiki.org/wiki/Extension:VisualEditor "mw:Extension:VisualEditor") para instalá-lo.

Você também precisará do backend Node.js [Parsoid](https://www.mediawiki.org/wiki/Parsoid "mw:Parsoid"), o qual está disponível por meio de [parsoid-git](https://aur.archlinux.org/packages/parsoid-git/).

Ajuste o caminho do MediaWiki em `/usr/share/webapps/parsoid/api/localsettings.js`:

```
parsoidConfig.setInterwiki( 'localhost', 'http://localhost/mediawiki/api.php' );

```

Após isso, [habilite](/index.php/Habilite "Habilite") e inicie `parsoid.service`.

Como alternativa, também é possível usar o pacote [parsoid](https://aur.archlinux.org/packages/parsoid/) e configurar o serviço através do arquivo yaml, onde as seguintes linhas devem estar presentes:

 `/usr/share/webapps/parsoid/config.yaml` 
```
uri: `'http://localhost/mediawiki/api.php'`
domain: 'localhost'

```

A parte correspondente nas configurações do mediawiki:

 `/usr/share/webapps/mediawiki/LocalSettings.php` 
```
$wgVirtualRestConfig['modules']['parsoid'] = array(
  // URL to the Parsoid instance - use port 8142 if you use the Debian package - the parameter 'URL' was first used but is now deprecated (string)
  'url' => 'http://localhost:8000/',
  // Parsoid "domain" (string, optional) - MediaWiki >= 1.26
  'domain' => 'localhost',
  // Parsoid "prefix" (string, optional) - deprecated since MediaWiki 1.26, use 'domain'
  'prefix' => 'localhost',
  // Forward cookies in the case of private wikis (string or false, optional)
  'forwardCookies' => false,
  // request timeout in seconds (integer or null, optional)
  'timeout' => null,
  // Parsoid HTTP proxy (string or null, optional)
  'HTTPProxy' => null,
  // whether to parse URL as if they were meant for RESTBase (boolean or null, optional)
  'restbaseCompat' => null,
);

```

Após a configuração, o serviço `parsoid` pode ser iniciado (reiniciado) e (se ainda não tiver sido feito) habilitado.