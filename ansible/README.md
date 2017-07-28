# Ansible playbook

This is intended to convert a small Debian server into a FreeRADIUS server with support for WPA2-Enterprise.

We suggest creating a small VM and installing basic Debian Stretch.

Make sure to configure SSH keys and sudo first, so you can login and run sudo commands.

Create a small ansible hosts file similar to:
```
# Default settings, if you want to change SSH port
[all:vars]
ansible_ssh_port=22

[radius]
radius ansible_ssh_host=10.1.2.3

# Consider using ansible for all your servers
#[infrastructure]
# OpenBSD Servers - need python_interpreter specified
#server01 ansible_ssh_host=10.0.0.4      ansible_python_interpreter=/usr/local/bin/python
#...
```

and run ansible using:
```
ansible -i hosts -K configure-freeradius.yml -l radius
```

This should perform multiple actions, like:

* Install the FreeRADIUS software
* Configure the FreeRADIUS software for WPA2-Enterprise
* Adding a configuration to allow any username and password configuration

Note: This recipe can also turn on the firewall if you want to, see and uncomment the lines/tasks in the code if you want that.


### configure SSH

Ansible uses SSH and it is highly recommended to use keys, so install your key with a command like:
```
ssh-copy-id -i .ssh/yourkey radius.example.com
```

### Configure Sudo

If you are part of the admin group on Debian you can use sudo
