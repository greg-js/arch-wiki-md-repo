From [docs.ansible.com](http://docs.ansible.com/):

	*Ansible is an IT automation tool. It can configure systems, deploy software, and orchestrate more advanced IT tasks such as continuous deployments or zero downtime rolling updates.*

## Contents

*   [1 Installation](#Installation)
*   [2 Basic usage](#Basic_usage)
    *   [2.1 Inventory](#Inventory)
    *   [2.2 Ping](#Ping)
    *   [2.3 Playbook](#Playbook)
    *   [2.4 Vault](#Vault)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 User account creation](#User_account_creation)
    *   [3.2 Python binary location](#Python_binary_location)
*   [4 See also](#See_also)

## Installation

On the control machine (server, master), [Install](/index.php/Install "Install") the [ansible](https://www.archlinux.org/packages/?name=ansible) package. [python](https://www.archlinux.org/packages/?name=python) is also required (Python versions 2.6, 2.7 or 3.5 and higher are supported).

On the managed machines (clients, slaves), where you want to automate deployment or configuration tasks, you need a way to communicate, which is normally [SSH](/index.php/SSH "SSH"). Note that a functioning [SSH key](/index.php/SSH_keys#Copying_the_public_key_to_the_remote_server "SSH keys") setup eases the use of Ansible but is not required.

## Basic usage

### Inventory

According to the default settings in `/etc/ansible/ansible.cfg`, one can define its infrastructure in `/etc/ansible/hosts`. For instance, the following inventory defines a tiny cluster with three nodes:

 `/etc/ansible/hosts` 
```
[control]
192.168.12.1

[managed]
192.168.12.2
192.168.12.3

```

One can assign specific attributes to every node in the file. Check [the official document](http://docs.ansible.com/ansible/latest/intro_inventory.html) for details.

### Ping

You may check if all the nodes listed in the inventory are alive by

```
$ ansible all -m ping

```

### Playbook

Playbooks are the main organizational unit to configure and deploy the whole infrastructure. Check [the official document](http://docs.ansible.com/ansible/latest/playbooks.html) for more details. Here is an extremely simple demonstration, where the administrator of the above inventory wants to perform a full system upgrade on a set of Arch Linux hosts. First, create a playbook file, with YAML formatting (*always* 2 spaces indentation):

 `syu.yml` 
```
---
- name: All hosts up-to-date
  hosts: control managed
  become: yes

  tasks:
    - name: full system upgrade
      pacman:
        update_cache: yes
        upgrade: yes

```

Then, run the playbook script:

```
# ansible-playbook --ask-become-pass syu.yml

```

### Vault

A [vault](http://docs.ansible.com/ansible/latest/playbooks_vault.html#using-vault-in-playbooks) can be used to keep sensitive data in an encrypted form, rather than plaintext, in playbooks or roles. The vault password can be stored in plaintext in a file. It can be created with `echo myvaultpassword > vault_pass.txt` to be used later on with Ansible as follows:

```
ansible-playbook site.yml --vault-id vault_pass.txt

```

In order to encrypt the content `varcontent` of a variable named `varname`, the following command should be used:

```
ansible-vault encrypt_string --vault-id vault_pass.txt varcontent -n varname

```

It returns directly the protected variable that can be inserted into a playbook. Encrypted and non-encrypted variables can be mixed together in a YAML file:

```
notsecret: myvalue
mysecret: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          66386439653236336462626566653063336164663966303231363934653561363964363833313662
          6431626536303530376336343832656537303632313433360a626438346336353331386135323734
          62656361653630373231613662633962316233633936396165386439616533353965373339616234
          3430613539666330390a313736323265656432366236633330313963326365653937323833366536
          3462
other_plain_text: othervalue
```

## Tips and tricks

### User account creation

Ansible is able to manage user accounts and in particular to create new ones. This is achieved in playbooks with the [user module](http://docs.ansible.com/ansible/latest/user_module.html) which takes an optional `password` argument to set the user's password. It is the **hashed value of the password** that needs to be provided to the module. The hashing can simply be performed on the fly within Ansible using one of the internal [hashing filters](http://docs.ansible.com/ansible/latest/playbooks_filters.html#hash-filters):

```
- user:
   name: madhead
   password: "{{ 'user_password' | password_hash('sha512', 'permsalt') }}"
   shell: /usr/bin/nologin

```

**Tip:** The salt should be fixed and explicitely supplied as a second parameter of the hash function for the operation to be indempotent (can be repeated without changing the state of the system).

With this approach it is recommended to vault-encrypt *user_password* so that it does not appear in plain text, see [#Vault](#Vault). However, an encrypted variable cannot be piped directly and will first need to be assigned to another one that will be piped.

Alternatively, the hashing can be performed outside Ansible. The following commands return respectively the MD5 and the SHA512 hashed values of *user_password*:

```
$ openssl passwd -1 user_password

```

```
$ python -c 'import crypt; print(crypt.crypt("user_password", crypt.mksalt(crypt.METHOD_SHA512)))'

```

### Python binary location

Ansible requires [Python](/index.php/Python "Python") on the target machine. By default Ansible assumes it can find a `/usr/bin/python` on your remote system that is a 2.X or 3.X version of Python, specifically 2.6 or higher.

If some of your modules specifically require Python2 you need to inform Ansible about its location by setting the `ansible_python_interpreter` variable in your inventory file. This can be done by using host groups in the inventory:

 `Inventory file` 
```
[archlinux]
server1
server2

[debian]
server3

[archlinux:vars]
ansible_python_interpreter=/usr/bin/python2
```

More information about Python versions is available in [[1]](https://docs.ansible.com/ansible/python_3_support.html), [[2]](http://docs.ansible.com/faq.html#how-do-i-handle-python-pathing-not-having-a-python-2-x-in-usr-bin-python-on-a-remote-machine) and [[3]](http://docs.ansible.com/intro_inventory.html#list-of-behavioral-inventory-parameters).

## See also

*   [Ansible concept in 12 minutes](https://www.ansible.com/quick-start-video)
*   [pacman module details](http://docs.ansible.com/ansible/latest/pacman_module.html)