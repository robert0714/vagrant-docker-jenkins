# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos/7"
#  config.vm.box = "chef/centos-7.2"
#    config.vm.box = "bento/centos-7.2"
#    config.vm.box ="ubuntu/trusty64"
#    config.vm.box ="bento/ubuntu-14.04"
#    config.vm.box = "ubuntu/wily64"
  # If you run into issues with Ansible complaining about executable permissions,
  # comment the following statement and uncomment the next one.
  config.vm.synced_folder ".", "/vagrant"
  # config.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=700,fmode=600"]
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
  end
  config.vm.define :cd, primary: true do |cd|
#    cd.vm.network :forwarded_port, host: 8080, guest: 8080
#    cd.vm.network :forwarded_port, host: 5000, guest: 5000
#    cd.vm.network :forwarded_port, host: 2201, guest: 22, id: "ssh", auto_correct: true
    cd.vm.network "private_network", ip: "192.168.50.91"
    cd.vm.network "public_network", bridge: "eno4", ip: "192.168.57.33", auto_config: "false", netmask: "255.255.255.0" , gateway: "192.168.57.1"
    cd.vm.provision "shell", path: "bootstrap.sh"
    cd.vm.provision :shell, inline: 'ansible-playbook /vagrant/ansible/cd.yml -c local -v'
    cd.vm.hostname = "cd"
  end
  config.vm.define :prod do |prod|
#    prod.vm.network :forwarded_port, host: 2202, guest: 22, id: "ssh", auto_correct: true
#    prod.vm.network :forwarded_port, host: 9001, guest: 9001
    prod.vm.network "private_network", ip: "192.168.50.92"
    prod.vm.network "public_network", bridge: "eno4", ip: "192.168.57.34",  netmask: "255.255.255.0" , gateway: "192.168.57.1"	
#   prod.vm.provision :shell, inline: 'ansible-playbook /vagrant/ansible/prod.yml -c local -v'
    prod.vm.hostname = "prod"
  end
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
end
