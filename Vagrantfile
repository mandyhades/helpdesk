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
  # Sử dụng Oracle Linux 7 từ repo Vagrant chính thức của Oracle
  config.vm.box = "oraclelinux/7"

  # Cấu hình mạng cho máy ảo
  config.vm.network "private_network", type: "dhcp"

  # Cấu hình bộ nhớ và CPU cho máy ảo
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"  # Tăng bộ nhớ RAM nếu cần thiết
    vb.cpus = 2         # Số lượng CPU
  end

  # Script provision để cài đặt Oracle Database
  config.vm.provision "shell", inline: <<-SHELL
    # Cập nhật hệ thống
    yum update -y

    # Cài đặt các gói cần thiết cho Oracle Database
    yum install -y oracle-database-preinstall-19c

    # Tải xuống Oracle Database (bạn cần tải file zip thủ công và đặt vào thư mục cài đặt)
    cd /vagrant
    if [ ! -f LINUX.X64_193000_db_home.zip ]; then
      echo "Vui lòng tải Oracle Database 19c từ trang web Oracle và đặt file LINUX.X64_193000_db_home.zip vào thư mục này."
      exit 1
    fi

    # Giải nén và cài đặt Oracle Database
    unzip LINUX.X64_193000_db_home.zip -d /opt/oracle
    /opt/oracle/database/runInstaller -silent -responseFile /opt/oracle/database/response/db_install.rsp -ignorePrereqFailure

    # Thiết lập Oracle
    /opt/oracle/product/19c/dbhome_1/root.sh
    /opt/oracle/product/19c/dbhome_1/runInstaller -executeConfigTools -responseFile /opt/oracle/database/response/dbca.rsp -silent

    # Thiết lập cấu hình môi trường Oracle
    echo "export ORACLE_HOME=/opt/oracle/product/19c/dbhome_1" >> /home/vagrant/.bashrc
    echo "export PATH=\$ORACLE_HOME/bin:\$PATH" >> /home/vagrant/.bashrc
    source /home/vagrant/.bashrc

    echo "Oracle Database đã được cài đặt thành công."
  SHELL
end

