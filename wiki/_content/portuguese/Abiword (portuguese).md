[Abiword](http://www.abisource.com/) é um processador de texto que oferece uma alternativa mais leve para o [LibreOffice](/index.php/LibreOffice "LibreOffice") Writer e o [OpenOffice](/index.php/OpenOffice "OpenOffice") Writer, ao mesmo tempo em que fornece excelente funcionalidade. O Abiword possui suporte a muitos tipos de documentos padrão, como documentos ODF, documentos do Microsoft Word, documentos do WordPerfect, documentos em formato Rich Text e páginas da Web em HTML.

## Contents

*   [1 Instalação](#Instalação)
*   [2 Diretório de configuração do usuário](#Diretório_de_configuração_do_usuário)
*   [3 Modelos](#Modelos)
    *   [3.1 Usando modelos](#Usando_modelos)
    *   [3.2 Criando ou alterando modelos](#Criando_ou_alterando_modelos)
*   [4 Verificação gramatical](#Verificação_gramatical)
*   [5 Alterar associações de teclas](#Alterar_associações_de_teclas)
*   [6 Fontes LaTeX](#Fontes_LaTeX)
*   [7 Solução de problemas](#Solução_de_problemas)
    *   [7.1 Correção para travamento do diálogo de impressão](#Correção_para_travamento_do_diálogo_de_impressão)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [abiword](https://www.archlinux.org/packages/?name=abiword). Você pode querer instalar dicionários se quiser a verificação ortográfica, que pode ser fornecida pelo pacote [aspell-en](https://www.archlinux.org/packages/?name=aspell-en) para inglês.

Para corrigir pequenos problemas de cursor e texto desalinhado, instale [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) ou [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) e [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont).

## Diretório de configuração do usuário

Desde a versão 3.0, AbiWord vai usar `~/.config/abiword-3.0` para armazenar arquivos do usuário.

Versões anteriores do AbiWord usavam `~/.config/AbiSuite` e, se este diretório for encontrado na inicialização do programa, ele será automaticamente renomeado. Se `~/.config/AbiSuite` e `~/.config/abiword-3.0` não existirem, o AbiWord **não** vai criá-lo.

## Modelos

AbiWord fornece um sistema de modelos que permite agilizar a escrita de documentos comuns. Modelos são fornecidos como arquivos *.awt*, para **A**bi**W**ord **T**emplate.

Arquivos de modelos são procurados dentro das pastas `/usr/share/abiword-3.0/templates` e `~/.config/abiword-3.0/templates`.

### Usando modelos

Em um novo documento, escolha *Arquivo > Novo a partir de Modelo...*, então, na caixa de diálogo "Escolha um modelo", selecione um dos modelos encontrados e listados, ou clique em "Abrir" para navegar pelos seus arquivos para um arquivo do AbiWord (não necessariamente um arquivo *.awt*).

### Criando ou alterando modelos

AbiWord possibilita que você faça seus próprios arquivos de modelos, com os estilos, textos, tabelas etc. desejados.

Para criar/alterar um arquivo de modelo, basta abrir um novo documento ou existente, e fazer as alterações desejadas a esse arquivo. Então, use a opção de menu "Salvar Como" para nomeá-lo como quiser, com *.awt* como extensão (por exemplo, *foobar.awt*) e salvá-lo na pasta `~/.config/abiword-3.0/templates`. Agora, seu novo modelo pode ser acessado em *Arquivo > Novo a partir de Modelo...* pelo seu nome de arquivo (*foobar.awt* no exemplo dado).

**Nota:** Se não existir, a pasta `templates` será criada automaticamente na inicialização dentro de `~/.config/abiword-3.0/`.

## Verificação gramatical

Habilite verificação gramatical em *Editar > Opções > Verificação Ortográfica > Verificação automática e gramática*.

## Alterar associações de teclas

**Nota:** [Essa página de wiki](http://www.abisource.com/wiki/Keyboard_bindings) têm instruções sobre isso, mas algumas estão desatualizadas e não funcionam

Você pode alterar as associações de teclas padrão no AbiWord usando [KeyBindings](https://www.abisource.com/wiki/KeyBindings).

Para definir as associações de teclas, edite `~/.config/abiword/profile` e, dentro da seção `AbiPreferences`, adicione as *KeyBindings* desejadas. Por exemplo, você pode adicionar `KeyBindings="viEdit"` ou `KeyBindings="emacs"`.

## Fontes LaTeX

The package [abiword](https://www.archlinux.org/packages/?name=abiword) comes with a function which allows user to insert LaTeX codes in a document. To display mathematics symbols properly, one needs to download [latex-xft-fonts](http://movementarian.org/latex-xft-fonts-0.1.tar.gz) and save it to the directory `/usr/share/fonts`. To install the font, extract the tarball and then run the following:

```
# fc-cache -fv

```

## Solução de problemas

### Correção para travamento do diálogo de impressão

**Note:** This bug has been reported as non-existent for version 2.8.1 or higher. However, this section will remain for legacy versions or if it crops up again,

For some reason, the current versions of Abiword and libgnomeprint are not playing nice together. The `.abw` default template causes the program to crash when the user attempts to print. The solution is to force abiword to work with the `.rtf` format instead. By following the steps below, you will set the default save format to .rtf and trick Abiword into using a `.rtf` file as its default template.

Open `~/.AbiSuite/AbiWord.Profile` and insert the following line into the second <scheme> section.

```
DefaultSaveFormat=".rtf"

```

It should look similar to the following:

```
<Scheme
   name="_custom_"
   ZoomPercentage="64"
   DefaultSaveFormat=".rtf"
/>

```

It is then neccessary to change the default template. You must follow these steps exactly.

1.  Open Abiword and save a blank document titled `normal.rtf` in `~/.AbiSuite/templates/`. If the directory does not exist, create it.
2.  Rename the file to *normal.awt*.

Do **not** just save a blank `.awt` file! You must trick Abiword into using a `.rtf` template in order for this to work.

As soon as the conflict between Abiword and libgnomeprint is resovled, these instructions will no longer be neccessary and should be removed.