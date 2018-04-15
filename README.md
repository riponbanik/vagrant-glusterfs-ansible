# vagrant-glusterfs-ansible

This repository is suitable to use in Windows since it uses ansible-local provisioner.
It will installation 3 nodes cluster. Change the value of N to resize the number of nodes. 

It depends on the glusterfs ansible role. Download [glusterfs role] (https://galaxy.ansible.com/geerlingguy/glusterfs/) into the roles directory after cloning the repo.

## Plugins

The followng plugings needs to be installed for vagrant.

1. [vagrant host manager](https://github.com/devopsgroup-io/vagrant-hostmanager)
2. [vagrant cachier](https://github.com/fgrehm/vagrant-cachier)


## Build the cluster
```
git clone https://github.com/riponbanik/vagrant-glusterfs-ansible
cd vagrant-glusterfs-ansible
vagrant up 
```
## Provision the cluster
To re-provision the cluster after build is complete, run the following command -
```
ansible-playbook -i inventory playbook.yml --become
```
## Troubleshooting 

After the build is complete, us the following comannds to ssh into one of the node and
check the status

```
vagrant ssh gluster-node1
gluster peer status
gluster volume info
```

## When you're done, you can shut down the cluster using
```
vagrant destroy -f
```


