# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"


Vagrant.configure(2) do |config|
  config.vm.box = "generic/ubuntu2004"

  #config.vm.network "private_network", ip: "10.0.4.91"

  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder ".", "/vagrant"
  config.vm.box_version = "3.1.16"
  config.vm.provision:shell, inline: <<-SHELL
      echo "root:rootroot" | sudo chpasswd
      sudo timedatectl set-timezone Asia/Kolkata
  SHELL
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
     vb.name = "ubuntu-docker-host"
     vb.gui = false
     vb.cpus = 2
  
     # Customize the amount of memory on the VM:
     vb.memory = "4096"
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get -y update && sudo apt install -y ansible
    sudo ansible-galaxy install geerlingguy.pip geerlingguy.docker
    ansible-playbook /vagrant/docker.yml
  SHELL
end
