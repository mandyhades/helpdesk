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


# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Specify the base box to use
  config.vm.box = "ubuntu/focal64"  # Replace with your desired base box

  # Configure the Oracle Database installation
  config.vm.provision :shell do |s|
    s.path = "install_oracle.sh"
    s.args = ["<oracle_database_file>"]  # Replace with the path to your Oracle Database file
  end
end

