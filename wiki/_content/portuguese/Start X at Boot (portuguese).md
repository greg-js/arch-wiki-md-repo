Artigos relacionados

*   [Automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")
*   [Display Manager](/index.php/Display_Manager "Display Manager")
*   [Xinitrc](/index.php/Xinitrc "Xinitrc")

Um [gestor de display](/index.php/Display_manager_(Portugu%C3%AAs) "Display manager (Português)") pode ser utilizado para prover uma tela de login e incializar o [servidor X](/index.php/Servidor_X "Servidor X"). Este artigo explica como isto pode ser feito utilizando um terminal virtual existente.

Para inciar o X manualmente, `startx` ou `xinit` são utilizados. Ambos executarão o `~/.xinitrc`, que pode ser customizado para iniciar um gerenciador de janelas de sua escolha como descrito no artigo [xinitrc](/index.php/Xinitrc "Xinitrc").

## Arquivo profile do shell

**Nota:** Isso roda o X na mesma tty usada para login, que é requerida para manter as permissões locais.

*   Para o bash, adicione o seguinte no final do `~/.bash_profile`. Se o arquivo não existir, copie uma versão do diretório skel `/etc/skel/.bash_profile`.

Para o zsh, adicione o seguinte em `~/.zprofile`.

 `arquivo profile do shell` 
```
[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && exec startx

```

**Nota:**

*   Você pode susbstituir a comparação `-eq 1` com uma outra como `-le 3` (vt1 para vt3) se você quiser usar logins gráficos em mais de um terminal virtual.
*   X deve sempre rodar no mesmo tty onde o login ocorreu, para preservar a sessão logind. É tratado pelo padrão `/etc/X11/xinit/xserverrc`.

*   Para [Fish](/index.php/Fish "Fish"), adicione o seguinte no final do seu `~/.config/fish/config.fish`.

```
# start X at login
if status --is-login
    if test -z "$DISPLAY" -a $XDG_VTNR = 1
        exec startx
    end
end

```

## Dicas

*   Este método pode ser combinado com [login automático para console virtual](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console"). Ao fazer isso, você tem que definir as dependências corretas para o serviço autologin do systemd garantir que dbus seja iniciado antes de ler `~/.xinitrc` e, portanto, pulseaudio iniciado (veja: [BBS#155416](https://bbs.archlinux.org/viewtopic.php?id=155416))
*   Se quiser permanecer conectado quando a sessão X termina, remova `exec`.
*   Para redirecionar a saída da sessão X para um arquivo, crie um [alias](/index.php/Alias "Alias"):

	 `alias startx='startx &> ~/.xlog'`