[fish](https://fishshell.com), the ***f**riendly **i**nteractive **sh**ell*, is a [commandline shell](/index.php/Command-line_shell "Command-line shell") intended to be interactive and user-friendly.

*fish* is intentionally not fully [POSIX](https://en.wikipedia.org/wiki/POSIX "wikipedia:POSIX") compliant, it aims at addressing POSIX inconsistencies (as perceived by the creators) with a simplified or a different syntax. This means that even simple POSIX compliant scripts may require some significant adaptation or even full rewriting to run with fish.

## Contents

*   [1 Installation](#Installation)
*   [2 System integration](#System_integration)
    *   [2.1 Setting fish as default shell](#Setting_fish_as_default_shell)
    *   [2.2 Setting fish as secondary shell](#Setting_fish_as_secondary_shell)
        *   [2.2.1 Modify .bashrc to drop into fish](#Modify_.bashrc_to_drop_into_fish)
        *   [2.2.2 Use terminal emulator options](#Use_terminal_emulator_options)
        *   [2.2.3 Use terminal multiplexer options](#Use_terminal_multiplexer_options)
*   [3 Configuration](#Configuration)
    *   [3.1 Web interface](#Web_interface)
    *   [3.2 Command completion](#Command_completion)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Disable greeting](#Disable_greeting)
    *   [4.2 Make su launch fish](#Make_su_launch_fish)
    *   [4.3 Start X at login](#Start_X_at_login)
    *   [4.4 Use liquidprompt](#Use_liquidprompt)
    *   [4.5 Put git status in prompt](#Put_git_status_in_prompt)
    *   [4.6 Evaluate ssh-agent](#Evaluate_ssh-agent)
    *   [4.7 The "command not found" hook](#The_.22command_not_found.22_hook)
    *   [4.8 Remove a process from the list of jobs](#Remove_a_process_from_the_list_of_jobs)
    *   [4.9 Quickly set a persistent alias](#Quickly_set_a_persistent_alias)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 History substitution](#History_substitution)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [fish](https://www.archlinux.org/packages/?name=fish) package. For the development version, install the [fish-git](https://aur.archlinux.org/packages/fish-git/) package.

Once installed simply type `fish` to drop into the fish shell.

Documentation can be found by typing `help` from fish; it will be opened in a web browser. It is recommended to read at least the "Syntax overview" section, since fish's syntax is different from many other shells.

## System integration

One must decide whether fish is going to be the default user's shell, which means that the user falls directly in fish at login or whether it is used in interactive terminal mode as a child process of the current default shell, here we will assume the latter is [Bash](/index.php/Bash "Bash"). To elaborate on these two setups:

*   fish used as an **interactive shell** only: this is the less disruptive mode, all the Bash initialization scripts are run as usual and fish runs on top of Bash in interactive mode connected to a terminal. To setup fish in this mode, follow [#Setting fish as secondary shell](#Setting_fish_as_secondary_shell).

*   fish used as the **default shell**: this mode requires some basic understanding of the fish functioning and its scripting language. The user's current initialization scripts and environment variables needs to be migrated to the new fish environment. To configure the system in this mode, follow [#Setting fish as default shell](#Setting_fish_as_default_shell).

### Setting fish as default shell

If you decide to set fish as the default user shell, the first step is to set the shell of this particular user to `/usr/bin/fish`. This can be done by following the instructions in [Command-line shell#Changing your default shell](/index.php/Command-line_shell#Changing_your_default_shell "Command-line shell").

Then, the next step is to port the current needed actions and configuration performed in the various Bash initialization scripts, namely `/etc/profile`, `~/.bash_profile`, `/etc/bash.bashrc` and `~/.bashrc`, into the fish framework.

In particular the content of the `$PATH` environment variable once directly logged under fish should be checked and adjusted to one's need. In fish the `$PATH` is a global environment variable, which means that it is exported to child processes and lost upon reboot. The recommended way of adding permanently additional locations to the path is by assigning the desired locations to the `fish_user_paths` universal variable. This variable is automatically added to `$PATH` and is preserved across restarts of the shell. For example by setting:

```
$ set -U fish_user_paths */first/path* */second/path* */third/one*

```

These three locations will be permanently prepended to the path. This is an easy way to complement the path without the need to add any instruction in scripts.

### Setting fish as secondary shell

Not setting fish as system wide or user default allows the current Bash scripts to run on startup. It ensures the current user's environment variables are unchanged and are exported to fish which then runs as a Bash child. Below are several options for using fish without setting it as the default shell.

#### Modify .bashrc to drop into fish

Keep the default shell as Bash and simply add the line `exec fish` to the appropriate [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash"), such as `.bashrc`. This will allow Bash to properly source `/etc/profile` and all files in `/etc/profile.d`. Because fish replaces the Bash process, exiting fish will also exit the terminal. Compared to the following options, this is the most universal solution, since it works both on a local machine and on a SSH server.

**Tip:**

*   In this setup, use `bash --norc` to manually enter Bash without executing the commands from `~/.bashrc` which would run `exec fish` and drop back into fish.
*   To have commands such as `bash -c 'echo test'` run the command in bash instead of starting fish, you can write `if [ -z "$BASH_EXECUTION_STRING" ]; then exec fish; fi` instead. (This is necessary for EternalTerminal to work.)
*   To color the hostname in the prompt differently in SSH mode, here in bright red, one can use the line `if [ -n "$SSH_TTY" ]; then exec fish -C 'set -g fish_color_host brred'; else exec fish; fi` in the Bash configuration file instead of simply `exec fish`.

#### Use terminal emulator options

Another option is to open your terminal emulator with a command line option that executes fish. For most terminals this is the `-e` switch, so for example, to open gnome-terminal using fish, change your shortcut to use:

```
gnome-terminal -e fish

```

With LilyTerm and other light terminal emulators that do not support setting the shell it would look like this:

```
SHELL=/usr/bin/fish lilyterm

```

You can also set fish as the default shell for the terminal in the terminal's configuration or for a terminal profile if your terminal emulator has a profiles feature.

Whenever you open your terminal emulator, you will be dropped into fish.

#### Use terminal multiplexer options

To set fish as the shell started in tmux, put this into your `~/.tmux.conf`:

```
set-option -g default-shell "/usr/bin/fish"

```

Whenever you run *tmux*, you will be dropped into fish.

## Configuration

User configurations for fish are located at `~/.config/fish/config.fish`. Adding commands or functions to the file will execute/define them when opening a terminal, similar to `.bashrc`.

### Web interface

The fish prompt and terminal colors can be set with the interactive web interface:

```
fish_config

```

Selected settings are written to your personal configuration file. You can also view defined functions and your history.

### Command completion

fish can generate autocompletions from man pages. Completions are written to `~/.config/fish/generated_completions/` and can be generated by calling:

```
fish_update_completions

```

You can also define your own completions in `~/.config/fish/completions/`. See `/usr/share/fish/completions/` for a few examples.

Context-aware completions for Arch Linux-specific commands like *pacman*, *pacman-key*, *makepkg*, *cower*, *pbget*, *pacmatic* are built into fish, since the policy of the fish development is to include all the existent completions in the upstream tarball. The memory management is clever enough to avoid any negative impact on resources.

## Tips and tricks

### Disable greeting

By default, fish prints a greeting message at startup. To disable it, run once:

```
 $ set -U fish_greeting

```

This clears the universal `fish_greeting` variable, shared with all fish instances and which is preserved upon restart of the shell.

### Make su launch fish

If *su* starts with Bash (because Bash is the default shell), define a function in your fish configuration file:

```
function su
    /bin/su --shell=/usr/bin/fish $argv
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

[Liquidprompt](https://github.com/nojhan/liquidprompt) is a popular "full-featured & carefully designed adaptive prompt for Bash & Zsh" and has no plans to make it compatible with fish [[1]](https://github.com/nojhan/liquidprompt/pull/230). [This project](https://github.com/wesbarnett/fish-lp) implements it for fish.

### Put git status in prompt

If you would like fish to display the branch and dirty status when you are in a git directory, you can add the following to your `~/.config/fish/config.fish`:

```
# fish git prompt
set __fish_git_prompt_showdirtystate 'yes'
set __fish_git_prompt_showstashstate 'yes'
set __fish_git_prompt_showupstream 'yes'
set __fish_git_prompt_color_branch yellow

# Status Chars
set __fish_git_prompt_char_dirtystate '⚡ '
set __fish_git_prompt_char_stagedstate '→ '
set __fish_git_prompt_char_stashstate '↩ '
set __fish_git_prompt_char_upstream_ahead '↑ '
set __fish_git_prompt_char_upstream_behind '↓ '

function fish_prompt
    printf '%s@%s %s%s%s%s> ' (whoami) (hostname) (set_color $fish_color_cwd) (prompt_pwd) (set_color normal) (__fish_git_prompt)
end

```

More explanations about the parameters can be found in the [fish-shell git](https://github.com/fish-shell/fish-shell/blob/master/share/functions/__fish_git_prompt.fish).

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

### Quickly set a persistent alias

To quickly make a persistent alias, one can simply open up fish shell and use the following method:

```
$ alias FooAliasName "foo"
$ funcsave FooAliasName

```

This will set you alias as a persistent fish shell function. if you wish to see all functions and/or edit them, one can simply use `fish_config` to view or edit all functions under the **Function** tab in the resulting web configuration page.

## Troubleshooting

### History substitution

Fish does not implement history substitution (e.g. `sudo !!`), and the fish developers have said that they [do not plan to](http://fishshell.com/docs/current/faq.html#faq-history). Still, this is an essential piece of many users' workflow. Reddit user, [crossroads1112](http://www.reddit.com/u/crossroads1112), created a function that regains some of the functionality of history substitution and with another syntax. The function is on [github](https://gist.github.com/crossroads1112/77badb2c3455e23b873b) and instructions are included as comments in it. There is a [forked version](https://gist.github.com/b-/981892a65837ab0a387e) that is closer to the original syntax and allows for `command !!` if you specify the command in the helper function.

Other alternatives to regaining the `command !!` syntax can be found on [Fish' github wiki](https://github.com/fish-shell/fish-shell/wiki/Bash-Style-History-Substitution-%28%21%21-and-%21%24%29). The examples here include e.g. the `bind_bang` function which expands `!!` to the latest command in the history (this will of course make it impossible to do to bangs in a row as they will expand). Another option is the command given on [this github issue](https://github.com/fish-shell/fish-shell/issues/288#issuecomment-158704275).

## See also

*   [http://fishshell.com/](http://fishshell.com/) - Home page
*   [http://fishshell.com/docs/current/index.html](http://fishshell.com/docs/current/index.html) - Documentation
*   [http://hyperpolyglot.org/unix-shells](http://hyperpolyglot.org/unix-shells) - Shell grammar correspondence table