# vagrant_dockerbackery
Collection of Vagrant provision scripts (shell, ansible) in directory provision.
Collection ob Dockerbuild-Files in directory dockerbuild.

## Required
- Vagrant 
- VMware Fusion
- Ansible 

## Create Dockerbakery VM
Create a Ubuntu VM and install Docker daemon and Ansible:

```
git clone https://github.com/dhessenm/vagrant_dockerbakery.git
cd vagrant_dockerbakery
vagrant up --provider=vmware_fusion
```





