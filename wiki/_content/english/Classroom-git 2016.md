This is the sign up page for a GIT class/workshop being held in 2016\. You only need to sign up if you want access to the git repo hosted by Arch Linux Women for the class. You can still go to the class and learn without signing up. Instructions to share your ssh key are below.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Create an SSH Key](#Create_an_SSH_Key)
*   [2 Share Your Public Key](#Share_Your_Public_Key)
*   [3 Sign Up](#Sign_Up)
    *   [3.1 Help](#Help)

### Create an SSH Key

You will need an ssh key to access git on the [Arch Women](https://archwomen.org) servers. If you don't have a key, you can create one by running:

```
 ssh-keygen

```

For more information on creating key pairs see, [SSH keys](/index.php/SSH_keys "SSH keys")

### Share Your Public Key

After generating key pairs you should have a public and private key in `~/.ssh`. The public key has the extension `.pub`. To paste your public key to [ptpb.pw](https://ptpb.pw) do:

```
cat ~/.ssh/id_rsa.pub | curl -F c=@- https://ptpb.pw/

```

Make **sure** the key you paste has the `.pub` extension, you don't want to publicly share your private key.

## Sign Up

Add the nick you want to use on git and a link to your public key to the table.

| Nick | SSH Public Key |
| meskarune | [public key](https://ptpb.pw/vj4X/sh) |
| ripelascra | [public key](https://ptpb.pw/9HEG/sh) |
| therue | [public key](https://ptpb.pw/2pnP/sh) |
| cirrusUK | [public key](https://ptpb.pw/6di9/sh) |
| 5225225 | [public key](https://ptpb.pw/TVjm/sh) |
| merriment | [public key](https://ptpb.pw/OtzU/sh) |
| nick | key |

### Help

If you have questions or need additional help join the #archlinux-newbie or #archlinux-women irc channels on irc.freenode.net.