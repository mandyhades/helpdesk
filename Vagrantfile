# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "oraclebase/oracle-18c-xe"
  config.vm.network "forwarded_port", guest: 1521, host: 1521
  config.vm.network "forwarded_port", guest: 5500, host: 5500

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    # Additional setup commands can be added here
    echo "Oracle Database XE setup complete"
  SHELL
end

Vagrant.configure("2") do |config|
  config.vm.box = "oraclelinux/7"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    yum install -y oracle-database-preinstall-21c
    yum install -y oracle-database-xe-21c
    /etc/init.d/oracle-xe-21c configure
  SHELL
end
