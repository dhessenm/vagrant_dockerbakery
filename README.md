# vagrant_dockerbackery
Collection of Vagrant provision scripts (shell, ansible) in directory provision.

Collection ob Dockerbuild-Files in directory dockerbuild.

## Required
- Vagrant 
- VMware Fusion
- Ansible 

## Create Dockerbakery VM
Create an Ubuntu VM and install Docker daemon and Ansible:

```
git clone https://github.com/dhessenm/vagrant_dockerbakery.git
cd vagrant_dockerbakery
vagrant up --provider=vmware_fusion
```

## build a Dockerimage
Log into VM and build a Dockerimage, e.g. an Ansible Dockerimage

```
hessen@DMBPr vagrant_dockerbakery $ vagrant ssh
vagrant@machine1:~$ /vagrant/provision/dockerbake/bake ansible
```

## Modifications
It's up to you to make some midifications.

You can change the Vagrant Box to any Ubuntu trusty Vagrant Box, just make sure VMware-Tools HGFS Support works 

You can uncomment the line in Vagrantfile to automate the Dockerimage build, e.g. build an Ansible Dockerimage directly  with the first `vagrant up`
```
#     machine1_config.vm.provision "shell", path: "provision/dockerbake/bake", args: "ansible"
```

Have fun!






