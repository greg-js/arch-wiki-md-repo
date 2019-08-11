[fish](https://fishshell.com), the ***f**riendly **i**nteractive **sh**ell*, is a [commandline shell](/index.php/Command-line_shell "Command-line shell") intended to be interactive and user-friendly.

*fish* is intentionally not fully [POSIX](https://en.wikipedia.org/wiki/POSIX "wikipedia:POSIX") compliant, it aims at addressing POSIX inconsistencies (as perceived by the creators) with a simplified or a different syntax. This means that even simple POSIX compliant scripts may require some significant adaptation or even full rewriting to run with fish.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 System integration](#System_integration)
    *   [2.1 Setting fish as default shell](#Setting_fish_as_default_shell)
    *   [2.2 Setting fish as interactive shell only](#Setting_fish_as_interactive_shell_only)
        *   [2.2.1 Modify .bashrc to drop into fish](#Modify_.bashrc_to_drop_into_fish)
        *   [2.2.2 Use terminal emulator options](#Use_terminal_emulator_options)
        *   [2.2.3 Use terminal multiplexer options](#Use_terminal_multiplexer_options)
*   [3 Configuration](#Configuration)
    *   [3.1 Web interface](#Web_interface)
    *   [3.2 Command completion](#Command_completion)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Command substitution](#Command_substitution)
    *   [4.2 Command chaining](#Command_chaining)
    *   [4.3 Disable greeting](#Disable_greeting)
    *   [4.4 Make su launch fish](#Make_su_launch_fish)
    *   [4.5 Start X at login](#Start_X_at_login)
    *   [4.6 Use liquidprompt](#Use_liquidprompt)
    *   [4.7 Put git status in prompt](#Put_git_status_in_prompt)
    *   [4.8 Color the hostname in the prompt in SSH](#Color_the_hostname_in_the_prompt_in_SSH)
    *   [4.9 Evaluate ssh-agent](#Evaluate_ssh-agent)
    *   [4.10 The "command not found" hook](#The_"command_not_found"_hook)
    *   [4.11 Remove a process from the list of jobs](#Remove_a_process_from_the_list_of_jobs)
    *   [4.12 Set a persistent alias](#Set_a_persistent_alias)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [fish](https://www.archlinux.org/packages/?name=fish) package. For the development version, install the [fish-git](https://aur.archlinux.org/packages/fish-git/) package.

Once installed, simply type `fish` to drop into the fish shell.

Documentation can be found by typing `help` from fish; it will be opened in a web browser. It is recommended to read at least the "Syntax overview" section, since fish's syntax is different from many other shells.

## System integration

One must decide whether fish is going to be the default user's shell, which means that the user falls directly in fish at login, or whether it is used in interactive terminal mode as a child process of the current default shell, here we will assume the latter is [Bash](/index.php/Bash "Bash"). To elaborate on these two setups:

*   fish used as the **default shell**: this mode requires some basic understanding of the fish functioning and its scripting language. The user's current initialization scripts and environment variables need to be migrated to the new fish environment. To configure the system in this mode, follow [#Setting fish as default shell](#Setting_fish_as_default_shell).

*   fish used as an **interactive shell only**: this is the less disruptive mode, all the Bash initialization scripts are run as usual and fish runs on top of Bash in interactive mode connected to a terminal. To setup fish in this mode, follow [#Setting fish as interactive shell only](#Setting_fish_as_interactive_shell_only).

### Setting fish as default shell

If you decide to set fish as the default user shell, the first step is to set the shell of this particular user to `/usr/bin/fish`. This can be done by following the instructions in [Command-line shell#Changing your default shell](/index.php/Command-line_shell#Changing_your_default_shell "Command-line shell").

The next step is to port the current needed actions and configuration performed in the various Bash initialization scripts, namely `/etc/profile`, `~/.bash_profile`, `/etc/bash.bashrc` and `~/.bashrc`, into the fish framework.

In particular, the content of the `$PATH` environment variable, once directly logged under fish, should be checked and adjusted to one's need. In fish, `$PATH` is defined as a *global environment variable*: it has a *global* scope across all functions, it is lost upon reboot and it is an *environment variable* which means it is exported to child processes. The recommended way of adding permanently additional locations to the path is by assigning them to the `fish_user_paths` universal variable. This variable is automatically added to `$PATH` and is preserved across restarts of the shell. For example by setting:

```
$ set -U fish_user_paths */first/path* */second/path* */third/one*

```

These three locations will be permanently prepended to the path. This is an easy way to complement the path without the need to add any instruction in scripts.

### Setting fish as interactive shell only

Not setting fish as system wide or user default allows the current Bash scripts to run on startup. It ensures the current user's environment variables are unchanged and are exported to fish which then runs as a Bash child. Below are several ways of running fish in interactive mode without setting it as the default shell.

#### Modify .bashrc to drop into fish

Keep the default shell as Bash and simply add the line `exec fish` to the appropriate [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash"), such as `.bashrc`. This will allow Bash to properly source `/etc/profile` and all files in `/etc/profile.d`. Because fish replaces the Bash process, exiting fish will also exit the terminal. Compared to the following options, this is the most universal solution, since it works both on a local machine and on a SSH server.

**Tip:**

*   In this setup, use `bash --norc` to manually enter Bash without executing the commands from `~/.bashrc` which would run `exec fish` and drop back into fish.
*   To have commands such as `bash -c 'echo test'` run the command in Bash instead of starting fish, you can write `if [ -z "$BASH_EXECUTION_STRING" ]; then exec fish; fi` instead.

#### Use terminal emulator options

Another option is to open your terminal emulator with a command line option that executes fish. For most terminals this is the `-e` switch, so for example, to open gnome-terminal using fish, change your shortcut to use:

```
gnome-terminal -e fish

```

With terminal emulators that do not support setting the shell, for example [lilyterm-git](https://aur.archlinux.org/packages/lilyterm-git/), it would look like this:

```
SHELL=/usr/bin/fish lilyterm

```

Also, depending on the terminal, you may be able to set fish as the default shell in either the terminal configuration or the terminal profile.

#### Use terminal multiplexer options

To set fish as the shell started in [tmux](/index.php/Tmux "Tmux"), put this into your `~/.tmux.conf`:

```
set-option -g default-shell "/usr/bin/fish"

```

Whenever you run *tmux*, you will be dropped into fish.

## Configuration

The configuration file runs at every login and is located at `~/.config/fish/config.fish`. Adding commands or functions to the file will execute/define them when opening a terminal, similar to `.bashrc`. Note that whenever a variable needs to be preserved, it be set as *universal* rather than defined in the aforementioned configuration file.

The user's functions are located in the directory `~/.config/fish/functions` under the filenames `*function_name*.fish`.

### Web interface

The fish terminal colors, prompt, functions, variables, history, bindings and abbreviations can be set with the interactive web interface:

```
fish_config

```

### Command completion

fish can generate autocompletions from man pages. Completions are written to `~/.local/share/fish/generated_completions/` and can be generated by calling:

```
fish_update_completions

```

You can also define your own completions in `~/.config/fish/completions/`. See `/usr/share/fish/completions/` for a few examples.

Context-aware completions for Arch Linux-specific commands like *pacman*, *pacman-key*, *makepkg*, *cower*, *pbget*, *pacmatic* are built into fish, since the policy of the fish development is to include all the existent completions in the upstream tarball. The memory management is clever enough to avoid any negative impact on resources.

## Tips and tricks

### Command substitution

*fish* does not implement Bash style history substitution (e.g. `sudo !!`), and the developers recommend in the [fish faq](http://fishshell.com/docs/current/faq.html#faq-history) to use the interactive history recall interface instead: the `Up` arrow recalls whole past lines and `Alt+Up` recalls individual arguments.

However some workarounds are described in the [fish wiki](https://github.com/fish-shell/fish-shell/wiki/Bash-Style-Command-Substitution-and-Chaining-(!!-!$-&&-%7C%7C)): while not providing complete history substitution, some functions replace `!!` with the previous command or `!$` with the previous last argument.

### Command chaining

Command chaining `&&` and `||` is not implemented in versions older than 3.0 and the recommended syntax to achieve similar results in *fish* is respectively `; and` and `; or`. Some keybindings can be set for automatic substitution as described in the [fish wiki](https://github.com/fish-shell/fish-shell/wiki/Bash-Style-Command-Substitution-and-Chaining-(!!-!$-&&-%7C%7C)#getting--and-).

### Disable greeting

By default, fish prints a greeting message at startup. To disable it, run once:

```
 $ set -U fish_greeting

```

This clears the universal `fish_greeting` variable, shared with all fish instances and which is preserved upon restart of the shell.

### Make su launch fish

If *su* starts with Bash because Bash is the target user's (*root* if no username is provided) default shell, one can define a function to redirect it to fish whatever the user's shell:

 `~/.config/fish/functions/su.fish` 
```
function su
   command su --shell=/usr/bin/fish $argv
end
```

### Start X at login

Add the following to the bottom of your `~/.config/fish/config.fish`.

```
# Start X at login
if status is-login
    if test -z "$DISPLAY" -a $XDG_VTNR = 1
        exec startx -- -keeptty
    end
end

```

### Use liquidprompt

[Liquidprompt](https://github.com/nojhan/liquidprompt) is a popular "full-featured & carefully designed adaptive prompt for Bash & Zsh" and has no plans to make it compatible with fish [[1]](https://github.com/nojhan/liquidprompt/pull/230). The [angel-PS1](https://github.com/dolmen/angel-PS1) project implements it's functionality for fish.

### Put git status in prompt

If you would like fish to display the branch and dirty status when you are in a git directory, you can define the following `fish_prompt` function:

 `~/.config/fish/functions/fish_prompt.fish` 
```
function fish_prompt
  set -l last_status $status

  if not set -q __fish_git_prompt_show_informative_status
    set -g __fish_git_prompt_show_informative_status 1
  end
  if not set -q __fish_git_prompt_color_branch
    set -g __fish_git_prompt_color_branch brmagenta
  end
  if not set -q __fish_git_prompt_showupstream
    set -g __fish_git_prompt_showupstream "informative"
  end
  if not set -q __fish_git_prompt_showdirtystate
    set -g __fish_git_prompt_showdirtystate "yes"
  end
  if not set -q __fish_git_prompt_color_stagedstate
    set -g __fish_git_prompt_color_stagedstate yellow
  end
  if not set -q __fish_git_prompt_color_invalidstate
    set -g __fish_git_prompt_color_invalidstate red
  end
  if not set -q __fish_git_prompt_color_cleanstate
    set -g __fish_git_prompt_color_cleanstate brgreen
  end

  printf '%s%s %s%s%s%s ' (set_color $fish_color_host) (prompt_hostname) (set_color $fish_color_cwd) (prompt_pwd) (set_color normal) (__fish_git_prompt)

  if not test $last_status -eq 0
    set_color $fish_color_error
  end
  echo -n '$ '
  set_color normal
end

```

However, this is now deprecated, see [fish-shell git](https://github.com/fish-shell/fish-shell/blob/master/share/functions/__fish_git_prompt.fish). Alternatively, the [Informative Git Prompt](http://mariuszs.github.io/blog/2013/informative_git_prompt.html) has now been built into fish and can be activated from fish_config if so desired.

### Color the hostname in the prompt in SSH

To color the hostname in the prompt dynamically whenever connected through SSH, add the following lines in either the `fish_prompt` function or the fish configuration file, here using the red color:

 `~/.config/fish/functions/fish_prompt.fish` 
```
...
if set -q SSH_TTY
  set -g fish_color_host brred
end
...
```

### Evaluate ssh-agent

In fish, `eval (ssh-agent)` generate errors due to how variables are set. To work around this, use the csh-style option `-c`:

```
 $ eval (ssh-agent -c)

```

### The "command not found" hook

[pkgfile](/index.php/Pkgfile "Pkgfile") includes a "command not found" hook that will automatically search the official repositories, when entering an unrecognized command. This hook will be run by default if [pkgfile](https://www.archlinux.org/packages/?name=pkgfile) is installed.

### Remove a process from the list of jobs

*fish* terminates any jobs put into the background when fish terminates. To keep a job running after fish terminates, first use the `disown` builtin. For example, the following starts `firefox` in the background and then disowns it:

```
 $ firefox &
 $ disown

```

This means firefox will not be closed when the fish process is closed. See disown(1) in *fish* for more details.

### Set a persistent alias

To quickly make a persistent alias, one can simply use the method showed in this example:

```
$ alias lsl "ls -l"
$ funcsave lsl

```

This will create the function:

```
function lsl
    ls -l $argv
end

```

and will set the alias as a persistent shell function. To see all functions and/or edit them, one can simply use `fish_config` and look into the *Function* tab in the web configuration page.

For more detailed information, refer to [fish - alias](https://fishshell.com/docs/current/commands.html#alias).

## See also

*   [http://fishshell.com/](http://fishshell.com/) - Home page
*   [http://fishshell.com/docs/current/index.html](http://fishshell.com/docs/current/index.html) - Documentation
*   [http://hyperpolyglot.org/unix-shells](http://hyperpolyglot.org/unix-shells) - Shell grammar correspondence table
*   [https://github.com/fish-shell/fish-shell](https://github.com/fish-shell/fish-shell) - fish on GitHub