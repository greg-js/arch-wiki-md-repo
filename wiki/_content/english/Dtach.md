dtach "is a tiny program that emulates the detach feature of screen, allowing you to run a program in an environment that is protected from the controlling terminal and attach to it later." [[1]](http://dtach.sourceforge.net/)

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Create a new session](#Create_a_new_session)
    *   [2.2 Attach to a session](#Attach_to_a_session)
    *   [2.3 Detach from a session](#Detach_from_a_session)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Share a session](#Share_a_session)

## Installation

[Install](/index.php/Install "Install") the [dtach](https://www.archlinux.org/packages/?name=dtach) package.

## Usage

### Create a new session

To create a new session running *command* and attach to it:

```
$ dtach -c *socket* *command*

```

For example, to create a new session running *bash* with the socket located at `/tmp/bashsession`:

```
$ dtach -c /tmp/bashsession bash

```

To create a new session running *command* without attaching to it:

```
$ dtach -n *socket* 'command

```

### Attach to a session

To attach to an existing session:

```
$ dtach -a *socket*

```

To attach to an existing session, and if not already existing, create it:

```
$ dtach -A *socket*

```

### Detach from a session

In an attached session, type `Ctrl+\`. This key combination can be modified with the `-e` flag.

## Tips and tricks

### Share a session

To share a session with another user, simply [#Create a new session](#Create_a_new_session) and change the permissions on the socket file such that the other user can read and write to it. Then the other user should be able to [attach](#Attach_to_a_session) to the session.