**Status de tradução:** Esse artigo é uma tradução de [AbiWord](/index.php/AbiWord "AbiWord"). Data da última tradução: 2019-01-09\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=AbiWord&diff=0&oldid=562520) na versão em inglês.

[AbiWord](http://www.abisource.com/) é um processador de texto que oferece uma alternativa mais leve para o [LibreOffice](/index.php/LibreOffice "LibreOffice") Writer e o [OpenOffice](/index.php/OpenOffice "OpenOffice") Writer, ao mesmo tempo em que fornece excelente funcionalidade. O AbiWord possui suporte a muitos tipos de documentos padrão, como documentos ODF, documentos do Microsoft Word, documentos do WordPerfect, documentos em formato Rich Text e páginas da Web em HTML.

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

Desde a versão 3.0, AbiWord vai usar `~/.config/abiword` para armazenar arquivos do usuário.

Versões anteriores do AbiWord usavam `~/.config/AbiSuite` e, se este diretório for encontrado na inicialização do programa, ele será automaticamente renomeado. Se `~/.config/AbiSuite` e `~/.config/abiword` não existirem, o AbiWord **não** vai criá-lo.

## Modelos

AbiWord fornece um sistema de modelos que permite agilizar a escrita de documentos comuns. Modelos são fornecidos como arquivos *.awt*, para **A**bi**W**ord **T**emplate.

Arquivos de modelos são procurados dentro das pastas `/usr/share/abiword-3.0/templates` e `~/.config/abiword/templates`.

### Usando modelos

Em um novo documento, escolha *Arquivo > Novo a partir de Modelo...*, então, na caixa de diálogo "Escolha um modelo", selecione um dos modelos encontrados e listados, ou clique em "Abrir" para navegar pelos seus arquivos para um arquivo do AbiWord (não necessariamente um arquivo *.awt*).

### Criando ou alterando modelos

AbiWord possibilita que você faça seus próprios arquivos de modelos, com os estilos, textos, tabelas etc. desejados.

Para criar/alterar um arquivo de modelo, basta abrir um novo documento ou existente, e fazer as alterações desejadas a esse arquivo. Então, use a opção de menu "Salvar Como" para nomeá-lo como quiser, com *.awt* como extensão (por exemplo, *foobar.awt*) e salvá-lo na pasta `~/.config/abiword/templates`. Agora, seu novo modelo pode ser acessado em *Arquivo > Novo a partir de Modelo...* pelo seu nome de arquivo (*foobar.awt* no exemplo dado).

**Nota:** Se não existir, a pasta `templates` será criada automaticamente na inicialização dentro de `~/.config/abiword-3.0/`.

## Verificação gramatical

Habilite verificação gramatical em *Editar > Opções > Verificação Ortográfica > Verificação automática e gramática*.

## Alterar associações de teclas

**Nota:** [Essa página de wiki](http://www.abisource.com/wiki/Keyboard_bindings) têm instruções sobre isso, mas algumas estão desatualizadas e não funcionam

Você pode alterar as associações de teclas padrão no AbiWord usando [KeyBindings](https://www.abisource.com/wiki/KeyBindings).

Para definir as associações de teclas, edite `~/.config/abiword/profile` e, dentro da seção `AbiPreferences`, adicione as *KeyBindings* desejadas. Por exemplo, você pode adicionar `KeyBindings="viEdit"` ou `KeyBindings="emacs"`.

## Fontes LaTeX

O pacote [abiword](https://www.archlinux.org/packages/?name=abiword) vem com uma função que permite ao usuário inserir códigos LaTeX em um documento. Para exibir os símbolos de matemática corretamente, é necessário fazer o download [latex-xft-fonts](http://movementarian.org/latex-xft-fonts-0.1.tar.gz) e salvá-lo no diretório `/usr/share/fonts`. Para instalar a fonte, extraia o tarball e execute o seguinte:

```
# fc-cache -fv

```

## Solução de problemas

### Correção para travamento do diálogo de impressão

**Nota:** Este erro foi relatado como inexistente para a versão 2.8.1 ou superior. No entanto, esta seção permanecerá para versões legadas ou se aparecer novamente.

Por alguma razão, as versões atuais do AbiWord e do [libgnomeprint](https://aur.archlinux.org/packages/libgnomeprint/) não estão funcionando bem juntas. O modelo padrão `.abw` faz com que o programa trave quando o usuário tenta imprimir. A solução é forçar o AbiWord a trabalhar com o formato `.rtf`. Seguindo os passos abaixo, você irá configurar o formato de salvamento padrão para .rtf e enganar o AbiWord para usar um arquivo `.rtf` como seu modelo padrão.

Abra `~/.AbiSuite/AbiWord.Profile` e insira a seguinte linha na segunda seção <scheme>.

```
DefaultSaveFormat=".rtf"

```

Ele deve se parecer com o seguinte:

```
<Scheme
   name="_custom_"
   ZoomPercentage="64"
   DefaultSaveFormat=".rtf"
/>

```

Então, é necessário alterar o modelo padrão. Você deve seguir os seguintes passos.

1.  Abra o AbiWord e salve um documento vazio com título `normal.rtf` em `~/.AbiSuite/templates/`. Se o diretório não existir, crie-o.
2.  Renomeie o arquivo para *normal.awt*.

**Não** apenas salve um arquivo `.awt` vazio! Você deve enganar o AbiWord para usar um modelo `.rtf` na pasta para isso funcionar.

Assim que o conflito entre AbiWord e *libgnomeprint* for resolvido, essas instruções não serão mais necessárias e deverão ser removidas.