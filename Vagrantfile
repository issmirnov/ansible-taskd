# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"

# Multiple VMs: http://www.thisprogrammingthing.com/2015/multiple-vagrant-vms-in-one-vagrantfile/
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # create bare vm for ubuntu 16.04
  config.vm.define :taskd do |taskd|
    taskd.vm.box = "ubuntu/xenial64"
    taskd.vm.hostname = "taskd"
    taskd.vm.network :private_network, ip: "192.168.33.48"

    taskd.vm.provider :virtualbox do |v|
      v.name = "taskd"
      v.memory = 1024
      v.cpus = 2
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    taskd.vm.provision "ansible", run: "always" do |ansible|
      ansible.playbook = "vagrant.yml"
      ansible.become = true
      ansible.compatibility_mode = "2.0"
      #ansible.verbose = "vv"
    end
  end

end
