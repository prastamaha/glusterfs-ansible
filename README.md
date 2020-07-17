# Ansible Playbook for Deploy 2 Node Glusterfs Cluster

This playbook has been tested on Centos7

## Prerequisites

- 2 vm or physical machine installed centos7 for gluster node
- The gluster node has at least 1 new disk that is separate from the disk that is installed os
- Gluster node connected to the internet
- The control node (it could be localhost) has been installed ansible
- The gluster node has been installed ssh server
- Control node can access gluster node though ssh without password

## Installation

- __Clone The Repository__

```
$ git clone https://github.com/prastamaha/glusterfs-ansible.git
$ cd glusterfs-ansible
```

- __Inventory Configuration__

Inventory Hosts file available on `inventory/hosts`. Edit the file and match it to your server environment

The default value will look like this

```
$ cat inventory/hosts
```

```
[gluster]
server1 ansible_user=root
server2 ansible_user=root
```

- __Playbook Variable Configuration__

Adjust the variables in `vars/config.yml` to your server environment

The default value will look like this

```
$ cat vars/config.yml
```

```
# server1
server1_ip_address: 10.1.1.164
server1_hostname: server1

#server2
server2_ip_address: 10.1.1.87
server2_hostname: server2

# note: must use a new disk that has not been partitioned / os installed
# gluster disk 
disk_device: /dev/vdb
partition_size: 2GiB

# brick 
brick_path: /bricks/brick1
brick_fstype: ext4

# volume 
volume_name: vol0
# choose ( replicated / distributed )
volume_type: distributed
```

- __Run The Playbook__

```
$ ansible-playbook glusterfs.yml
```
