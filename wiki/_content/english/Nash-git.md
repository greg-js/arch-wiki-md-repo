[Nash](https://github.com/NeowayLabs/nash) is a minimalist and yet powerful shell with focus on readability and security of scripts. It's inspired by Plan9 [rc](https://en.wikipedia.org/wiki/rc) shell and brings to linux a similar approach to [namespace](http://man7.org/linux/man-pages/man7/namespaces.7.html) creation. There's a *nashfmt* program to correctly format nash scripts in a readable manner (much like Golang [gofmt](https://golang.org/cmd/gofmt/) program).

## Contents

*   [1 Installation](#Installation)
*   [2 Initial configuration](#Initial_configuration)
*   [3 Organizing the init](#Organizing_the_init)
*   [4 Configuring $PATH](#Configuring_.24PATH)
*   [5 Making nash your default shell](#Making_nash_your_default_shell)
*   [6 Keybindings](#Keybindings)
*   [7 See also](#See_also)

### Installation

Install the [nash-git](https://aur.archlinux.org/packages/nash-git/) package.

### Initial configuration

Make sure that nash has been successfull installed issuing the command below in your current shell:

```
$ nash
λ>

```

If you got a lambda prompt, the everything is fine.

When first executed, nash will create a .nash directory in $HOME. Enter the command below to discover by yourself what is this directory:

```
λ> echo $NASHPATH
/home/i4k/.nash

```

Put a file called init inside this directory to configure it.

Nash only has 2 special variables:

*   PROMPT variable stores the unicode string used for ... you know
*   IFS is a list containing the set of character delimiters used internally to split command output into lists.

*Nash* doesn't have a *cd* builtin, but a builtin function *chdir*. In nash you cannot create aliases by matching string to strings, but only binding function to command names. The *init* below creates a *cd* alias:

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

After saving the init file, simple start a new shell and now you can use cd as if it were a builtin keyword.

```
git:(master)λ> nash
λ> cd
(/home/i4k)λ> cd /usr/local
(/usr/local)λ>

```

For a more elaborated *cd* or other aliases implementation, see the project [dotnash](https://github.com/tiago4orion/dotnash).

### Organizing the init

*Nash* scripts can be modular, but there's no concept of package. You can use the *import* keyword to load other files inside the current script session. For an example, see [dotnash init](https://github.com/tiago4orion/dotnash/blob/master/init).

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

See [https://wiki.archlinux.org/index.php/Command-line_shell#Changing_your_default_shell](https://wiki.archlinux.org/index.php/Command-line_shell#Changing_your_default_shell)

### Keybindings

The *cli* supports *emacs* and *vi* modes for common buffer editing. Default mode is *emacs* and you can change issuing:

```
λ> set mode vi

```

### See also

[nash](https://github.com/NeowayLabs/nash)

[dotnash](https://github.com/tiago4orion/dotnash)