# -*- mode: ruby -*-
# vi: set ft=ruby :

#Load vagrant api version 2 and assing to 'config'
Vagrant.configure("2") do |config|

  config.vm.box_check_update = "false"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"
  end

  config.vm.define "forensics" do |subconfig|
    subconfig.vm.hostname = "forensics"
    subconfig.vm.box = "hashicorp/bionic64"
    subconfig.vm.network :private_network, ip: "192.168.60.10"
    subconfig.vm.provision "shell" do |s|
        ssh_pub_key = File.readlines("#{Dir.home}/.ssh/ansible_private_key.pub").first.strip
        s.inline = <<-SHELL
          echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
        SHELL
      end
      subconfig.vm.provision "ansible" do |ansible|
        ansible.playbook="main.yml"
      end
  end

end
