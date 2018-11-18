# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-16.04"
  config.vm.box_version = "= 2.3.5"
  config.vm.synced_folder ".", "/vagrant"
  config.vm.network "forwarded_port", guest: 8000, host: 8000, host_ip: "127.0.0.1"
  # config.vm.network "private_network", ip: "192.168.205.10"
  config.vm.network :public_network, ip: "192.168.0.160"
  
  # Work around disconnected virtual network cable.
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--cableconnected1", "on"]
    # vb.vm.network "private_network", ip: "192.168.205.10"
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get -qqy update
    sudo apt-get install nginx -y
    sudo  apt install default-jdk -y
    sudo apt-get update

    wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
    sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
    sudo apt-get update
    sudo apt-get install jenkins -y
    sudo ufw allow 8080
    sudo ufw allow OpenSSH
    sudo ufw enable -y
    echo sudo ufw status
    echo "Done installing your virtual machine!"
  SHELL
end
