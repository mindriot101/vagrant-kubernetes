# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Common settings
  config.vm.box = "centos/7"
  config.vm.synced_folder ".", "/vagrant", enabled: false
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2084"
  end
  config.vm.box_check_update = false

  # Configure the master
  config.vm.define "master" do |master|
    master.vm.network "private_network", ip: "192.168.33.10"

    master.vm.provision "shell", inline: <<-SHELL
      yum update -y
      hostnamectl set-hostname "master"
      reboot
    SHELL
  end

  # Configure the workers
  (1..3).each do |machine_idx|
    machine_name = "node#{machine_idx}"
    config.vm.define machine_name do |node|
      node.vm.network "private_network", ip: "192.168.33.#{10 + machine_idx}"

      node.vm.provision "shell", inline: <<-SHELL
        yum update -y
        hostnamectl set-hostname #{machine_name}
        reboot
      SHELL
    end
  end
end
