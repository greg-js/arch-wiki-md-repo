Artículos relacionados

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")

**P: ¿Cómo puedo apagar limpiando la pantalla después de que el sistema haya booteado así puedo ver los mensajes que se imprimen durante arranque de sistema?.** R: Eliminando el primer carácter del archivo /etc/issue que luce así: ^[c

**P: Y cómo lo puedo poner otra vez?.** R: No puedes tipear el carácter como habías puesto el carácter literal de escape. Este es dependiente del redactor. En vim:

```
i (insert)
ctrl-v (insert literal character)
ESC (insert escape character)
c
ESC (exit insert mode)
ZZ (Save and Exit)

```

Pero si quieres mantener la pantalla limpia después del login en una Terminal virtual, sin despejar después de que el sistema haya booteado puedes hacer:

```
echo clear >> ~/.bash_logout

```