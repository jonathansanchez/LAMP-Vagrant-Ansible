# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
sudo yum install -y epel-release
sudo yum install -y ansible
SCRIPT

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.ssh.private_key_path = ["provision_key", "~/.vagrant.d/insecure_private_key"]
  config.vm.provision "file", source: "provision_key.pub", destination: "~/.ssh/authorized_keys"

  config.vm.define "provisioner" do |provisioner|
  	provisioner.vm.box = "centos/7"
  	provisioner.vm.network :private_network, ip: "10.0.0.2"
    provisioner.vm.synced_folder ".", "/vagrant"
    provisioner.vm.synced_folder "ansible", "/ansible", create: true
    provisioner.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
    provisioner.vm.provision "shell", inline: $script
  end

  config.vm.define "www" do |www|
  	www.vm.box = "centos/7"
    www.vm.network :private_network, ip: "10.0.0.10"
    www.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
  end
end

