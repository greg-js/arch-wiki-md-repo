**Status de tradução:** Esse artigo é uma tradução de [Flyspray](/index.php/Flyspray "Flyspray"). Data da última tradução: 2019-06-24\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Flyspray&diff=0&oldid=557661) na versão em inglês.

Artigos relacionados

*   [LAMP](/index.php/LAMP "LAMP")

[Flyspray](http://www.flyspray.org/) é um sistema de rastreador de erros escrito em [PHP](/index.php/PHP "PHP").

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [flyspray](https://www.archlinux.org/packages/?name=flyspray). Flyspray precisa de um servidor web, tal como [servidor Apache HTTP](/index.php/Apache_HTTP_Server "Apache HTTP Server") com [PHP](/index.php/PHP "PHP"), e um servidor SQL, tal como [MySQL](/index.php/MySQL "MySQL") ou [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

### Configuração do Apache

**Nota:** Você precisará [Apache](/index.php/Apache "Apache") configurado para executar com [PHP](/index.php/PHP "PHP"). Confira [Apache#PHP](/index.php/Apache#PHP "Apache") para instruções. Certifique-se de descomentar `extension=mysqli` em `/etc/php/php.ini`.

Você precisará criar um arquivo de configuração para o apache localizar sua instalação de Flyspray. Crie o seguinte arquivo:

 `/etc/httpd/conf/extra/flyspray.conf` 
```
Alias /flyspray "/usr/share/webapps/flyspray"
<Directory "/usr/share/webapps/flyspray">
    AllowOverride All
    Options FollowSymlinks
    Require all granted
    php_admin_value open_basedir "/srv/http/:/tmp/:/usr/share/webapps/flyspray"
</Directory>
```

Você então precisará editar `/etc/webapps/flyspray/.htaccess` e alterar `deny from all` para `allow of all`. Agora você deve poder navegar até a interface do flyspray (por exemplo, `[http://localhost/flyspray](http://localhost/flyspray)`) e ele mostrará uma página de verificações de pré-instalação. Quaisquer problemas aqui devem ser resolvidos antes de continuar.