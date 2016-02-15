O FAM (File Alteration Monitor) no daemon é usado para ambientes desktop, como [GNOME](/index.php/GNOME "GNOME") e [Xfce](/index.php/Xfce "Xfce") para o monitor e reportar as mudaças no filesystem. FAM é também é usando no servidor Samba no daemon. Note que o [KDE](/index.php/KDE "KDE") usa muito o FAM, tem movido no kernel-based _inotify_ um requerimento especial na configuração.

**Atenção** | FAM é absoluto; usa como alternativa o [Gamin](/index.php/Gamin "Gamin"), se possível. Gamin é a implementação da especificação do FAM. Este é o mais novo e mantido ativamente, é muito simples para configurar.

## Instalação

O FAM precisa de algumas dependências para utilização do pacote, como:

```
# pacman -S fam

```

## Configuração

Iniciando o FAM manualmente

```
# /etc/rc.d/fam start

```

A inicialização do FAM no boot, adionione na linha do DAEMON no diretório `/etc/rc.conf`. Se estiver usando o [NetworkManager](/index.php/NetworkManager "NetworkManager") no daemon, adicione depois dele.

```
# DAEMONS=(syslog-ng powersaved dhcdbd networkmanager fam ...)

```