Related articles

*   [tmux](/index.php/Tmux "Tmux")

[tmuxp](https://tmuxp.git-pull.com) is a session manager for the [tmux](/index.php/Tmux "Tmux") terminal multiplexer. Compare to [tmuxinator](https://github.com/tmuxinator/tmuxinator) or [teamocil](https://github.com/remiprev/teamocil).

## Installation

Install the [tmuxp](https://www.archlinux.org/packages/?name=tmuxp) package.

```
$ pacman -S tmuxp

```

## Configurations

*tmuxp* accepts both JSON and YAML configurations. The YAML markup is similar to *tmuxinator'*s.

You can put configurations in any directory to access them via 3 ways:

1.  Via absolute or relative file path `tmuxp load *file*`, `tmuxp load ../*myconfig*`
2.  In the `$TMUXP_CONFIGDIR` path (default `$HOME/.tmuxp`) and access them via `tmuxp load *basename*`. So `$HOME/.tmuxp/*myconfig*.yaml` would be loadable via `tmuxp load myconfig`.
3.  Via `.tmuxp.yaml` in a project or directory (so you can store configs in a VCS per-project / folder. And then `tmuxp load *path/to/dir*`

A sample YAML configuration with 4 panes:

```
session_name: 4-pane-split
windows:
- window_name: dev window
  layout: tiled
  shell_command_before:
    - cd ~/                    # run as a first command in all panes
  panes:
    - shell_command:           # pane no. 1
        - cd /var/log          # run multiple commands in this pane
        - ls -al | grep \.log
    - echo second pane         # pane no. 2
    - echo third pane          # pane no. 3
    - echo forth pane          # pane no. 4

```

*tmuxp* is also capable of running arbitrary scripts before building *tmux* sessions via `before_script`. In this example, [from the tmuxp project itself](https://github.com/tony/tmuxp/blob/master/.tmuxp.yaml), a [bootstrap script](https://github.com/tony/tmuxp/blob/master/bootstrap_env.py) runs which creates a [virtualenv](/index.php/Virtualenv "Virtualenv") (python package environment) for the project and installs dependency packages. In addition, the session configures all panes to source the project's *virtualenv*:

```
session_name: tmuxp
start_directory: ./ # load session relative to config location (project root).
before_script: ./bootstrap_env.py # ./ to load relative to project root.
windows:
- window_name: tmuxp
  focus: True
  layout: main-horizontal
  options:
    main-pane-height: 35
  shell_command_before:
    - '[ -d .venv -a -f .venv/bin/activate ] && source .venv/bin/activate'
  panes:
  - focus: true
  - pane 
  - make watch_test
- window_name: docs
  layout: main-horizontal
  options:
    main-pane-height: 35
  start_directory: doc/
  shell_command_before: 
    - '[ -d ../.venv -a -f ../.venv/bin/activate ] && source ../.venv/bin/activate'
  panes:
  - focus: true
  - pane
  - make serve
  - make watch

```

[More examples](https://tmuxp.git-pull.com/en/latest/examples.html) are available in the documentation showcasing YAML, as well as JSON configurations.

## See also

*   [Official Homepage](https://tmuxp.git-pull.com), including documentation and examples
*   [GitHub](https://www.github.com/tony/tmuxp)
*   [PyPI package](https://pypi.org/project/tmuxp/)