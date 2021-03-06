# Linux basic configuration

This role is used to config linux basic setting. Supporting features as follows:

* disable firewalld(default operation is not change firewall settings)
* disable selinux(default operation is not change selinux settings)
* enable ntp(default operation is not change ntp settings)
* install epel(default operation is not installing epel)
* install user defined packages
* config /etc/hosts file
* add sysctl entries
* add sudo/normal users

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
linux_basic_installed_packages=["htop", "nload", "tree", "tmux", "smartmontools", "pciutils", "ethtool", "bind-utils", "tcpdump", "sysstat", "sysbench", "fio", "iperf", "iptraf"]

```

## Role Variables
No required vars.

If you want to disable firewalld, set **linux_basic_disable_firewall** variable to true.

If you want to disable selinux, set **linux_basic_disable_selinux** variable to true.

If you want to set timezone, set **linux_basic_timezone** variable to you timezone as you want, eg, "Asia/Shanghai"

If you want to install ntp, set **linux_basic_ntp_installed** variable to true.

If you want to install epel, set **linux_basic_install_epel** variable to true.

If you want to install some package ,you should first set **linux_basic_install_epel** variable to true. And then define the packages, for example:

> linux_basic_installed_packages=["htop", "nload", "tree", "tmux", "smartmontools", "pciutils", "ethtool", "bind-utils", "tcpdump", "sysstat", "sysbench", "fio", "iperf"]


If you want to config /etc/hosts file, setting the **ip_hostname_in_etc_hosts** variable:

```
ip_hostname_in_etc_hosts:
  - ip: 192.168.168.201
    hostname: vagrant-1
    state: present
  - ip: 192.168.168.202
    hostname: vagrant-2
    state: present
```


If you want to define sysctl entries, setting the **ip_hostname_in_etc_hosts** variable:

```
linux_basic_sysctl_pair:
  - name: vm.swappiness
    value: 0
  - name: net.ipv4.ip_forward
    value: 1
```


If you want to create sudo users, you can set the **linux_basic_users** variable:

```
linux_basic_users:
  - name: frank6866
    state: present
    public_key: ssh-rsa xxx
    group: wheel
```

If you want to create normal users, remove the group key in **linux_basic_users** variable.


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

