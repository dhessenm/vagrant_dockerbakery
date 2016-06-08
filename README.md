# vagrant_dockerbakery
Collection of Vagrant provision scripts (shell, ansible) in directory provision.

Collection of Docker build files in directory dockerbuild.

## Required
- Vagrant 
- VMware Fusion
- Ansible 

## Create Dockerbakery VM
Create an Ubuntu VM and install Docker daemon and Ansible.

```
git clone https://github.com/dhessenm/vagrant_dockerbakery.git
cd vagrant_dockerbakery
vagrant up --provider=vmware_fusion
```

## Build a Dockerimage
Log into VM and build a Dockerimage, e.g. an Ansible Dockerimage.

```
hessen@DMBPr vagrant_dockerbakery $ vagrant ssh
vagrant@machine1:~$ /vagrant/provision/dockerbake/bake ansible
```

## Modifications
It's up to you to make some modifications.

You can change the Vagrant box to any Ubuntu trusty Vagrant box, just make sure VMware-Tools HGFS Support works.

You can uncomment the line in Vagrantfile to automate the Dockerimage build, e.g. build an Ansible Dockerimage directly  with the first `vagrant up`.
```
#     machine1_config.vm.provision "shell", path: "provision/dockerbake/bake", args: "ansible"
```

Have fun!


## semaphore start
First run a Mysql Container
```
docker run -d -p=3306:3306 --name semaphore-db -e MYSQL_ROOT_PASSWORD=<your password> mysql
```
Then run semaphore-app container and link it with mysql container
```
docker run -d -p=3000:3000 --name semaphore-app --link semaphore-db:dockerhub.noncd.rz.db.de/dirkhessenmueller/semaphore-app dockerhub.noncd.rz.db.de/dirkhessenmueller/semaphore-app
```

debug semaphore-app container with interactive docker session:
```
docker run -ti --name semaphore-app-debug --rm --link semaphore-db:dockerhub.noncd.rz.db.de/dirkhessenmueller/semaphore-app dockerhub.noncd.rz.db.de/dirkhessenmueller/semaphore-app /bin/bash
```

