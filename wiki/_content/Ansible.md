# Ansible

From [docs.ansible.com](http://docs.ansible.com/):

NaN

## Installation

[Install](/index.php/Install "Install") the [ansible](https://www.archlinux.org/packages/?name=ansible) package. The remote machine where you want to automate deployment or configuration tasks only requires a Python interpreter and an [OpenSSH server](/index.php/Openssh "Openssh").

### Telling Ansible where Python2 is located

Ansible requires [Python](/index.php/Python "Python") 2 on the target machine (but support for Python 3 is going to be [added](https://github.com/ansible/ansible/issues/1409)). By default Ansible assumes it can find a `/usr/bin/python` on your remote system that is a 2.X version of Python, specifically 2.4 or higher.

Since Arch Linux defaults to Python 3, you need to tell Ansible where to find Python 2 by setting the `ansible_python_interpreter` variable in your Ansible inventory file.

More information about this is available in [[1]](http://docs.ansible.com/faq.html#how-do-i-handle-python-pathing-not-having-a-python-2-x-in-usr-bin-python-on-a-remote-machine) and [[2]](http://docs.ansible.com/intro_inventory.html#list-of-behavioral-inventory-parameters).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Ansible&oldid=412506](https://wiki.archlinux.org/index.php?title=Ansible&oldid=412506)"