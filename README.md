# Linux basic configuration

This role is used to config linux basic setting. Supporting features as follows:

* disable firewalld(default operation is not change firewall settings)
* disable selinux(default operation is not change selinux settings)
* enable ntp(default operation is not change ntp settings)
* install epel(default operation is not installing epel)
* install user defined packages

## Inventory file demo

```
vagrant1  ansible_ssh_host=192.168.168.11 ansible_ssh_port=3322 ansible_ssh_user=centos

[linux-basic]
vagrant1

[linux-basic:vars]
linux_basic_disable_firewall=true
linux_basic_disable_selinux=true
linux_basic_ntp_installed=true
linux_basic_install_epel=true
linux_basic_installed_packages=["htop", "nload", "tree", "tmux", "smartmontools", "pciutils", "ethtool", "bind-utils", "tcpdump", "sysstat", "sysbench", "fio", "iperf"]

```

## Role Variables
No required vars.

If you want to disable firewalld, set **linux_basic_disable_firewall** variable to true.

If you want to disable selinux, set **linux_basic_disable_selinux** variable to true.

If you want to install ntp, set **linux_basic_ntp_installed** variable to true.

If you want to install epel, set **linux_basic_install_epel** variable to true.

If you want to install some package ,you should first set **linux_basic_install_epel** variable to true. And then define the packages, for example:

> linux_basic_installed_packages=["htop", "nload", "tree", "tmux", "smartmontools", "pciutils", "ethtool", "bind-utils", "tcpdump", "sysstat", "sysbench", "fio", "iperf"]

## Example Playbook

```
---
- hosts: linux-basic
  become: true
  roles:
    - frank6866.linux_basic
```

License
-------

MIT

