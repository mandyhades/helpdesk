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

#!/bin/bash

# Download and install Oracle Database
wget <oracle_database_download_url>
sudo dpkg -i <oracle_database_file>

# Configure Oracle Database (adjust as needed)
sudo su - oracle
sqlplus / as sysdba <<EOF
CREATE USER <your_username> IDENTIFIED BY <your_password>;
GRANT CONNECT, RESOURCE TO <your_username>;
EOF
exit


