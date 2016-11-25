[Nash](https://github.com/NeowayLabs/nash) (or Nash shell) is a minimalist yet powerful [shell](/index.php/Shell "Shell") with focus on readability and security of scripts. It is inspired by Plan9 [rc](https://en.wikipedia.org/wiki/rc) shell and brings to Linux a similar approach to [namespaces(7)](http://man7.org/linux/man-pages/man7/namespaces.7.html) creation. There is a *nashfmt* program to correctly format nash scripts in a readable manner, much like the Golang [gofmt](https://golang.org/cmd/gofmt/) program.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Organizing the init](#Organizing_the_init)
    *   [2.2 Configuring $PATH](#Configuring_.24PATH)
    *   [2.3 Making nash your default shell](#Making_nash_your_default_shell)
*   [3 Usage](#Usage)
    *   [3.1 Keybindings](#Keybindings)
*   [4 See also](#See_also)

## Installation

Install the [nash-git](https://aur.archlinux.org/packages/nash-git/) package.

## Configuration

Make sure that nash has been successfully installed issuing the command below in your current shell:

 `$ nash` 
```
λ>

```

If it returned a lambda prompt, then everything is fine.

When first executed, nash will create a `~/.nash/` directory in the user's homepath. Enter the command below to discover by yourself what is this directory:

 `λ> echo $NASHPATH` 
```
/home/*username*/.nash

```

Put a file called `init` inside this directory to configure it.

Nash only has 1 special variables:

*   `PROMPT` variable stores the unicode string used for the shell prompt.

*Nash* default *cd* is a very simple alias to the builtin function *chdir*; you may find it odd to use. To improve your usage you can create your own *cd* alias. In nash you cannot create aliases by matching string to strings, but only binding function to command names. The *init* below creates a *cd* alias as example:

```
defPROMPT = "λ> "

fn cd(path) {
        if $path == "" {
                path = $HOME
        }

        chdir($path)
        PROMPT = "("+$path+")"+$defPROMPT
        setenv PROMPT
}

# bind the "cd" function to "cd" command name
bindfn cd cd
```

After saving the init file, simply start a new shell and now you can use *cd* as if it were a builtin keyword.

```
git:(master)λ> nash
λ> cd
(/home/i4k)λ> cd /usr/local
(/usr/local)λ>

```

For a more elaborated *cd* or other aliases implementation, see the project [dotnash](https://github.com/tiago4orion/dotnash).

### Organizing the init

*Nash* scripts can be modular, but there is no concept of package. You can use the *import* keyword to load other files inside the current script session. For an example, see [dotnash init](https://github.com/tiago4orion/dotnash/blob/master/init).

### Configuring $PATH

Inside the *init* put the code below (edit for your needs):

```
path = (
        "/bin"
        "/usr/bin"
        "/usr/local/bin"
        $HOME+"/bin"
)

PATH = ""

for p in $path {
        PATH = $PATH+":"+$p
}

setenv PATH
```

### Making nash your default shell

See [Command-line shell#Changing your default shell](/index.php/Command-line_shell#Changing_your_default_shell "Command-line shell").

## Usage

### Keybindings

The *cli* supports *emacs* and *vi* modes for common buffer editing. Default mode is *emacs* and you can change issuing:

```
λ> set mode vi

```

## See also

*   [Nash shell](https://github.com/NeowayLabs/nash)
*   [dotnash](https://github.com/tiago4orion/dotnash)
*   [Autocomplete for nash shell](https://github.com/NeowayLabs/nashcomplete)