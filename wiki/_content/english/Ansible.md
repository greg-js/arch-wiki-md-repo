From [docs.ansible.com](http://docs.ansible.com/):

	*Ansible is an IT automation tool. It can configure systems, deploy software, and orchestrate more advanced IT tasks such as continuous deployments or zero downtime rolling updates.*

## Installation

[Install](/index.php/Install "Install") the [ansible](https://www.archlinux.org/packages/?name=ansible) package. The remote machine where you want to automate deployment or configuration tasks only requires a Python interpreter and an [OpenSSH server](/index.php/Openssh "Openssh").

### Telling Ansible where Python is located

Ansible requires [Python](/index.php/Python "Python") on the target machine, Python 3 is supported as a preview [[1]](https://docs.ansible.com/ansible/python_3_support.html) but might not work for all modules. By default Ansible assumes it can find a `/usr/bin/python` on your remote system that is a 2.X or 3.X version of Python, specifically 2.4 or higher.

If some of your modules requires Python 2 you need to tell Ansible where to find Python 2 by setting the `ansible_python_interpreter` variable in your Ansible inventory file.

More information this is available in [[2]](https://docs.ansible.com/ansible/python_3_support.html), [[3]](http://docs.ansible.com/faq.html#how-do-i-handle-python-pathing-not-having-a-python-2-x-in-usr-bin-python-on-a-remote-machine) and [[4]](http://docs.ansible.com/intro_inventory.html#list-of-behavioral-inventory-parameters).