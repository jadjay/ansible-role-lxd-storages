# Ansible Role : lxd-storages

Creation of the storages on a remote lxd.

Third stage to enable the creation of containers.

## Requirements

- A working installation of LXD local and distant
- A network connection between LXDs
- A ssh connection from local to remote

## Inventory

- need a _Container ship(s)_ group, which will be the hosts of the role
- each host in this group need to be detailled as such:
  - _alias-or-hostname_ [ ansible_host=_ipaddress-or-else_ ]

## Role Variables

Variable for the role are:

- lxd_storages : List of storages objects
  - name: the name of the storage
  - mode: 
  - size: 
  - description: useless at now

### 2 modes : vlan / local

- Local mode is for local network with private network
  - it can be connected to real network via an interface_phy
  - it can be accessed via the vxlan tunnel from the ansible host
  - its containers have an automatic dhcp address
- vlan mode is for physic/public network 
  - its dhcp is off
  - it has to be connected with a vlan interface (eg : eth0.234 vlan 234 on interface eth0)
  - its container need to have a static ip, in ansible its needed to set this address via lxd_connection


## Example playbook

### Inventory

```
[containerships]
clementine ansible_host=2.16.3.168
gudrun     ansible_host=cs.maersk.com
```

### Playbook

```
- hosts: containerships
  roles:
    - jadjay.lxd-storages
```

### Variables

*File: group_vars/containerships.yml*
```
lxd_storages:
  - name: baarwerk42
    mode: 
    size:
    description: "Zone nummer 42"
```

# License

GNU/GPLv3

# Author Information

This role was created in 2017 by Jerome Avond.

