**Status de tradução:** Esse artigo é uma tradução de [Telnet](/index.php/Telnet "Telnet"). Data da última tradução: 2019-10-08\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Telnet&diff=0&oldid=584717) na versão em inglês.

[Telnet](https://en.wikipedia.org/wiki/pt:Telnet ou encapsulada através de uma VPN. Para uma alternativa segura, veja [SSH](/index.php/SSH_(Portugu%C3%AAs) "SSH (Português)").

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [inetutils](https://www.archlinux.org/packages/?name=inetutils).

Inclui um cliente de telnet. Um servidor telnet pode ser configurado com soquetes [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") ou xinetd. O telnetd via systemd requer apenas o pacote [inetutils](https://www.archlinux.org/packages/?name=inetutils). Para configurar um servidor telnet com xinetd, instale [xinetd](https://www.archlinux.org/packages/?name=xinetd) também.

## Configuração

Para habilitar conexão de servidor telnet no systemd, [habilite](/index.php/Habilite "Habilite") `telnet.socket` (se o servidor telnet deve ser iniciado na inicialização) e [inicia](/index.php/Inicia "Inicia") `telnet.socket` para testar a conectividade.

Para habilitar as conexões de servidor telnet em xinetd, edite `/etc/xinetd.d/telnet`, altere `disable = yes` para `disable = no` e reinicie o serviço xinetd.

[Habilite](/index.php/Habilite "Habilite") o serviço de xinetd no systemd se você quiser iniciá-lo na inicialização do computador.

### Testando a configuração

Tente abrir uma conexão telnet ao seu servidor:

```
$ telnet localhost

```

Tente um login root para ver se sua configuração permite isso e as implicações de segurança que isso implica.

Se a sessão se desconectar antes de você receber um prompt de login, tente instalar [inetutils-git](https://aur.archlinux.org/packages/inetutils-git/) no lugar dos inetutils atuais e reiniciar o telnet.socket.

**Dica:** Se você receber códigos de lixo de um servidor de telnet remoto enviando caracteres não-ascii com uma codificação não unicode, você pode tentar [xorg-luit](https://www.archlinux.org/packages/?name=xorg-luit) para resolver este problema.