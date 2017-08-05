From [docs.ansible.com](http://docs.ansible.com/):

	*Ansible is an IT automation tool. It can configure systems, deploy software, and orchestrate more advanced IT tasks such as continuous deployments or zero downtime rolling updates.*

## Contents

*   [1 Installation](#Installation)
*   [2 Basic usage](#Basic_usage)
    *   [2.1 Inventory](#Inventory)
    *   [2.2 Ping](#Ping)
    *   [2.3 Playbook](#Playbook)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Telling Ansible where Python is located](#Telling_Ansible_where_Python_is_located)
*   [4 See also](#See_also)

## Installation

On the control machine (server, master), [Install](/index.php/Install "Install") the [ansible](https://www.archlinux.org/packages/?name=ansible) package.

On the managed machines (clients, slaves), where you want to automate deployment or configuration tasks, install [python2](https://www.archlinux.org/packages/?name=python2) and [openssh](https://www.archlinux.org/packages/?name=openssh). (Or you can use [python](https://www.archlinux.org/packages/?name=python) instead of [python2](https://www.archlinux.org/packages/?name=python2), but Python 3 support in Ansible is currently experimental.)

Note that a functioning [SSH key](/index.php/SSH_keys#Copying_the_public_key_to_the_remote_server "SSH keys") setup makes the use of Ansible much more frictionless (but this is not required).

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

## Tips and tricks

### Telling Ansible where Python is located

Ansible requires [Python](/index.php/Python "Python") on the target machine, Python 3 is supported as a preview [[1]](https://docs.ansible.com/ansible/python_3_support.html) but might not work for all modules. By default Ansible assumes it can find a `/usr/bin/python` on your remote system that is a 2.X or 3.X version of Python, specifically 2.4 or higher.

If some of your modules require Python 2 you need to tell Ansible where to find Python 2 by setting the `ansible_python_interpreter` variable in your Ansible inventory file. This can be done succinctly by using host groups in the inventory:

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

More information about Python versions is available in [[2]](https://docs.ansible.com/ansible/python_3_support.html), [[3]](http://docs.ansible.com/faq.html#how-do-i-handle-python-pathing-not-having-a-python-2-x-in-usr-bin-python-on-a-remote-machine) and [[4]](http://docs.ansible.com/intro_inventory.html#list-of-behavioral-inventory-parameters).

## See also

*   [Ansible concept in 12 minutes](https://www.ansible.com/quick-start-video)
*   [pacman module details](http://docs.ansible.com/ansible/latest/pacman_module.html)