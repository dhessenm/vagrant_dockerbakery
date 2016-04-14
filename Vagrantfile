# -*- mode: ruby -*-

# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

$script = <<SCRIPT
# set root password
echo root:vagrant | chpasswd

SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "dh/ubuntu-14.04.2"

  # Turn off shared folders
  # config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true
  # config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true

  # Begin machine1
  config.vm.define "machine1" do |machine1_config|
    machine1_config.vm.hostname = "machine1"

    machine1_config.vm.provision "shell", inline: $script

    # eth1
    # machine1_config.vm.network "private_network", ip: "192.168.236.20"

    machine1_config.vm.provider "vmware_fusion" do |v|
        v.vmx["memsize"] = "2048"
        v.vmx["numvcpus"] = "1"
        v.vmx["vhv.enable"] = "TRUE"
    end

    machine1_config.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--memory", "2048"]
        v.customize ["modifyvm", :id, "--cpus", "1"]
    end
    machine1_config.vm.provision :ansible do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "provision/dockerhost/playbook.yml" 
    end
    machine1_config.vm.provision :ansible do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "provision/ansible/playbook.yml" 
    end
#     machine1_config.vm.provision "shell", path: "provision/dockerbake/bake", args: "ansible"
  end
  # End machine1

end

