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
  - mode: the type of storage (actually : only *dir* is available)
  - size: useless at now
  - description: useless at now

### 1 mode : dir

- dir mode is for local directory 
  - it's a simple directory local to the LXD host
  - Can't have a limited size

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
    mode: dir
    size: false
    description: "Zone nummer 42"
```

# License

GNU/GPLv3

# Author Information

This role was created in 2017 by Jerome Avond.

