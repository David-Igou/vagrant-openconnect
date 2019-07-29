# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "geerlingguy/centos7"
  config.vm.provider "virtualbox"
  config.vm.provider "virtualbox" do |vb|
     # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end

  config.vm.provision "file", source: "system-connections", destination: "~/system-connections"

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell" do |s|
    s.inline = <<-SHELL
      cp /home/vagrant/system-connections/* /etc/NetworkManager/system-connections/
      chmod 600 /etc/NetworkManager/system-connections/*
      yum install -y epel-release
      yum install -y vim NetworkManager-openconnect
      echo "nmcli con up my-vpn-connection --ask" > /etc/motd
      systemctl restart NetworkManager
      exit 0
    SHELL
  end
end
